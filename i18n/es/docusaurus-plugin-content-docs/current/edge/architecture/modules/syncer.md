---
id: syncer
title: Syncer
description: Explicación para el módulo Syncer de Polygon Edge.
keywords:
  - docs
  - polygon
  - edge
  - architecture
  - module
  - synchronization
---

## Resumen {#overview}

Este módulo contiene la lógica para el protocolo de sincronización. Se utiliza para sincronizar un nuevo nodo con la red en ejecución, o para validar/insertar nuevos bloques para los nodos los cuales no participan en consensus (no validadores).

El Polygon Edge utiliza **libp2p** como la capa de red, y encima de eso se ejecuta en **gRPC**

Existen esencialmente 2 tipos de sincronización en Polygon Edge:
* Bulk Sync: sincroniza una gran variedad de bloques a la vez
* Watch Sync - sincronización por bloque

### Bulk Sync {#bulk-sync}

Los pasos para el Bulk Sync son bastante sencillos para acomodar el objetivo de Bulk Sync - sincronizando tantos bloques como sea posible (disponibles) de otro par para poder ponerse al día, lo más rápido posible.

Este es el flujo del proceso de Bulk Sync:

1. ** Determinar si el nodo necesita de Bulk Sync ** - En este paso el nodo revisa mapa de pares para ver si hay alguien que tenga un número más grande de bloque que lo que el nodo tiene localmente
2. ** Encuentra el mejor par (utilizando el mapa de sincronización de pares) ** - En este paso el nodo encuentra el mejor par para sincronizarse basado con los criterios mencionados en el ejemplo anterior.
3. **Abrir una secuencia de sincronización masiva ** En este paso el nodo abre una secuencia de gRPC para transmitir al mejor par para sincronizar bloques de forma masiva desde el número de bloque común
4. ** El mejor par cierra la secuencia cuando se realiza el envío masivo ** - En este paso el mejor par el nodo se está sincronizando con el que se cerrará la secuencia tan pronto como se envíen todos los bloques disponibles que tiene
5. ** Cuando se realiza la sincronización masiva, revisa si el nodo es un validador ** - En este paso la secuencia se cierra por el mejor par, y el nodo necesita revisar si son un validador después de la sincronización masiva.
  * Si son, saltan de la declaración de sincronización e inician la participación en Consensus
  * Si no lo son, continúan a ** Watch Sync **

### Watch Sync {#watch-sync}

:::info
El paso para Watch Sync solo se ejecuta si el nodo no es un validador, sino un nodo no validador regular en la red que solo escucha los bloques que se aproximan.
:::

El comportamiento de Watch Sync es bastante sencillo, el nodo ya está sincronizado con el resto de la red y solo necesita analizar nuevos bloques que están entrando.

Este es el flujo del proceso de Watch Sync:

1. **Agregar un nuevo bloque cuando el estado de un par se actualiza** - En este paso los nodos escuchan los nuevos eventos del bloque, cuando tenga un nuevo bloque este ejecutará una llamada a la función gRPC, que obtendrá el bloque y actualizará la declaración local.
2. ** Revisar si el nodo es un validador después de sincronizar el bloque más reciente**
   * Si es así, salte de la declaración de sincronización
   * Si no lo es, continúe escuchando los nuevos eventos del bloque

## Informe de Rendimiento {#perfomance-report}

:::info
El rendimiento se midió en una máquina local sincronizando ** millones de bloques**
:::

| Nombre | Resultado |
|----------------------|----------------|
| Sincronización de 1 millón de bloques | ~ 25 min |
| Transferencia de 1 millón de bloques | ~ 1 min |
| Número de llamadas GRPC | 2 |
| Prueba de cobertura | ~ 93% |