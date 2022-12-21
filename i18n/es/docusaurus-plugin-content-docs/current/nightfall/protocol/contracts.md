---
id: contracts
title: Contratos inteligentes
sidebar_label: Smart Contracts
description: "Escudo, proponentes, desafíos y cálculos del árbol de Merkle."
keywords:
  - docs
  - polygon
  - nightfall
  - smart
  - contracts
  - shield
image: https://matic.network/banners/matic-network-16x9.png
---

Los contratos definen las reglas que cada actor en Nightfall necesita seguir para operar en la red.
Los contratos inteligentes incluyen:

- [Shield.sol](#shield)
- [Proposers.sol](#proposers)
- [Challenges.sol](#challenges)
- [MerkleTree_Computations.sol](#merkletree_computations)

## Escudo {#shield}
Este contrato permite al usuario enviar una transacción para el procesamiento de un proponente. Si se trata de depositar una transacción, tomará el pago.
También permite que cualquiera pueda solicitar que se actualice la declaración del contrato Escudo (compromiso raíz y listas de nulificadores).
Cuando la declaración se actualice, cualquier retiro en la actualización se procesará.

No hay necesidad fundamental de publicar una transacción de transferencia o retiro a la cadena de bloques: esta simplemente actúa como un tablero de mensajes para que
los proponentes os proponentes recojan la transacción y la incorporen a un bloque de capa 2.

Desde que Nightfall interactúa con contratos reales de ERC, las siguientes verificaciones no se pueden hacer privadas:

- Durante **Depósito/Retiro**, la dirección del token ERC es válida.
- Durante **Depósito**, el usuario tiene saldo o posee tokens para crear compromiso.

## Proponentes {#proposers}
El contrato incluye funcionalidad para registrar, cancelar el registro, pagar y rotar proponentes, y proponer una nueva capa de bloque 2 a la cadena de bloques.
La primera versión de Nightfall solo acepta un único proponente operado por Polygon. En las próximas versiones, esta restricción se levantará, donde se permitirán múltiples proponentes.

## Desafíos {#challenges}
La funcionalidad permite un bloque para ser desafiado como incorrecto.

## MerkleTree_Stateless {#merkletree_stateless}
Una versión sin declaración (función pura) del original `MerkleTree.sol` utilizada por `Challenges.sol` para ayudar a calcular desafíos de bloques en cadena.

## Otros contratos {#other-contracts}
- `Utils.sol`: reúne la funcionalidad que se usa en múltiples contratos o que, si se deja en línea, afectaría la legibilidad del código.
- `Config.sol`: contiene constantes, similares a un archivo de configuración de Node.js.
- `Structures.sol`: define estructuras globales, enumeraciones, eventos, asignaciones y variables de declaración. Esto hace que sea más fácil de encontrar.

## Actualización {#upgradability}
Al menos al principio, Polygon mantiene la capacidad de actualizar los contratos de Nightfall después de la implementación.
Usamos Openzeppelin [Actualiza complementos](https://docs.openzeppelin.com/upgrades-plugins/1.x/) para Truffle para hacer eso.

Polygon utiliza un módulo [desplegar](https://github.com/EYBlockchain/nightfall_3/tree/master/nightfall-deployer) para actualizar contratos.
Él `deployer` tiene 4 migraciones almacenadas en su carpeta de migración.
Las primeras tres migraciones realizan un despliegue "normal" del contrato suite de Polygon Nightfall. Sin embargo
se aseguran de que todos los contratos (pero no las bibliotecas) se desplieguen con un proxy para poder
para poder actualizarlos posteriormente. La cuarta migración se utiliza para actualizar contratos.
