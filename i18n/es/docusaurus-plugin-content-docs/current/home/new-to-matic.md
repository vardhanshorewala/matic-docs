---
id: new-to-polygon
title: ¿Eres nuevo en Polygon?
description: Desarrolla tu próxima app de cadena de bloques en Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
Polygon es una solución de escalabilidad para cadenas de bloques públicas. PoS de Polygon es compatible con todas las herramientas existentes de Ethereum, junto con transacciones más rápidas y baratas.

## Tipos de interacción en Polygon {#types-of-interaction-on-polygon}

* [Cadena PoS de Polygon](/docs/develop/getting-started)
* [Ethereum y Polygon con puente de PoS](https://docs.polygon.technology/docs/develop/ethereum-polygon/pos/getting-started)
* [Ethereum y Polygon con puente de Plasma](https://docs.polygon.technology/docs/develop/ethereum-polygon/plasma/getting-started)

## Desplegar contratos inteligentes {#deploy-smart-contracts}

<!-- ### Are you an Experience Blockchain Developer? -->

* Desplegar tus contratos en Polygon
    - [Cómo utilizar Alchemy](/docs/develop/alchemy)
    - [Cómo utilizar Chainstack](/docs/develop/chainstack)
    - [Cómo utilizar QuickNode](/docs/develop/quicknode)
    - [Cómo utilizar Remix](/docs/develop/remix)
    - [Cómo utilizar Truffle](/docs/develop/truffle)
    - [Cómo utilizar Hardhat](/docs/develop/hardhat)
* Configura la RPC-URL de web3 en https://rpc-mumbai.matic.today, *todo lo demás permanece igual*

## ¿Qué es una cadena de bloques? {#what-is-a-blockchain}
En términos simples, la cadena de bloques es un libro contable compartido e inalterable para registrar transacciones, hacer seguimiento de activos y establecer confianza. Dirígete a [Conceptos básicos sobre cadena de bloques](blockchain-basics/basics-blockchain.md) para leer más.

:movie_camera: [Tu primera aplicación descentralizada](https://www.youtube.com/watch?v=rzvk2kdjr2I)

## ¿Qué es una cadena lateral? {#what-is-a-sidechain}
Piensa en una cadena lateral como un clon de una cadena de bloques “principal”, que permite transferir activos hacia y desde la cadena principal. Es simplemente una alternativa a la cadena principal, que crea una nueva cadena de bloques con su propio mecanismo de creación de bloques (mecanismo de consenso). La conexión de una cadena lateral a una cadena principal implica configurar un método de trasladar activos entre las cadenas.

:page_facing_up: [Cadenas laterales y cadenas secundarias](https://hackernoon.com/what-are-sidechains-and-childchains-7202cc9e5994)

## Funciones de delegador y validador {#validator-and-delegator-roles}

En la red de Polygon, puedes ser un validador o un delegador. Consulta lo siguiente:

* [Quién es validador](/docs/maintain/polygon-basics/who-is-validator)
* [Quién es delegador](/docs/maintain/polygon-basics/who-is-delegator)

## Arquitectura {#architecture}

Si tu objetivo es convertirte en validador, es fundamental que comprendas la arquitectura de Polygon.

Consulta [Arquitectura de Polygon](/docs/maintain/validator/architecture).

### Componentes {#components}

Para tener una comprensión al detalle de la arquitectura de Polygon, consulta los componentes principales:

* [Heimdall](/docs/pos/heimdall/overview)
* [Bor](/docs/pos/bor/overview)
* [Contratos](/docs/pos/contracts/stakingmanager)

#### Bases de código {#codebases}

Para tener una comprensión al detalle de los componentes principales, consulta las bases de código:

* [Heimdall](https://github.com/maticnetwork/heimdall)
* [Bor](https://github.com/maticnetwork/bor)
* [Contratos](https://github.com/maticnetwork/contracts)

## Instructivos {#how-tos}

### Configuración de nodo {#node-setup}

* [Ejecuta un nodo validador con Ansible](/docs/maintain/validate/run-validator-ansible)
* [Ejecuta un nodo validador desde Binaries](/docs/maintain/validate/run-validator-binaries)

### Operaciones de Staking {#staking-operations}

* [Operaciones de staking de los validadores](/docs/maintain/validate/validator-staking-operations)
* [Delegar](/docs/maintain/delegate/delegate)
