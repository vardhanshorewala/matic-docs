---
id: secrets
title: Distribución Secreta en Banda
sidebar_label: In Band Secret Distribution
description: "Una solución para encriptar secretos y asegurar su descripción."
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

## Resumen {#overview}

Para garantizar que un destinatario recibe la información secreta necesaria para gastar sus compromisos, el remitente
encripta los secretos (*sal*, *valor*, *Id de token*, *ercAddress*) del compromiso enviado al destinatario y
demuestra el uso de ZKP que ellos encriptaron esto correctamente con la clave pública del destinatario. La [**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf) se utiliza el paradigma de encriptado híbrido.

## Encriptado híbrido de KEM-DEM {#kem-dem-hybrid-encryption}


### Creación de Clave {#key-creation}

Usa la curva elíptica (aquí usamos la curva Baby Jubjub)`E` sobre un campo finito `Fp`donde`p` es una gran
prima y `G` es el generador.

Alice genera un par de claves asimétricas efímeras   :
$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

Estas claves se utilizan solo una vez, y son exclusivas para esta transacción, lo que nos brinda un secreto de avance perfecto.

### Encriptado {#encryption}

El proceso de encriptación implica 2 pasos: un paso de KEM para obtener una clave de encriptación simétrica de un secreto compartido, y un paso de DEM para encriptar los textos sin formato usando la clave de encriptado.

### Método Clave de Encapsulado (Encriptado) {#key-encapsulation-method-encryption}
Usando la clave privada asimétrica generada previamente, obtenemos un secreto compartido, $key_{DH}$ usando el estándar Diffie-Hellman. Esto se hashea junto con la efímera clave pública para obtener la clave de encriptado.

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


donde  
   es la clave pública del destinatario  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### Método de Encapsulado de Datos (Encriptado) {#data-encapsulation-method-encryption}
Para la eficiencia de circuitos, la encriptación que se usa es un bloque cifrado en modo de contador donde el algoritmo de cifrado es un hash de mimc. Dado que las claves efímeras son exclusivas para cada transacción, no hay necesidad de un mientras tanto para ser incluidos. El encriptado del mensaje $i^{th}$ es como sigue:

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

Donde  

$Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

El remitente entonces proporciona al destinatario con $(Q_e, \text{ciphertexts})$. Estos son incluidos como parte de la transacción que se envía en cadena.

### Desencriptado {#decryption}
Con el fin de desencriptar, el destinatario realiza una versión ligeramente modificada de los pasos de KEM-DEM.

### Método Clave de Encapsulado (Desencriptado) {#key-encapsulation-method-decryption}
Dado $Q_e$, el destinatario puede calcular la clave de cifrado localmente realizando los siguientes pasos.

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

donde  
   es la clave pública efímera  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### Método de Encapsulado de Datos (Desencriptado) {#data-encapsulation-method-decryption}
Con el texto sin formato $key_{enc}$ and an array of ciphertexts, the $i_{th}$ se puede recuperar con lo siguiente:

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

Donde  

$Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## La derivación y la generación de las diversas claves involucradas en el encriptado, la propiedad de los compromisos y el gasto {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

Usando BIP39 generar una `mnemonic` de 12 palabras y desde esta generar un `seed` llamando `mnemonicToSeedSync`.
Luego, siguiendo los estándares de BIP32 y BIP44, genere un `rootKey` basado en esto`seed` y `path`.

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

Si se `rootKey` o `mnemonic` está comprometida, entonces el adversario puede calcular él `zkpPrivateKey` y `nullifierKey`.
Él `zkpPrivateKey` se puede usar para descifrar los secretos de un compromiso, mientras que `nullifierKey` se puede usar para gastar el compromiso.
Por lo tanto `rootKey` y `mnemonic` deben almacenarse de forma muy segura.

Las aplicaciones que usarán él `ZkpKeys` para generar estas claves pueden almacenar él `rootKey` en diferentes dispositivos dividiendo
esto en acciones usando Compartir el Secreto de Shamir.

También se recomienda almacenar `zkpPrivateKey` y `nullifierKey` por separado para evitar el robo de compromisos en caso de que uno de estos
esté comprometido.

La siguiente figura muestra los pasos para derivar las diferentes claves en Nightfall
![](../imgs/key-derivation.png)
