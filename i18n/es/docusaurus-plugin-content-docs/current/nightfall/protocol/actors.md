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
- [Desafiantes](#challenger)

## Transactor {#transactor}
Un transactor es un cliente regular del servicio. Desean realizar transacciones, es decir, depositar, transferir y retirar de manera privada.
Estos clientes generalmente utilizarán una billetera web o un servidor dedicado (cliente) para realizar las pruebas ZK necesarias para generar las transacciones.

## Proponente {#proposer}
Un proponente cobra las transacciones de los clientes y propone nuevas actualizaciones al estado del
contrato del Escudo.
Por estado, nos referimos específicamente a las variables de almacenamiento asociadas con una transacción ZKP:
anuladores, y raíces de compromiso.
Las propuestas de actualización contienen varias transacciones, enrolladas en un bloque de capa 2. Solo un hash
del estado final, que existiría después de que todas las transacciones en el bloque fueran procesadas,
se almacena en cadena. Las transacciones se vuelven finales después de un período de 1 semana.

Cualquiera puede convertirse en proponente pero deben publicar alguna participación. La participación está destinada a incentivar un buen comportamiento.
Los proponentes ganan dinero al proporcionar bloques correctos y cobrar tarifas de transactores. Son algo análogos a los mineros en una cadena de bloques convencional.

## Desafiante {#challenger}
Un desafiante supervisa la corrección de los bloques propuestos dentro de una semana después de que el bloque fue enviado. Cualquiera puede ser un desafiante.
Los desafiantes toman la participación publicada por los proponentes al construir sus bloques cuando presentan de manera exitosa un desafío.


## Notas {#notes}
En la implementación de referencia de Polygon, tanto el proponente como el desafiante descargan algo de la funcionalidad a un módulo común llamado Optimist.
Este módulo Optimist proporciona algunos servicios a un número de proponentes y desafiantes, como generar y desafiar bloques
(el proponente y los desafiantes necesitarían firmar estas transacciones), sincronizando con eventos de cadena de bloques, etc.

Aparte de los actores descritos anteriormente, hay un actor adicional llamado Cliente. Un cliente actúa como un servicio de confianza que recopila transacciones de los usuarios, realiza las pruebas ZK en su nombre, envía transacciones al proponente, escucha eventos de cadena de bloques, etc. En resumen, el cliente actúa como un transmisor de confianza para un conjunto de usuarios que quieren descargar el pesado cálculo de pruebas y que confían entre sí.

La alternativa al cliente es utilizar la billetera navegador, un servicio sin servidor proporcionado por Polygon. Esta billetera gestiona todas las actividades de la transacción para un único usuario mientras se mantiene la privacidad.
