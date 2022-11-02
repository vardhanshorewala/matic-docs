---
id: polygon-architecture
title: Arquitectura PoS de Polygon
description: "Staking, Heimdall y Bor."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

La red de Polygon es una plataforma de aplicaciones de cadena de bloques que proporciona cadenas laterales híbridas de prueba de participación y habilitadas para Plasma.

En cuanto a su arquitectura, lo bueno de Polygon consiste en su diseño moderno, que cuenta con una capa de validación genérica separada de entornos de ejecución variados, como cadenas laterales EVM de gran escala y, en el futuro, tendrá otros enfoques de capa 2, como rollups de prueba de conocimiento cero.

Para habilitar el mecanismo PoS en nuestra plataforma, se despliegan un conjunto de contratos de administración de **apilamiento** en Ethereum, así como un grupo de validadores incentivados que ejecutan nodos **Heimdall** y **Bor**. Ethereum es la primera basechain compatible con Polygon, pero Polygon busca ofrecer soporte para otras basechains, que se fundamentan en sugerencias de la comunidad y el consenso, como forma de habilitar una plataforma de cadenas de bloques de capa 2 descentralizada e interoperable.

PoS de Polygon tiene una arquitectura de tres capas:

1. Contratos inteligentes de apilamiento en Ethereum
2. Heimdall (capa de prueba de participación)
3. Bor (capa de productor de bloques)

<img src={useBaseUrl("img/matic/Architecture.png")} />

### Contratos inteligentes de Polygon (en Ethereum) {#polygon-smart-contracts-on-ethereum}

Polygon mantiene una serie de contratos inteligentes en Ethereum, que gestionan lo siguiente:

- La administración de staking para la capa de prueba de participación
- La administración de delegación, que incluye las porciones de los validadores
- Puntos de verificación/instantáneas del estado de las cadenas laterales

### Heimdall (capa validadora de prueba de participación) {#heimdall-proof-of-stake-validator-layer}

**Heimdall** es el nodo validador PoS que funciona en sintonía con los contratos de apilamiento en Ethereum para habilitar el mecanismo PoS en Polygon. Lo hemos implementado a partir de la construcción por encima del motor de consenso Tendermint, con cambios en el esquema de firma y diversas estructuras de datos. Está a cargo de la validación de bloques, de la selección del comité productor de bloques, de la verificación de una representación de los bloques de las cadenas laterales a Ethereum en nuestra arquitectura y también de muchas otras responsabilidades.

La capa Heimdall gestiona la agregación de bloques que produce Bor dentro de un árbol de Merkle y publica la raíz Merkle de forma periódica en la cadena raíz. Estas publicaciones periódicas se denominan `checkpoints`. Por cada algunos bloques en Bor, un validador (en la capa Heimdall) realiza lo siguiente:

1. Valida todos los bloques desde el último punto de verificación
2. Crea un árbol de Merkle de los hashes de los bloques
3. Publica la raíz de Merkle en la cadena principal

Los puntos de verificación son importantes por dos razones:

1. Proporcionan una finalización en la cadena raíz
2. Proporcionan prueba de quemado en el retiro de activos

Un panorama general del proceso se puede explicar de la siguiente manera:

- se selecciona un subconjunto de validadores activos del grupo para que funcionen como productores de bloques para un span. La selección de cada span también tendrá el consentimiento de una posesión de al menos dos tercios. Estos productores de bloques son responsables de crear bloques y transmitirlos al resto de la red.
- Un punto de verificación incluye la raíz de todos los bloques que se crearon durante un determinado intervalo. Todos los nodos validan el mismo y le adjuntan su firma.
- Un proponente de bloques seleccionado del conjunto de validadores es responsable de recopilar todas las firmas para un punto de verificación en particular y de remitir lo mismo en la cadena principal.
- La responsabilidad de crear bloques y también de proponer puntos de verificación depende, de forma variable, de la proporción de participación de un validador dentro del grupo general.

### Bor (capa del productor de bloques) {#bor-block-producer-layer}

Bor es la capa del productor de bloques Polygon: la entidad responsable de agregar transacciones a los bloques.

Los productores de bloques rotan de forma periódica a través de la selección de un comité en Heimdall en plazos que se denominan `span` en Polygon. Los bloques se producen en el nodo **Bor** y la cadena lateral VM es compatible con EVM. Los bloques que se producen en Bor también se validan de forma periódica por nodos Heimdall y se asigna a Ethereum de forma periódica. un punto de verificación que consiste en el hash del árbol de Merkle de un conjunto de bloques en Bor.

### **dirigirse:recursos**

clip de papel: [arquitectura Bor](https://forum.polygon.technology/t/matic-system-overview-bor/9123) <br/>
 :clip de papel: [arquitectura Heimdall](https://forum.polygon.technology/t/matic-system-overview-heimdall/8323) <br/>
 :clip de papel: [mecanismo de punto de verificación](https://forum.polygon.technology/t/checkpoint-mechanism-on-heimdall/7160)
