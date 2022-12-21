---
id: circuits
title: Circuitos y transacciones
sidebar_label: Circuits and Transactions
description: "Tipos de circuitos en Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - circuits
  - deposit
  - transfer
image: https://matic.network/banners/matic-network-16x9.png
---

Se utilizan los circuitos para definir las reglas que una transacción debe de seguir para ser considerada correcta. En términos generales existen tres tipos de circuitos, uno para cada tipo de transacción:

- [Depósito](#deposit)
- [Transferencia](#transfer)
- [Retiro](#withdraw)

Cada transacción incluye una prueba ZK siguiendo las restricciones especificadas en estos circuitos. Los usuarios construyen esta prueba utilizando una billetera,
o a través del servidor de un cliente.
Se genera una prueba solamente si todos los siguientes casos son verdaderos:

- El nuevo [compromiso](./commitments#what-are-commitments) es válido
- El [compromiso](./commitments#what-are-commitments) antiguo es válido y propiedad del remitente
- [El anulador] (./commitments#what-are-nullifiers) es válido
- La ruta/raíz del árbol de Merkle es válida
- El Ciphertext que contiene el compromiso es válido


## Depósito {#deposit}
Los depósitos convierten los tokens ERC públicamente visibles en un compromiso de token que tiene el mismo valor o Id. de token que el del token original,
y la clave pública Nightfall del propietario del compromiso previsto.

Una prueba de depósito ZK comprueba que el probador ha creado un compromiso válido$Z_A$ with a public key $pk_A$.

El circuito luego comprueba que $Z_A$ == H(@ | ɑ | $pk_A$ | σ)
La información filtrada de una transacción de depósito incluye la dirección que acuñó el nuevo compromiso y la dirección y valor del token ERC que se utilizó.

![](../imgs/deposit.png)

## Transferencia {#transfer}
Las transferencias habilitan la transmisión de hasta dos compromisos del mismo activo entre dos partes al anular los compromisos anteriores y crear hasta dos nuevos compromisos:
- Se enviará uno al receptor, que contiene el valor del importe transferido
- Se creará otro con el valor del cambio (diferencia entre la suma de los valores de los compromisos utilizados menos el valor transferido), propiedad del transmisor.

Una prueba de transferencia ZK comprueba que el probador ha anulado hasta dos compromisos antiguos que existían en el árbol de Merkle, creó uno nuevo, y cifró su información para el destinatario.

En cualquier caso, la información filtrada será que una dirección Ethereum tiene compromisos anulados
entre el grupo de compromiso propiedad del transmisor y que se han creado nuevos compromisos.
La información sobre el nuevo propietario, qué compromisos se usaron o el monto transferido permanecen privados.

El primer diagrama repasa los pasos con respecto a la anulación de un compromiso existente (o compromisos) y la adición de información a la  estructura de datos de la`transaction`.

![](../imgs/transfer_a.png)

El segundo diagrama repasa los pasos necesarios para generar y cifrar el compromiso recién creado.

![](../imgs/transfer_b.png)

## Retiro {#withdraw}
Retirar es la operación de anular un compromiso Nightfall existente y convertirlo en tokens ERC públicamente visibles con el mismo valor y la misma Id. de token que el compromiso quemado. Retirar es la operación opuesta a un depósito. Del mismo modo que las transferencias, los retiros aceptan como entrada hasta dos compromisos.

Una prueba ZK de retiro comprueba que el probador ha anulado hasta dos compromisos antiguos que existían en el MerkleTree.

La información filtrada durante el retiro incluye la dirección de la dirección que retiró el compromiso y la Id. del valor/token y la dirección del token retirado.

![](../imgs/withdraw.png)

### Período de enfriamiento {#cooling-off-period}

Los retiros requieren de un período de `COOLING OFF` de una semana para finalizar. Esto es debido a la naturaleza optimista de Nightfall, ya que se supone que un bloque nuevo es correcto hasta que un desafiante presente una prueba de fraude. Los fondos se mantienen hasta que haya pasado una semana y se pueden retirar a L1.

# Tarifas {#fees}

El proponente toma la transacción entrante y los enrolla en un bloque L2 a cambio de una tarifa. Hay dos tipos diferentes de tarifas pagadas a la propuesta dependiendo de la transacción:
- Los depósitos pagan tarifas ETH directamente en L1.
- Las transferencias y los retiros pagan las tarifas en MATIC en L2.
