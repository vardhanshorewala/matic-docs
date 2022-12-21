---
id: secrets
title: Distribuição de segredos na banda
sidebar_label: In Band Secret Distribution
description: "Uma solução para criptografar segredos e garantir a sua descriptografia."
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

## Visão geral {#overview}

Para garantir que um destinatário receba as informações secretas necessárias para gastar os seus compromissos, o remetente criptografa esses segredos (*sal*, *valor*, *IDtoken*, *EndereçoErc*) do compromisso enviado para o destinatário e comprova usando a ZKP que criptografaram isto corretamente com a chave pública do destinatário. É utlizado o paradigma de criptografia híbrida [**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf).

## Criptografia híbrida KEM-DEM {#kem-dem-hybrid-encryption}


### Criação de chave {#key-creation}

Use a curva elíptica (aqui usamos a curva Baby Jubjub) `E` num campo finito `Fp`, onde `p` é um grande prime e `G` é o gerador.

Alice gera um par de chaves assimétricas efémeras e aleatórias   :$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

Estas chaves são usadas apenas uma vez, e são exclusivas para esta transação, possibilitando manter o segredo de forma perfeita no futuro.

### Criptografia {#encryption}

O processo de criptografia envolve 2 etapas: uma etapa KEM para obter uma chave de criptografia simétrica de um segredo compartilhado e uma etapa DEM para criptografar texto simples usando a chave de criptografia.

### Método de encapsulamento da chave (criptografia) {#key-encapsulation-method-encryption}
Usando a chave privada assimétrica gerada anteriormente, obtemos um segredo compartilhado, $key_{DH}$, usando o padrão Diffie-Hellman. É criptografado em hash juntamente com a chave pública efémera para obter a chave de criptografia.

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


onde  
   é a chave pública do destinatário  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### Método de encapsulamento de dados (criptografia) {#data-encapsulation-method-encryption}
Para eficiência do circuito, a criptografia usada é uma cifra de bloco no modo de contador, onde o algoritmo de cifra é um hash mimc. Dado que as chaves efémeras são únicas para cada transação, não há necessidade de incluir um nonce. A criptografia da mensagem $i^{th}$ é a seguinte:

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

onde  

$Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

O remetente fornece então ao destinatário $(Q_e, \text{ciphertexts})$. São incluídos como parte da estrutura de transação enviada on-chain.

### Descriptografia {#decryption}
Para descriptografar, o destinatário executa uma versão ligeiramente modificada das etapas KEM-DEM.

### Método de encapsulamento de chave (descriptografia) {#key-encapsulation-method-decryption}
Considerando $Q_e$, o destinatário é capaz de calcular a chave de criptografia localmente executando as seguintes etapas.

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

onde  
   é a chave pública efémera  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### Método de encapsulamento de dados (descriptografia) {#data-encapsulation-method-decryption}
Com $key_{enc}$ and an array of ciphertexts, the $i_{th}$, texto simples pode ser recuperado com o seguinte:

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

onde  

$Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## Derivação e geração das várias chaves envolvidas na criptografia, propriedade dos compromissos e gastos {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

Usando BIP39 gere um `mnemonic` de 12 palavras e a partir disto gerar um `seed` chamando `mnemonicToSeedSync`. Depois, seguindo os padrões de BIP32 e BIP44, gere um `rootKey` com base neste `seed` e `path`.

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

Se `rootKey` ou `mnemonic` estiver comprometido, o adversário pode calcular `zkpPrivateKey` e `nullifierKey`.
O `zkpPrivateKey` pode ser usado para descriptografar segredos de um compromisso enquanto o `nullifierKey` pode ser usado para gastar o compromisso.
Portanto, `rootKey` e `mnemonic` devem ser armazenados com muita segurança.

As aplicações que usarão o `ZkpKeys` para gerar estas chaves podem armazenar o `rootKey` em diferentes dispositivos dividindo isto em compartilhamentos usando o Shamir Secret Sharing.

Também é recomendável armazenar `zkpPrivateKey` e `nullifierKey` separadamente para evitar o roubo de compromissos caso um deles esteja comprometido.

A figura abaixo mostra as etapas para obter as diferentes chaves no Nightfall![](../imgs/key-derivation.png)
