---
id: actors
title: Actores
sidebar_label: Actors
description: "Tipos de actores en Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - transactor
  - proposer
  - challenger
  - liquidity
  - provider
image: https://matic.network/banners/matic-network-16x9.png
---

Hay cuatro actores involucrados en la red:

- [Transactores](#transactor)
- [Proponentes](#proposer)
- [Desafiadores](#challenger)

## Transactores {#transactor}
Un Transactor es un cliente regular del servicio. Desean realizar transacciones, es decir, depositar, transferir y retirar de forma privada.
Estos clientes típicamente usan una billetera web o un servidor dedicado al (Cliente) para realizar las pruebas necesarias de ZK para generar las transacciones.

## Proponente de bloques {#proposer}
Un proponente recoge las transacciones de los clientes y propone nuevas actualizaciones para declarar del
contrato de Shield.
Por estado nos referimos específicamente a las variables de almacenamiento asociadas con una transacción de ZKP:
anuladores y raíces de compromiso.
Las propuestas de actualización contienen varias transacciones, haciendo rollup hacia una capa de bloque 2. Solo un hash
de la declaración final que existiría después de que todas las transacciones en el bloque que fueron procesadas
se almacenan en la cadena. Las transacciones se vuelven finales después de un periodo de 1 semana.

Cualquiera puede convertirse en proponente, pero deben publicar algún stake. El stake es intentar incentivar un buen comportamiento. Los proponentes ganan dinero al proporcionar los bloques correctos, recogiendo tarifas de los transactores. Ellos son algo análogos a los mineros en una cadena de bloques convencionales.

## Retadores {#challenger}
Un retador supervisa la corrección de los bloques propuestos dentro de una semana después de que se enviaron los bloques. Cualquiera puede ser un retador.
Los retadores toman el stake que publicaron los proponentes cuando construyen sus bloques cuando envían con éxito un reto.


## Notas {#notes}
En la implementación de la referencia de Polygon, tanto el proponente y el retador descargan alguna funcionalidad a un módulo común llamado Optimist.
Este módulo Optimist proporciona algunos servicios a una serie de proponentes y retadores, como, por ejemplo, generadores y retadores de bloques
(Proponentes y retadores necesitarían firmar estas transacciones), sincronizándose con los eventos de cadenas de bloques, etcétera.

Aparte de los actores descritos anteriormente, hay un actor adicional cliente. Un cliente actúa como un servicio de confianza que recoge, las transacciones de un usuario y realiza las pruebas de ZK en su nombre, envía transacciones al proponente y escucha los eventos de cadena de bloques etc. En resumen, El cliente actúa como un repetidor de confianza para una colección de usuarios que quieren descargar la prueba pesada de computación y que confían entre sí.

La alternativa al cliente es usar la billetera de navegador, un servicio sin servidor que proporciona Polygon. Esta billetera administra todas las actividades de transacciones para un único usuario mientras mantiene la privacidad.
