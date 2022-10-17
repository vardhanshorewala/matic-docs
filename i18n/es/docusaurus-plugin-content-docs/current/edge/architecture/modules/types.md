---
id: types
title: Tipos
description: Explicación para el tipo de módulos de Polygon Edge.
keywords:
  - docs
  - polygon
  - edge
  - architecture
  - module
  - types
  - marshaling
---

## Resumen {#overview}

El módulo **Tipos** implementa tipos de objetos principales, tales como:

* **Dirección**
* **Hash**
* **Encabezado**
* muchas funciones de ayuda

## Codificación/descodificación RLP {#rlp-encoding-decoding}

A diferencia de clientes como GETH, Polygon Edge no se utiliza la reflexión para la codificación.<br />
 La preferencia era no usar la reflexión porque esta introduce nuevos problemas, como el rendimiento degradación y escalamiento más duro.

El módulo de **Tipos** proporciona una interfaz fácil de usar para clasificar y desclasificar RLP, utilizando el paquete FastRLP.

La clasificación se hace a través de los métodos *MarshalRLPWith* y *MarshalRLPTo* Los métodos análogos existen para desclasificar.

Al definir estos métodos de forma manual, el Polygon Edge no necesita usar la reflexión. En *rlp_marshal.go*, puedes encontrar
 métodos para clasificar:

* **Cuerpos**
* **Bloques**
* **Encabezados**
* **Recibos**
* **Registros**
* **Transacciones**