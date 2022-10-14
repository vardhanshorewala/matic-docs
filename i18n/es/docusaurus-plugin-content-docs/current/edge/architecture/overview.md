---
id: overview
title: Resumen de Arquitectura
sidebar_label: Overview
description: Introducción a la arquitectura de Polygon Edge.
keywords:
  - docs
  - polygon
  - edge
  - architecture
  - modular
  - layer
  - libp2p
  - extensible
---

Empezamos con la idea de hacer software que fuera *modular*.

Esto es algo que está presente en casi todas las partes del Polygon Edge. Abajo encontrarás una breve descripción general de la arquitectura construida y su estratificación.

## Estratificación de Polygon Edge {#polygon-edge-layering}

![Arquitectura de Polygon Edge](/img/edge/Architecture.jpg)

## Libp2p {#libp2p}

Todo comienza en la capa de red base, que utiliza **libp2p**. Decidimos ir con esta tecnología porque encaja dentro de las filosofías de diseño de Polygon Edge. Libp2p es:

- Modular
- Extensible
- Rápida

Lo más importante es que proporciona una base excelente para características más avanzadas, las cuales cubriremos más adelante.


## Sincronización y Consensus {#synchronization-consensus}
La separación de los protocolos de sincronización y consenso permiten modularidad e implementación de **personalizados** mecanismos de sincronización y consensus, dependiendo de cómo esté ejecutando el cliente.

Polygon Edge está diseñado para ofrecer algoritmos de consensus conectables existentes.

La lista actual de algoritmos consensus soportados:

* IBFT PoA
* IBFT PoS

## Cadena de bloques {#blockchain}
La capa de cadena de bloques es la capa central que coordina todo dentro del sistema Polygon Edge. Que está cubierto en profundidad en la sección correspondiente de *Módulos*.

## Declaración {#state}
La capa interna de declaración contiene una lógica transición de declaración. Se trata de cómo cambia la declaración cuando se incluye un nuevo bloque. Que está cubierto en profundidad en la sección correspondiente de *Módulos*.

## JSON RPC {#json-rpc}
La capa JSON RPC es una capa de API que los desarrolladores de aplicaciones descentralizadas utilizan para interactuar con la cadena de bloques. Que está cubierto en profundidad en la sección correspondiente de *Módulos*.

## TxPool {#txpool}
La capa de TxPool representa al grupo de transacciones, y está estrechamente relacionada con otros módulos en el sistema, ya que las transacciones se pueden agregar desde múltiples puntos de entrada.

## GRPC {#grpc}
La capa de GRPC es vital para las interacciones de los operadores. A través de ella, los operadores de nodos pueden fácilmente interactuar con el cliente, proporcionando una UX agradable.