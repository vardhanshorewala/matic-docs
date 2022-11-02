---
id: avail-consensus
title: Consenso Avail
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

Hasta ahora, el enfoque para mantener las soluciones de aplicación descentralizada, en general ha sido a través
 de un DAC (comíte de disponibilidad de datos, según sus siglas en inglés). Un DAC es el responsable de devolver
 las firmas a la cadena principal y que acreditan la disponibilidad fuera de la cadena
 de datos. El DAC debe asegurar que los datos estarán disponibles de inmediato.

A través de un DAC, las soluciones de escalamiento se basan en un DAC para alcanzar un Validium. El problema
 con los DAC es que la disponibilidad de datos se convierte en un servicio de confianza sobre un pequeño grupo
 de los grupos del comité, que son los responsables de almacenar y notificar los datos con veracidad.

Avail no es un DAC, pero sí una red de cadena de bloques real con su mecanismo
 de consenso y que tiene su propio conjunto de nodos validadores y productores de bloques.

## Prueba de participación {#proof-of-stake}

:::caution Validadores actuales

Con el lanzamiento inicial de la red de prueba de Avail, los validadores
 se operarán y mantendrán de forma interna por Polygon.

:::

Los sistemas de prueba de participación tradicionales requieren que los autores de producción de bloques cuenten con
 tenencias de token (stake) en la cadena para producir bloques, en contraposición a los recursos
 computacionales (trabajo).

Los productos de Polygon utilizan PoS prueba de participación o una modificación de PoS.

En general, los validadores de los sistemas PoS tradicionales que cuentan con el mayor stake
 son los que tienen más influencia y control de la red. Los sistemas con muchos mantenedores de red
 tienden a formar pools fuera de la cadena para maximizar las ganancias de capital, al reducir la diferencia de recompensa. Esta
 problema de centralización se vuelve menos desafiante cuando los pools están incluidos en la cadena, lo que permite que los poseedores
 de tokens regresen con los mantenedores de la red con quienes sientan que mejor los representan a ellos y a los intereses
 de la red. Esto también hace que se distribuya la concentración de poder de los validadores, si se supone
 que existen mecanimos de votación y de elección correctos, ya que la stake general de la red
 se asigna como una relación de uno a muchos o de muchos a muchos, en lugar de solo delegar en
 una relación uno a uno, en la que la confianza se pone en los validadores que “hicieron más staking”. Esta
 modificación de la prueba de participación se puede adminsitrar a través de la delegación o de la nominación,
 a la que comúnmente se la denomida DPoS (prueba de participación delegada) o NPoS (prueba de participación nominada).
 Las soluciones de escalamiento de Polygon han adaptado estos mecanismos mejorados con la inclusión de
 Avail de Polygon.

Avail utiliza NPoS con una modificación en la verificación de bloques. Los actores involucrados aún
 son validadores y nominadores.

Los clientes ligeros también contribuyen a la disponiblidad de datos en Avail. El consenso de Avail
 requiere que dos tercios más 1 de los validadores alcancen consenso para la validez.

## Nominadores {#nominators}

Los nominadores pueden elegir respaldar a un conjunto candidato de validadores de Avail con su
 stake. Los nominadores nominarán a los validadores que crean
 que proporcionarán la disponibilidad de datos de forma efectiva.

:::info ¿Cuál es la diferencia entre DPos y NPoS

Si se tiene en cuenta el valor nominal, delegar y nominar parecen ser la misma acción, en especial
 desde el punto de vista de un staker afincionado. Sin embargo, las diferencias subyacen en los
 mecanismos de consenso y en cómo se produce la selección de los validadores.

En DPoS, un sistema de elección centrado en la votación determina un número fijo de
 validadores para asegurar la red. Los delegadores pueden delegar sus
 stakes contra los validadores de la red de candidatos, al utilizarla como poder de voto para respaldar
 a los delegados. Los delegadores a menudo brindan soporte a los validadores en que cuentan con los stakes más altos. Al contar con eso,
 los validadores tienen más posibilidades de que los eligan. Los delegados con más votos
 se convierte en los validadores de la red y pueden verificar las transacciones. Al tiempo que utilizan su
 stake como poder de voto, en Avail, no están sujetos a consecuencias mediante recortes en el caso de que
 su validador elegido se comportara de forma maliciosa. En otros sistemas de DPoS, los delegadores pueden
 estar sujetos a recortes.

En NPoS, los delegadores se convierten en nominadores y utilizan su stake de una manera
 similar para designar a los posibles candidatos a validadores para asegurar la red.
 El stake está bloqueado en la cadena, y a diferencia de la DPoS, los nominadores están sujetos a recortes
 en función de una posible conducta maliciosa de sus nominaciones. En tal sentido,
 NPoS es mecanismo proactivo de hacer staking, que contrasta con una forma de hacer staking que “se fija y
 se olvida”, ya que los nominadores buscan validadores que actúen de forma adecuada y sean sostenibles. Esto
 también anima a los validadores a crear operaciones de validador sólidas para captar y
 mantener las nominaciones.

:::
