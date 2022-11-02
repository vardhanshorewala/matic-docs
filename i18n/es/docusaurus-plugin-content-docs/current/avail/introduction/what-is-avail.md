---
id: what-is-avail
title: Avail por Polygon
sidebar_label: Introduction to Avail
description: Obtén información sobre la cadena de disponibilidad de datos de Polygon.
keywords:
  - docs
  - polygon
  - avail
  - availability
  - scale
  - rollup
image: https://matic.network/banners/matic-network-16x9.png
slug: what-is-avail
---

<!-- Page is WIP -->

import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import useBaseUrl from '@docusaurus/useBaseUrl';

Avail es una cadena de bloques que está enfocada en el láser en la disponibilidad de datos: ordenar y registrar transacciones de la cadena de bloques y haciéndolo posible para probar que los datos de bloque están disponibles sin descargar todo el bloque. Esto le permite escalar de maneras que las cadenas de bloques monolíticas no pueden.

:::note Una sólida capa de disponibilidad de datos escalables de propósito general

* Permite que las soluciones de Layer-2 ofrezcan un mayor rendimiento de escalabilidad al aprovechar Avail para construir Validiums con datos fuera de la cadena de disponibilidad.

* Permite las cadenas independientes o a las cadenas laterales con ejecución arbitraria de entornos para la seguridad del validador de arranque sin la necesidad de crear y administrar su propio conjunto de validadores garantizando Disponibilidad de datos de la transacción.

:::

## Disponibilidad actual y desafíos de escalado {#current-availability-and-scaling-challenges}

<TabItem value="da"><Tabs
defaultValue="da"
values={[
{ label: 'Data Availability', value: 'da', },
{ label: 'Rollup Scaling', value: 'scaling', },
]
}>


### ¿Cuál es el problema de disponibilidad de datos? {#what-is-the-data-availability-problem}

Los pares en una red de cadena de bloques necesitan una manera de garantizar que todos los datos de un bloque recientemente propuesto son fácilmente disponible. Si no están disponibles los datos, el bloque podría contener transacciones maliciosas las que están siendo ocultas por el productor de bloques. Incluso si el bloque contiene transacciones no maliciosas, ocultas podrían comprometer la seguridad del sistema.

### El enfoque de Avail para la disponibilidad de datos {#avail-s-approach-to-data-availability}

#### Alta garantía {#high-guarantee}

Avail proporciona una garantía comprobable, de alto nivel de que los datos están disponibles. Los clientes ligeros pueden verificar de forma independiente la disponibilidad en un número constante de consultas, sin descargar todo el bloque.

#### Confianza Mínima {#minimum-trust}

No es necesario ser validador o alojar un nodo completo. Incluso con un cliente ligero, obtén la disponibilidad verificable.

#### Fácil de usar {#easy-to-use}

Construida utilizando el Substrato modificado, la solución se enfoca en la facilidad de uso, ya sea que aloje una aplicación o que opere una solución de escalado fuera de la cadena

#### Perfecto para el escalamiento fuera de la cadena {#perfect-for-off-chain-scaling}

Desbloquea el potencial de escalamiento completo de tu solución de escalamiento fuera de la cadena manteniendo los datos con nosotros y aun evitando el problema de DA en L1.

#### El agnóstico de ejecución {#execution-agnostic}

Que las cadenas que utilizan Avail pueden implementar cualquier tipo de entorno de ejecución independientemente de la lógica de la aplicación. Transacciones desde cualquier Se admiten los entornos: EVM, Wasm, o incluso nuevas máquinas virtuales que aún no se han construido. todavía Avail es perfecto para experimentar con unas nuevas capas de ejecución n/a

#### Seguridad de Arranques {#bootstrapping-security}

Avail permite crear nuevas cadenas sin necesidad de girar en un nuevo conjunto de validadores, y aprovecha Avail en su lugar. Avail se encarga de la secuenciación de transacciones, consenso y disponibilidad a cambio de honorarios de transacciones simples (gas).

#### Finalidad rápida y demostrable utilizando NPoS {#fast-provable-finality-using-npos}

Finalidad rápida y demostrable a través de prueba nominada de participación. Respaldada por KZG codificación de compromisos y borrado.

</TabItem>
<TabItem value="scaling">

Comienza por mirar esta [publicación](https://blog.polygon.technology/polygon-research-ethereum-scaling-with-rollups-8a2c221bf644/) de blog sobre el escalamiento Ethereum con Rollups.

## Validiums Alimentados por Avail {#avail-powered-validiums}

Debido a la arquitectura de las cadenas monolíticas de bloques (tales como Ethereum en su estado actual), operando la cadena de bloques es caro, resultando en altas tarifas de transacción. Los rollups intentan extraer la carga de ejecución corriendo las transacciones fuera de la cadena y luego publicando los resultados de ejecución y los datos [de] la transacción generalmente comprimidos.

Los validiums son el siguiente paso: en lugar de publicar los datos de la transacción, que se mantiene disponible fuera de la cadena, donde una prueba / certificación es solo publicada en la capa base. Esta es, con mucho, la solución más rentable porque tanto la ejecución como la disponibilidad de datos se mantienen fuera de la cadena mientras que todavía está permitiendo la verificación y liquidación final en la cadena de la capa 1.

Avail es una cadena de bloques optimizada para la disponibilidad de datos. Cualquier rollup que desee convertirse en validium puede cambiar para publicar datos de la transacción a Avail en lugar de la capa 1 y desplegando un contrato de verificación que, además de verificar la ejecución correcta, también verifica los datos de disponibilidad.

:::note Acreditación

El equipo de Avail hará que esta verificación de disponibilidad de datos sea simple en Ethereum mediante la construcción de un puente de certificación para publicar la disponibilidad de los datos las certificaciones directamente en Ethereum. Esto hará que la verificación de contratos de trabajo sea simple, ya que las certificaciones de DA ya serán en cadena. Este puente está actualmente en diseño; por favor contacta con El equipo Avail para obtener más información o para unirte a nuestro programa de acceso temprano.

:::

</TabItem>
</Tabs>

## Ver también {#see-also}

* [Presentamos Avail por Polygon — una capa de disponibilidad de datos escalable de uso general robusto](https://polygontech.medium.com/introducing-avail-by-polygon-a-robust-general-purpose-scalable-data-availability-layer-98bc9814c048)
* [El problema de disponibilidad de datos](https://blog.polygon.technology/the-data-availability-problem-6b74b619ffcc/)
