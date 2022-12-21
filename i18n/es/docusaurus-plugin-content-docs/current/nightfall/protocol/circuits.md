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

Los circuitos se utilizan para definir las reglas que una transacción debe seguir para que se considere correcta. Hay en general tres tipos de circuitos, uno para cada tipo de transacción:

- [Depósitos](#deposit)
- [Transferencias](#transfer)
- [Retiros](#withdraw)

Cada transacción incluye una prueba de ZK que sigue las restricciones especificadas en estos circuitos. Los usuarios construyen esta prueba usando una billetera
o a través de un servidor de cliente.
Una prueba se genera solo si todos los siguientes casos son verdaderos:

- Nuevo [compromiso](./commitments#what-are-commitments) es válido
- El viejo [compromiso](./commitments#what-are-commitments) es válido y propiedad del emisor
- [Nulificador] (./commitments#what-are-nullifiers) es válido
- La ruta / raíz del árbol de Merkle es válida
- Ciphertext que contiene el compromiso es válido


## Depósitos {#deposit}
Los depósitos convierten los tokens ERC públicamente visibles en tokens de compromiso que contienen el mismo valor e identificación de token que el de los tokens originales,
y la clave pública de Nightfall del propietario de un compromiso previsto.

Una prueba ZK de depósito prueba que el probador ha creado un compromiso válido$Z_A$ with a public key $pk_A$.

Después el circuito verifica que $Z_A$ == H(@ | ɑ | $pk_A$ | σ)
Información filtrada de un depósito de transacción incluyen la dirección que acuñó el nuevo compromiso y la dirección y valor del token del ERC que se utiliza.

![](../imgs/deposit.png)

## Transferencias {#transfer}
Las transferencias habilitan la transmisión de dos compromisos del mismo activo entre dos partes al nulificar los anteriores compromisos y crear nuevos compromisos de los dos:
- Uno se enviará al receptor, que contiene el valor del monto transferido
- Otro se creará con el valor de cambio (diferencia entre la suma de valores de los compromisos usados menos el valor transferido) y del transmisor propietario.

Una prueba de transferencia de ZK confirma que el proveedor ha nulificado hasta dos viejos compromisos que existían en el Merkle Tree, creando unos nuevos, y encriptando su información para el destinatario.

En cualquiera de los casos, la información filtrada será que una dirección de Ethereum tiene compromisos nulificados
entre el grupo de compromiso que es propiedad del transmisor y que se han creado nuevos compromisos.
Información sobre el nuevo propietario, de que se gastaron los compromisos o la cantidad transferida sigue siendo privada.

El primer diagrama va sobre los pasos alrededor de nulificar un compromiso existente (o compromisos) y agrega la información a la estructura de datos `transaction`.

![](../imgs/transfer_a.png)

El segundo diagrama va sobre los pasos necesarios para generar y encriptar el nuevo compromiso.

![](../imgs/transfer_b.png)

## Retiros {#withdraw}
Retirar es la operación de nulificar un compromiso existente de Nightfall y convertirlo en tokens ERC públicamente visibles con el mismo valor e identificación de token que el compromiso de quemarlo. Retirar es la operación opuesta a depositar. Del mismo modo que las transferencias, los retiros aceptan como entrada hasta dos compromisos.

Un retiro de prueba de ZK comprueba que el probador ha nulificado hasta dos viejos compromisos que existían en el MerkleTree.

La información filtrada durante un retiro incluye la dirección de la dirección que retiró el compromiso y el valor / de identificación del token y la dirección del token retirado.

![](../imgs/withdraw.png)

### Periodo de enfriamiento {#cooling-off-period}

Los retiros requieren un periodo `COOLING OFF` de una semana para finalizar. Esto es debido a la naturaleza optimista de Nightfall, ya que se supone que un bloque nuevo es correcto hasta que un retador envía una prueba de fraude. Los fondos se mantienen hasta que haya pasado una semana y ellos se puedan retirar a L1.

# Tarifas {#fees}

El proponente toma la transacción entrante y la convierte en un bloque L2 a cambio de una tarifa. Hay dos tipos diferentes de tarifas pagadas para la proposición dependiendo de la transacción:
- Los depósitos pagan tarifas ETH directamente en L1.
- Las transferencias y retiros pagan tarifas en MATIC en L2.
