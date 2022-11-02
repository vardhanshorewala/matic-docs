---
id: what-is-polygon
title: ¿Qué es Polygon?
description: "Descubre lo que es la solución de escalabilidad de Polygon."
keywords:
  - docs
  - matic
  - polygon
  - blockchain
image: https://matic.network/banners/matic-network-16x9.png
---

[Polygon](https://polygon.technology/) es una solución de escalabilidad de la capa 2 que logra la escala utilizando cadenas laterales para la computación fuera de la cadena y de una red descentralizada de validadores de prueba de participación (PoS).

Polygon se esfuerza por resolver los problemas de escalabilidad y usabilidad, sin comprometer la descentralización, y aprovecha la comunidad y el ecosistema de desarrolladores existentes. Polygon es una solución de escalamiento ​off-/sidechain para plataformas existentes, que proporciona escalabilidad y experiencia de usuario superior a DApps y a las funcionalidades de los usuarios.

Es una solución de escalamiento para las cadenas de bloques públicas. Polygon PoS es compatible con todas las herramientas existentes de Ethereum, junto con transacciones más rápidas y baratas.

## Características y aspectos destacados {#key-features-highlights}

- **Escalabilidad**: Transacciones rápidas, bajo-costo y seguras en las cadenas laterales de Polygon, con la finalidad de que se logre en la cadena principal y Ethereum, como primera base de la capa 1 compatible.
- **Alto rendimiento**: Se logró hasta 10.000 TPS en una sola cadena lateral en una red de prueba interna; se agregarán varias cadenas para la escala horizontal.
- **Experiencia del usuario**: la abstracción de los desarrolladores y UX fluida de la cadena principal a la cadena de Polygon; aplicaciones móviles nativas y SDK con soporte de WalletConnect.
- **Seguridad**: los operadores de cadena de Polygon son los propios participantes del sistema PoS.
- **Las cadenas laterales**de Polygon son de naturaleza pública (frente a las cadenas DApp individuales), sin permiso y capaces de soportar múltiples protocolos.

El sistema Polygon, de forma consciente, fue arquitecto para soportar transiciones estatales arbitrarias en las cadenas laterales de Polygon, que están habilitadas por EVM.

## Funciones de delegado y validador {#delegator-and-validator-roles}

Puedes participar en la red Polygon, como un delegado o validador. Ver:

* [Quién es un validador](/docs/maintain/polygon-basics/who-is-validator)
* [Quién es un delegado](/docs/maintain/polygon-basics/who-is-delegator)

## Arquitectura {#architecture}

Si tu objetivo es convertirte en validador, es esencial que comprendas la arquitectura de Polygon.

Para más información, consulta [la arquitectura de](/docs/maintain/validator/architecture) Polygon.

### Componentes {#components}

Para tener una comprensión granular de la arquitectura de Polygon, consulta los componentes principales:

* [Heimdall](/docs/pos/heimdall/overview)
* [Bor](/docs/pos/bor/overview)
* [Contratos](/docs/pos/contracts/stakingmanager)

#### Bases de código {#codebases}

Para tener una comprensión granular de los componentes principales, consulta los siguientes códigos de configuración:

* [Heimdall](https://github.com/maticnetwork/heimdall)
* [Bor](https://github.com/maticnetwork/bor)
* [Contratos](https://github.com/maticnetwork/contracts)

## Cómo hacer {#how-tos}

### Configuración de nodo: {#node-setup}

Básicamente, hay dos formas de ejecutar un nodo de validador en Polygon, utilizando Ansible o directamente desde los binarios. Puedes comprobar cómo hacerlo con los siguientes enlaces:

* [Ejecuta un nodo de validador con Ansible](/docs/maintain/validate/run-validator-ansible)
* [Ejecuta un nodo de validador desde Binarios](/docs/maintain/validate/run-validator-binaries)

### Operaciones de apilamiento {#staking-operations}

Consulta cómo se lleva a cabo el proceso de apuesta para los perfiles de los validadores y delegados:

* [Operaciones de apuesta de los validadores](docs/maintain/validate/validator-staking-operations)
* [Delegado](/docs/maintain/delegate/delegate)
