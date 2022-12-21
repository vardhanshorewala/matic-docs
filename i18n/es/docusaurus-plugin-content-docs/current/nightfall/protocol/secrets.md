---
id: secrets
title: Distribución secreta en banda
sidebar_label: In Band Secret Distribution
description: "Una solución para cifrar los secretos y asegurar su descifrado."
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

## Descripción general {#overview}

Para garantizar que un destinatario recibe la información secreta necesaria para usar sus compromisos, el remitente
cifra los secretos (*salt*, *valor*, *tokenId*, *ercAddress*) del compromiso presentado al destinatario y
prueba, usando ZKP, que cifraron esto correctamente con la clave pública del destinatario. Se utiliza el paradigma de cifrado híbrido [**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf).

## Cifrado híbrido KEM-DEM {#kem-dem-hybrid-encryption}


### Creación de clave {#key-creation}

Utiliza la curva elíptica (aquí utilizamos la curva de Baby Jubjub) `E` sobre un campo finito `Fp` donde `p` es un gran
primo y `G`es el generador.

Alice genera una clave asimétrica temporal par   :
$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

Estas claves se utilizan solo una vez y son únicas para esta transacción, otorgándonos un secreto perfecto por delante.

### Cifrado {#encryption}

El proceso de cifrado implica 2 pasos: un paso KEM para derivar una clave de cifrado simétrica de un secreto compartido y un paso DEM para cifrar los textos sin formato utilizando la clave de cifrado.

### Método clave de encapsulamiento (cifrado) {#key-encapsulation-method-encryption}
Utilizando la clave privada asimétrica previamente generada, obtenemos un secreto compartido, $key_{DH}$, utilizando Diffie-Hellman estándar. Esto se encuentra en hash junto con la clave pública temporal para obtener la clave de cifrado.

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


donde  
   es la clave pública del destinatario  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### Método de encapsulamiento de datos (cifrado) {#data-encapsulation-method-encryption}
Para la eficiencia del circuito, el cifrado utilizado es un bloque de cifrado en modo de contador donde el algoritmo de cifrado es un hash mimc. Dado que las claves temporales son únicas para cada transacción, no hay necesidad de que se incluya un nonce. El cifrado del mensaje $i^{th}$ es el siguiente:

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

donde  

$Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

Después, el remitente proporciona al destinatario con $(Q_e, \text{ciphertexts})$. Estos se incluyen como parte de la transacción estructurada presentada en cadena.

### Descifrado {#decryption}
Para poder descifrar, el destinatario realiza una versión ligeramente modificada de los pasos KEM-DEM.

### Método de encapsulamiento de la clave (descifrado) {#key-encapsulation-method-decryption}
Dado $Q_e$, el destinatario es capaz de calcular la clave de cifrado localmente realizando los siguientes pasos.

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

donde  
   es la clave pública del destinatario  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### Método de encapsulamiento de datos (descifrado) {#data-encapsulation-method-decryption}
Con $key_{enc}$ and an array of ciphertexts, the $i_{th}$, el texto sin formato  puede ser recuperado mediante lo siguiente:

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

donde  

$Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## Derivación y generación de las diversas claves involucradas en el cifrado, propiedad de los compromisos y el gasto {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

Utiliza BIP39 para generar una palabra de 12 `mnemonic` y a partir de esto genera una `seed` llamando `mnemonicToSeedSync`.
Después, siguiendo los estándares de BIP32 y BIP44, genera una `rootKey` basada en esta `seed` y `path`.

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

Si `rootKey` o `mnemonic` se compromete, entonces el adversario puede calcular la `zkpPrivateKey` y `nullifierKey`.
La `zkpPrivateKey` puede ser utilizada para descifrar los secretos de un compromiso mientras que la `nullifierKey` puede ser utilizada para gastar el compromiso.
Por lo tanto, `rootKey` y `mnemonic` deben ser almacenados de manera muy segura.

Las aplicaciones que utilizarán la `ZkpKeys` para generar estas claves pueden almacenar la `rootKey` en diferentes dispositivos mediante la división
de estos en acciones utilizando el compartimiento secreto de Shamir.

También se recomienda almacenar `zkpPrivateKey` y `nullifierKey` por separado para evitar el robo de los compromisos en caso de que uno de estos
esté en peligro.

La figura abajo muestra los pasos para derivar las diferentes claves en Nightfall
![](../imgs/key-derivation.png)
