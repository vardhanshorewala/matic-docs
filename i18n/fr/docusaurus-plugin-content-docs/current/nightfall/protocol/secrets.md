---
id: secrets
title: Distribution des secrets en bande
sidebar_label: In Band Secret Distribution
description: "Une solution pour chiffrer les secrets et assurer leur déchiffrement."
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

## Aperçu {#overview}

Pour s'assurer qu'un destinataire reçoit les informations secrètes requises pour dépenser ses engagements, l'expéditeur
chiffre les secrets (*salt*, *valeur*, *tokenId*, *ercAddress*) de l'engagement envoyé au destinataire et
prouve à l'aide de ZKP qu'ils l'ont chiffré correctement avec la clé publique du destinataire. Le paradigme de chiffrement hybride [**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf) est utilisé.

## Chiffrement hybride KEM-DEM {#kem-dem-hybrid-encryption}


### Création de clé {#key-creation}

Utilisez la courbe elliptique (ici nous utilisons la courbe de Baby Jubjub) `E` sur un champ fini `Fp` où `p` est un grand
nombre premier et `G` est le générateur.

Alice génère une paire de clés asymétriques éphémères aléatoires   :
$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

Ces clés ne sont utilisées qu'une seule fois, et sont uniques à la transaction, ce qui nous donne un secret parfait.

### Chiffrement {#encryption}

Le processus de chiffrement comprend 2 étapes : une étape KEM pour dériver une clé de chiffrement symétrique à partir d'un secret partagé, et une étape DEM pour chiffrer les textes en clair à l'aide de la clé de chiffrement.

### Méthode d'encapsulation de clé (chiffrement) {#key-encapsulation-method-encryption}
En utilisant la clé privée asymétrique générée précédemment, nous obtenons un secret partagé, $key_{DH}$, à l'aide de la norme Diffie-Hellman. Ceci est haché avec la clé publique éphémère afin d'obtenir la clé de chiffrement.

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


où  
   est la clé publique du destinataire  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### Méthode d'encapsulation de données (chiffrement) {#data-encapsulation-method-encryption}
Pour l'efficacité du circuit, le chiffrement utilisé est un chiffrement de bloc en mode compteur où l'algorithme de chiffrement est un hachage mimc. Étant donné que les clés éphémères sont uniques à chaque transaction, il n'est pas nécessaire d'inclure un nonce. Le chiffrement du message $i^{th}$ est le suivant :

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

où  

$Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

L'expéditeur fournit ensuite au destinataire $(Q_e, \text{ciphertexts})$. Ceux-ci sont inclus dans la structure de la transaction envoyée sur la chaîne.

### Déchiffrement {#decryption}
Afin de déchiffrer, le destinataire effectue une version légèrement modifiée des étapes KEM-DEM.

### Méthode d'encapsulation de clé (déchiffrement) {#key-encapsulation-method-decryption}
En fonction de $Q_e$, le destinataire est en mesure de calculer localement la clé de chiffrement en effectuant les étapes suivantes.

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

où  
   est la clé publique éphémère  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### Méthode d'encapsulation de clé (déchiffrement) {#data-encapsulation-method-decryption}
Avec $key_{enc}$ and an array of ciphertexts, the $i_{th}$, le texte en clair peut être récupéré avec les éléments suivants :

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

où  

$Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## Dérivation et génération des différentes clés impliquées dans le chiffrement, appropriation des engagements et dépenses {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

En utilisant BIP39, générez une `mnemonic` de 12 mots et à partir de là, générez une `seed` en appelant `mnemonicToSeedSync`.
Ensuite, en suivant les normes BIP32 et BIP44, générez une `rootKey` basée sur ce `seed` et ce `path`.

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

Si `rootKey` ou `mnemonic` est compromis, alors l'adversaire peut calculer la `zkpPrivateKey` et la `nullifierKey`.
La `zkpPrivateKey` peut être utilisée pour déchiffrer les secrets d'un engagement tandis que la `nullifierKey` peut être utilisé pour dépenser l'engagement.
Par conséquent, `rootKey` et `mnemonic` doivent être stockées en toute sécurité.

Les applications qui utiliseront les `ZkpKeys` pour générer ces clés peuvent stocker la `rootKey` dans différents appareils en divisant
ceci en actions en utilisant le partage de clé secrète de Shamir.

Il est également recommandé de stocker `zkpPrivateKey` et `nullifierKey` séparément pour éviter le vol d'engagements au cas où l'une d'entre elles
serait compromise.

La figure ci-dessous montre les étapes pour dériver les différentes clés dans Nightfall
![](../imgs/key-derivation.png)
