---
id: faq
title: Preguntas frecuentes
sidebar_label: FAQ
description: Preguntas frecuentes sobre Avail de Polygon
keywords:
  - docs
  - polygon
  - avail
  - availability
  - client
  - consensus
  - faq
image: https://matic.network/banners/matic-network-16x9.png
slug: faq
---

:::tip

Si no encuentras tu pregunta en esta página, envíala al
 **[servidor Discord de Avail de Polygon](https://discord.gg/jXbK2DDeNt)**.

:::

## ¿Qué es un cliente ligero? {#what-is-a-light-client}

Los clientes ligeros les permiten a los usuarios interactuar con una red de cadena de bloques
 sin tener que sincronizar la cadena de bloques completa, al tiempo que se mantiene
 la descentralización y la seguridad. En general, descargan los encabezados de
 la cadena de bloques, pero no los contenidos de cada bloque. Los clientes ligeros de Avail (DA),
 además, verifican que los contenidos del bloque estén disponibles, a través de la realización
 de un muestro de disponibilidad de datos: una técnica en la que se descargan pequeñas secciones aleatorias de
 un bloque.

## ¿Qué es un caso de uso común de un cliente ligero? {#what-is-a-popular-use-case-of-a-light-client}

Existen muchos casos de uso, que hoy en día dependen de un intermediario para
 mantener un nodo completo, de manera que los usuarios finales de una cadena de bloques no
 se comunican de forma directa con la cadena de bloques, sino a través de
 un intermediario. Hasta ahora, los clientes ligeros no han sido un reemplazo
 adecuado para esta arquitectura porque carecían de garantías
 de disponibilidad de datos. Avail resuelve este problema y, de esta manera, más
 aplicaciones pueden participar de forma directa en la red de cadena de bloques sin
 intermediarios. Aunque Avail no admite nodos completos, esperamos que la mayoría
 de las aplicaciones no necesiten ejecutar uno, o que tengan que ejecutar menos.

## ¿Qué es el muestreo de disponibilidad de datos? {#what-is-data-availability-sampling}

Los clientes ligeros de Avail, al igual que otros clientes ligeros, solo descargan los
 encabezados de la cadena de bloques. Sin embargo, además realizan muestreos
 de disponibilidad de datos: una técnica que toma muestras de pequeñas secciones
 de los datos del bloque de forma aleatoria y verifica que sean correctos. Cuando
 esto se combina con la codificación de borrado y con compromisos polinómicos Kate, los clientes
 de Avail son capaces de proporcionar garantías contundentes (de casi el 100 %) de
 la disponibilidad, sin depender de pruebas de fraude y con solo una pequeña
 cantidad constante de consultas.

## ¿Cómo se utiliza la codificación de borrado para aumentar las garantías de disponibilidad de datos? {#how-is-erasure-coding-used-to-increase-data-availability-guarantees}

La codificación de borrado es una técnica que codifica datos de una manera en la que
 propaga información sobre múltiples “shards”, de manera que se puede tolerar
 la pérdida de algunos shards. Es decir, la información se puede
 reconstruir a partir de los otros shards. En la cadena de bloques,
 esto significa que aumentamos de forma eficaz el tamaño de cada bloque, pero
 evitamos que un protagonista malicioso pueda ocultar alguna parte de un bloque
 hasta el tamaño redundante del shard.

Dado que un protagonista malicioso necesita ocultar una gran parte del bloque,
 a fin de intentar ocultar incluso una transacción única, eso genera que sea mucho
 más probable que el muestreo aleatorio capte las grandes “lagunas” en
 los datos. Realmente, la codificación de borrado hace que el muestreo de disponibilidad de datos
 sea una técnica mucho más contundente.

## ¿Qué son los compromisos Kate? {#what-are-kate-commitments}

Los compromisos Kate, que introdujeron Aniket Kate, Gregory M. Zaverucha y Ian Goldberg en el 2010, proporcionan una
 modalidad de comprometerse con los polinomios de una manera concisa. Recientemente, los compromisos polinómicos pasaron a primer plano,
 al ser utilizados más que nada como compromisos en construcciones sin conocimientos técnicos, tipo PLONK.

En nuestra construcción, utilizamos los compromisos Kate por los siguientes motivos:

- Nos permiten comprometernos con los valores de una manera concisa para permanecer dentro del encabezado de bloque.
- Se pueden realizar aperturas breves, lo que ayuda a que un cliente ligero verifique la disponibilidad.
- La propiedad vinculante criptográfica nos ayuda a evitar las pruebas de fraude, al hacer que sean computacionalmente inviables
 para producir compromisos erróneos.

<!-- This allows the extension of commitments be same as the commitment to extended data, which proves
correctness of commitment construction without having access to the entire data of the block. -->

En el futuro, podríamos utilizar otros esquemas de compromiso polinómico, si eso nos da mejores vínculos o garantías.

## Dado que a Avail lo utilizan múltiples aplicaciones, ¿eso significa que las cadenas tienen que descargar las transacciones de otras cadenas? {#since-avail-is-used-by-multiple-applications-does-that-mean-chains-have-to-download-transactions-from-other-chains}

No. Los encabezados de Avail contienen un índice que permite que una aplicación puntual
 determine y descargue solo las secciones de un bloque que contiene datos
 para esa aplicación. En consecuencia, no se ven afectados en gran medida por otras cadenas
 que utilizan Avail al mismo tiempo ni por los tamaños de los bloques.

La única excepción es el muestreo de disponibilidad de datos. A fin de verificar
 que esos datos estén disponibles (y debido a la naturaleza de la codificación de borrado),
 los clientes toman muestras de pequeñas partes del bloque al azar, por lo que, de esta manera, es probable
 que se incluyan secciones que contienen datos para otras aplicaciones.
