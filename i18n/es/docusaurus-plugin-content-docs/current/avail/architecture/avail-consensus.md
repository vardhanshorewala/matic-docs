---
id: avail-consensus
title: Consenso de Avail
sidebar_label: Consensus
description: Obtén información sobre el mecanismo de consenso de Avail
keywords:
  - docs
  - polygon
  - avail
  - consensus
  - proof of stake
  - nominated proof of stake
  - pos
  - npos
image: https://matic.network/banners/matic-network-16x9.png
slug: avail-consensus
---

## Comités de disponibilidad de datos {#data-availability-committees}

Hasta ahora, el enfoque para mantener las soluciones de disponibilidad de datos, en general, ha sido a través
 de un DAC (comité de disponibilidad de datos, según sus siglas en inglés). Un DAC es el responsable de volver a publicar
 las firmas en la cadena principal y de certificar la disponibilidad fuera de la cadena
 de datos. El DAC debe asegurar que los datos estén disponibles de inmediato.

A través de un DAC, las soluciones de escalamiento se basan en un DAC para alcanzar un Validium. El problema
 con los DAC es que la disponibilidad de datos se convierte en un servicio de confianza que depende de un pequeño grupo
 de los miembros del comité, que son los responsables de almacenar y notificar los datos con veracidad.

Avail no es un DAC, pero sí una red de cadena de bloques real con su mecanismo
 de consenso y que tiene su propio conjunto de nodos validadores y productores de bloques.

## Prueba de participación {#proof-of-stake}

:::caution Validadores actuales

Con el lanzamiento inicial de la red de prueba Avail, Polygon
 operará y mantendrá de manera interna los validadores.

:::

Los sistemas de prueba de participación tradicionales requieren que los autores de producción de bloques cuenten con
 tenencias de tokens (stake) en la cadena para producir bloques, a diferencia de los recursos
 computacionales (trabajo).

Los productos de Polygon utilizan la PoS (prueba de participación) o una modificación de la PoS.

En general, los validadores de los sistemas PoS tradicionales que cuentan con el mayor stake
 son los que tienen más influencia y control de la red. Los sistemas con muchos mantenedores de red
 tienden a formar pools fuera de la cadena para maximizar las ganancias de capital, mediante la reducción de la diferencia de recompensa. Este
 problema de centralización se vuelve menos desafiante cuando los pools están incluidos en la cadena, lo que permite que los poseedores
 de tokens respalden a los mantenedores de la red que sientan que mejor los representan tanto a ellos como a los intereses
 de la red. Esto también hace que se distribuya la concentración de poder del validador, si se da como válido que
 existen mecanismos de votación y de elección correctos, ya que la stake general de la red
 se asigna como una relación de uno a muchos o de muchos a muchos, en lugar de solo depender de
 una relación uno a uno, en la que la confianza se pone en los validadores que cuentan con “mayor participación” (un stake más alto). Esta
 modificación de la prueba de participación se puede administrar a través de la delegación o de la nominación,
 a la que comúnmente se la conoce como DPoS (prueba de participación delegada) o NPoS (prueba de participación nominada).
 Las soluciones de escalamiento de Polygon han adaptado estos mecanismos mejorados, gracias a la inclusión de
 Avail de Polygon.

Avail utiliza NPoS con una modificación en la verificación de bloques. Los protagonistas involucrados siguen
 siendo validadores y nominadores.

Los clientes ligeros también pueden contribuir a la disponibilidad de datos en Avail. El consenso de Avail
 requiere que dos tercios más 1 de los validadores logren consenso para que sea válido.

## Nominadores {#nominators}

Los nominadores pueden optar por respaldar un conjunto de candidatos a validadores de Avail con su
 stake. Los nominadores nominarán aquellos validadores que crean
 que proporcionarán la disponibilidad de datos de forma efectiva.

:::info ¿Cuál es la diferencia entre DPoS y NPoS

Si se tiene en cuenta el valor nominal, delegar y nominar parecen ser la misma acción, en especial,
 desde el punto de vista de un staker aficionado. Sin embargo, las diferencias subyacen en los
 mecanismos de consenso y en cómo se produce la selección de los validadores.

En la DPoS, un sistema de elección centrado en la votación determina la cantidad fija de
 validadores para asegurar la red. Los delegadores pueden delegar su
 stake a los candidatos a validadores de la red, si lo utilizan como poder de voto para respaldar
 a los delegados. Los delegadores, a menudo, brindan soporte a los validadores que poseen los stakes más alto. A su vez, los validadores con el stake más alto tienen más posibilidades de que los elijan. Los delegados con más votos
 se convierten en los validadores de la red y pueden verificar transacciones. Al tiempo que utilizan su
 stake como poder de voto, en Avail no están sujetos a consecuencias mediante recortes en el caso de que
 su validador elegido se comportara de forma maliciosa. En otros sistemas de DPoS, a los delegadores se les pueden
 aplicar recortes.

En la NPoS, los delegadores se convierten en nominadores y utilizan su stake de una manera
 similar para nominar a los posibles candidatos a validadores para asegurar la red.
 El stake está bloqueado en la cadena y, en contraposición con la DPoS, los nominadores pueden sufrir recortes
 en función de una posible conducta maliciosa de aquellos a quienes hayan nominado. En tal sentido,
 la NPoS es un mecanismo proactivo de hacer staking, que contrasta con una forma de hacer staking del tipo “se fija y
 se olvida”, ya que los nominadores buscan validadores que actúen de forma adecuada y sean sostenibles. Esta
 también anima a los validadores a crear operaciones de validador sólidas para captar y
 mantener las nominaciones.

:::
