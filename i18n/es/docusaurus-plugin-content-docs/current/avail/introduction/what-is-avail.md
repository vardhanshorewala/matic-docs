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

Avail es una cadena de bloques que está enfocada en el láser en la disponibilidad de datos:
 ordenar y registrar transacciones de la cadena de bloques y haciéndolo posible
 para probar que los datos de bloque están disponibles sin descargar todo el
 bloque. Esto le permite escalar de maneras que las cadenas de bloques monolíticas
 no pueden.

:::note Una sólida capa de disponibilidad de datos escalables de propósito general

* Permite que las soluciones de Layer-2 ofrezcan un mayor rendimiento de escalabilidad
 al aprovechar Avail para construir Validiums con disponibilidad de datos
 disponibilidad de los datos.

* Permite las cadenas independientes o a las cadenas laterales con ejecución arbitraria
 entornos de ejecución arbitrarios arrancar la seguridad de los validadores sin necesidad de
 crear y administrar su propio conjunto de validadores garantizando
 la disponibilidad de los datos de las transacciones.

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

Los pares de una red de cadena de bloques necesitan una forma de garantizar que todos los datos de un bloque recién propuesto
 estén disponibles. Si los datos no están disponibles, el bloque podría contener transacciones maliciosas
 que están siendo ocultadas por el productor de bloques. Incluso si el bloque contiene transacciones no maliciosas,
 ocultarlas podría comprometer la seguridad del sistema.

### El enfoque de Avail para la disponibilidad de datos {#avail-s-approach-to-data-availability}

#### Alta garantía {#high-guarantee}

Avail proporciona un alto nivel de garantía demostrable de que los datos están
 disponibles. Los clientes ligeros pueden verificar independientemente la disponibilidad en un
 número constante de consultas, sin necesidad de descargar el bloque completo.

#### Confianza Mínima {#minimum-trust}

No es necesario ser validador o alojar un nodo completo. Incluso con un cliente ligero, obtén la disponibilidad verificable.

#### Fácil de usar {#easy-to-use}

Construida con Substrate modificado, la solución se centra en la facilidad de uso, tanto si aloja una aplicación
 como si opera una solución de escalabilidad fuera de la cadena.

#### Perfecto para el escalamiento fuera de la cadena {#perfect-for-off-chain-scaling}

Desbloquea el potencial de escalamiento completo de tu solución de escalamiento fuera de la cadena manteniendo los datos con nosotros y
 aun evitando el problema de DA en L1.

#### Ejecución agnóstica {#execution-agnostic}

Las cadenas que utilizan Avail pueden implementar cualquier tipo de entorno de ejecución
 independientemente de la lógica de la aplicación. Se admiten transacciones de cualquier
 entorno: EVM, Wasm, o incluso nuevas VMs que aún no
 han sido construidas. Avail es perfecto para experimentar con unas nuevas capas de
 ejecución.

#### Seguridad en el arranque {#bootstrapping-security}

Avail permite crear nuevas cadenas sin necesidad de crear un nuevo conjunto
 de validadores, y aprovechar los de Avail en su lugar. Avail se encarga de la
 secuenciación de las transacciones, el consenso y la disponibilidad a cambio de unas
 simples tasas de transacción (gas).

#### Finalidad rápida y demostrable utilizando NPoS {#fast-provable-finality-using-npos}

Finalidad rápida y demostrable a través de prueba de participación nominada. Respaldado por compromisos KZG
 y codificación de borrado.

</TabItem>
<TabItem value="scaling">

Comienza por mirar esta [publicación de blog](https://blog.polygon.technology/polygon-research-ethereum-scaling-with-rollups-8a2c221bf644/) sobre el escalamiento
 Ethereum con Rollups.

## Validiums impulsados por Avail {#avail-powered-validiums}

Debido a la arquitectura de las cadenas de bloques monolíticas
 (como Ethereum en su estado actual), el funcionamiento de la cadena de bloques es
 costoso, lo que da lugar a elevadas tasas de transacción. Los rollups intentan extraer
 la carga de la ejecución ejecutando las transacciones fuera de la cadena y luego publicando
 los resultados de la ejecución y los datos de la transacción [normalmente comprimidos].

Los validiums son el siguiente paso: en lugar de publicar los datos
  de la transacción, se mantienen disponibles fuera de la cadena, donde una prueba/certificación solo se
 publica en la capa base. Esta es, con mucho, la solución
 más rentable, ya que tanto la ejecución como la disponibilidad de los datos se mantienen fuera de la cadena, al tiempo que se
 permite la verificación final y la liquidación en la cadena de capa 1.

Avail es una cadena de bloques optimizada para la disponibilidad de datos. Cualquier rollup que
 desee convertirse en un validium puede pasar a publicar los datos de las transacciones en
 Avail en lugar de en la capa 1 y desplegar un contrato de verificación que,
 además de verificar la correcta ejecución, también verifique la
 disponibilidad de los datos.

:::note Certificación

El equipo de Avail simplificará la verificación de la disponibilidad de los datos en
 Ethereum construyendo un puente de certificación para publicar los certificados de disponibilidad de los datos
 directamente en Ethereum. Esto hará que la verificación
 de contratos de trabajo sea simple, ya que las certificaciones de DA ya serán
 en cadena. Este puente está actualmente en diseño; por favor contacta con
 el equipo Avail para obtener más información o para unirte a nuestro programa de acceso temprano.

:::

</TabItem>
</Tabs>

## Ver también {#see-also}

* [Presentamos Avail por Polygon — una robusta capa de disponibilidad de datos escalable de propósito general](https://polygontech.medium.com/introducing-avail-by-polygon-a-robust-general-purpose-scalable-data-availability-layer-98bc9814c048)
* [El problema de la disponibilidad de datos](https://blog.polygon.technology/the-data-availability-problem-6b74b619ffcc/)
