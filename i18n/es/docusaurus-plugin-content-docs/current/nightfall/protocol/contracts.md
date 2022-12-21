---
id: contracts
title: Contratos inteligentes
sidebar_label: Smart Contracts
description: "Escudo, proponentes, desafíos y cálculos de árboles de Merkle."
keywords:
  - docs
  - polygon
  - nightfall
  - smart
  - contracts
  - shield
image: https://matic.network/banners/matic-network-16x9.png
---

Los contratos definen las reglas que cada actor de Nightfall necesita seguir para operar en la red.
Los contratos inteligentes incluyen:

- [Shield.sol](#shield)
- [Proposers.sol](#proposers)
- [Challenges.sol](#challenges)
- [MerkleTree_Computations.sol](#merkletree_computations)

## Escudo {#shield}
Este contrato permite a un usuario enviar una transacción para su procesamiento por un proponente. Si se trata de una transacción de depósito, tomará el pago.
También permite a cualquiera solicitar que el estado del contrato de Escudo (listas de compromiso raíz y anuladores) se actualice. Cuando se actualiza el estado, cualquier retiro en la actualización se procesará.

No hay una necesidad fundamental de publicar una transacción de transferencia o retiro a la cadena de bloques: simplemente actúa como un tablero de mensajes para
que los proponentes recojan las transacciones y las incorporen en un bloque de capa 2.

Dado que Nightfall interactúa con contratos ERC reales, las siguientes verificaciones no se pueden hacer privadas:

- Durante el **depósito / retiro**, la dirección del token ERC es válida.
- Durante el **depósito**, el usuario tiene saldo o posee token para crear el compromiso.

## Proponentes {#proposers}
El contrato incluye la funcionalidad para registrar, anular el registro, pagar y rotar proponentes, y proponer un nuevo bloque de capa 2 a la cadena de bloques.
La primera versión de Nightfall solo acepta un único proponente boot operado por Polygon. En las versiones siguientes, esta restricción se levantará y varios proponentes serán permitidos.

## Desafíos {#challenges}
La funcionalidad permite que se desafíe un bloque como incorrecto.

## MerkleTree_Stateless {#merkletree_stateless}
Una versión de la `MerkleTree.sol` original sin estado (pura función), utilizada por `Challenges.sol` para ayudar a calcular desafíos en bloque de cadena.

## Otros contratos {#other-contracts}
- `Utils.sol`- reúne la funcionalidad que se utiliza ya sea en múltiples contratos o que, si se deja en línea, afectaría la legibilidad del código.
- `Config.sol`- mantiene constantes, similares a un archivo config Node.js.
- `Structures.sol`- define las estructuras globales, los enums, los eventos, los mappings y las variables de estado. Hace que estos sean más fáciles de encontrar.

## Actualización {#upgradability}
Al menos al principio, Polygon conserva la capacidad de actualizar los contratos de Nighfall tras su despliegue.
Utilizamos [los plugins de las actualizaciones](https://docs.openzeppelin.com/upgrades-plugins/1.x/) de Openzeppelin para Truffle para hacerlo.

Polygon utiliza un módulo de [despliegue](https://github.com/EYBlockchain/nightfall_3/tree/master/nightfall-deployer) para actualizar los contratos.
El `deployer` tiene 4 migraciones almacenadas en su carpeta de migración.
Las primeras tres migraciones realizan un despliegue 'normal' del paquete de contratos de Nightfall Polygon. Sin embargo,
ellos se aseguran de que todos los contratos (pero no las bibliotecas) se desplieguen con un proxy para permitirles que
se actualicen en una fecha posterior. La cuarta migración se utiliza para actualizar los contratos.
