---
id: secrets
title: Distribuzione in-band dei segreti
sidebar_label: In Band Secret Distribution
description: "Una soluzione per crittografare i segreti e garantirne la decrittazione."
keywords:
  - docs
  - polygon
  - nightfall
  - secret
  - encryption
  - key
image: https://matic.network/banners/matic-network-16x9.png
---
import katex from 'katex';

## Panoramica {#overview}

Per assicurare che un destinatario riceva le informazioni segrete necessarie per spendere i propri impegni, il mittente
crittografa i segreti (*salt*, *value*, *tokenId*, *ercAddress*) dell'impegno inviati al destinatario e
dimostra tramite ZKP che i segreti sono stati correttamente crittografati con la chiave pubblica del destinatario. A tal fine, viene utilizzato il paradigma di crittografia ibrida [**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf).

## Crittografia ibrida KEM-DEM {#kem-dem-hybrid-encryption}


### Creazione della chiave {#key-creation}

Utilizza la curva Ellittica (qui utilizziamo una curva Baby Jubjub) `E` su un campo finito `Fp` in cui `p` è
un numero primo e `G` è il generatore.

Alice genera una coppia di chiavi asimmetrica effimera casuale   :
$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

Queste chiavi sono utilizzate una sola volta e sono specifiche per questa transazione, garantendoci una perfect forward secrecy.

### Crittografia {#encryption}

Il processo di crittografia prevede 2 fasi: una fase KEM per ricavare una chiave crittografica simmetrica da un segreto condiviso e una fase DEM per crittografare i testi non crittografati utilizzando la chiave crittografica.

### Metodo di incapsulamento della chiave, o KEM (crittografia) {#key-encapsulation-method-encryption}
Utilizzando la chiave privata asimmetrica precedentemente generata, otteniamo un segreto condiviso, $key_{DH}$, utilizzando lo standard Diffie-Hellman. Questo viene sottoposto a hash insieme alla chiave pubblica effimera per ottenere la chiave crittografica.

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


dove  
   è la chiave pubblica del destinatario  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### Metodo di incapsulamento dei dati, o DEM (crittografia) {#data-encapsulation-method-encryption}
Per assicurare l'efficienza del circuito, la crittografia utilizzata è una cifratura a blocchi in modalità contatore, in cui l'algoritmo di cifratura è un hash mimc. Dato che le chiavi effimere sono univoche per ciascuna transazione, non è necessario includere una nonce. La crittografia del messaggio $i^{th}$ è la seguente:

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

dove  

$Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

Quindi, il mittente fornisce $(Q_e, \text{ciphertexts})$ al destinatario. Queste sono incluse nella transazione struct inviata on-chain.

### Decrittazione {#decryption}
Per procedere alla decrittazione, il destinatario esegue una versione leggermente modificata dei passaggi KEM-DEM.

### Metodo di incapsulamento delle chiavi, o KEM (decrittazione) {#key-encapsulation-method-decryption}
Dato $Q_e$, il destinatario è in grado di calcolare la chiave crittografica a livello locale eseguendo i passaggi seguenti.

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

dove  
   è la chiave pubblica effimera  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### Metodo di incapsulamento dei dati, o DEM (decrittazione) {#data-encapsulation-method-decryption}
Con $key_{enc}$ and an array of ciphertexts, the $i_{th}$, è possibile recuperare il testo non crittografato come segue:

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

dove  

$Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## Derivazione e generazione delle chiavi coinvolte nella crittografia, proprietà degli impegni e spesa {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

Utilizzando BIP39, genera `mnemonic` da 12 parole, quindi genera `seed` chiamando `mnemonicToSeedSync`.
Successivamente, seguendo gli standard di BIP32 e BIP44, genera `rootKey` basato su `seed` e `path`.

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

Se `rootKey` o `mnemonic` sono compromessi, allora l'avversario può calcolare `zkpPrivateKey` e `nullifierKey`.
È possibile utilizzare `zkpPrivateKey` per decrittare i segreti di un impegno e `nullifierKey` per spendere l'impegno stesso.
È quindi fondamentale conservare `rootKey` e `mnemonic` in maniera molto sicura.

Le app che utilizzano `ZkpKeys` per generare le chiavi possono memorizzare `rootKey` in dispositivi diversi, suddividendole
in quote tramite l'algoritmo Shamir Secret Sharing.

È inoltre consigliato conservare `zkpPrivateKey` e `nullifierKey` separatamente, in modo da evitare il furto di impegni nel caso in cui
una delle due sia compromessa.

La figura di seguito mostra i passaggi per ricavare le varie chiavi in Nightfall
![](../imgs/key-derivation.png)
