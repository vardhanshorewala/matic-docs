---
id: poa
title: Prueba de Autoridad (PoA)
description: "Explicación e instrucciones acerca de la prueba de autoridad."
keywords:
  - docs
  - polygon
  - edge
  - PoA
  - autorithy
---

## Resumen {#overview}

El PoA IBFT es el mecanismo consensus por defecto en el Polygon Edge. En PoA, los validadores son los únicos responsables para crear los bloques y agregarlos a la cadena de bloques en una serie.

Todos los validadores forman un conjunto de validadores dinámicos, donde los validadores pueden agregarse o eliminarse del conjunto mediante el empleo de un mecanismo de votación. Esto significa que los validadores pueden ser votados dentro / fuera del conjunto de validadores si la mayoría (51%) de los nodos validadores votan para agregar/sacar a un determinado validador del conjunto. De esta manera, los validadores maliciosos pueden ser reconocidos y eliminados de la red, mientras nuevos validadores de confianza pueden agregarse a la red.

Todos los validadores toman turnos para proponer el siguiente bloque todos contra todos (round-robin), y para el bloque que sea validado/insertado, en la cadena de bloques una supermayoría de los validadores (más de 2/3) debe aprobar el mencionado bloque.

Además de los validadores, hay no validadores que no participan en la creación del bloque, pero participan en el proceso de validación del bloque.

## Agregar un validador al conjunto de validadores {#adding-a-validator-to-the-validator-set}

Esta guía describe cómo agregar a un nuevo nodo validador a una red IBFT activa con 4 nodos validadores. Si necesita ayuda para configurar la red, consulte las secciones [Configuración local](/docs/edge/get-started/set-up-ibft-locally) / [Configuración en la nube](/docs/edge/get-started/set-up-ibft-on-the-cloud).

### paso 1: Inicializa las carpetas de datos para IBFT y genera claves validadores para el nuevo nodo  {#step-1-initialize-data-folders-for-ibft-and-generate-validator-keys-for-the-new-node}

Para comenzar a utilizar IBFT en el nuevo nodo, primero debes inicializar las carpetas de datos y generar las claves:

````bash
polygon-edge secrets init --data-dir test-chain-5
````

Este comando imprimirá la clave del validador La dirección y la identificación del nodo. Necesitará la clave del validador la dirección para el paso siguiente.

### paso 2: Proponga un nuevo candidato de otros nodos validadores {#step-2-propose-a-new-candidate-from-other-validator-nodes}

Para que un nuevo nodo se convierta en un validador al menos el 51% de los validadores necesitan proponerlo.

Ejemplo de cómo proponer un nuevo validador (`0x8B15464F8233F718c8605B16eBADA6fc09181fC2`) desde el nodo validador existente en la dirección grpc: 127.0.0.1:10000:

````bash
polygon-edge ibft propose --grpc-address 127.0.0.1:10000 --addr 0x8B15464F8233F718c8605B16eBADA6fc09181fC2 --bls 0x9952735ca14734955e114a62e4c26a90bce42b4627a393418372968fa36e73a0ef8db68bba11ea967ff883e429b3bfdf --vote auth
````

La estructura de los comandos IBFT se cubre en la sección [Comandos de CLI](/docs/edge/get-started/cli-commands).

:::info Clave pública BLS

La clave pública BLS solo es necesaria si la red se ejecuta con el BLS, para la red que no se ejecuta en modo BLS `--bls`es innecesaria

:::

### Paso 3: Ejecutar el nodo cliente {#step-3-run-the-client-node}

Porque en este ejemplo estamos intentando el ejecutar la red donde todos los nodos se encuentran en la misma máquina, necesitamos tener cuidado para evitar conflictos de puerto.

````bash
polygon-edge server --data-dir ./test-chain-5 --chain genesis.json --grpc-address :50000 --libp2p :50001 --jsonrpc :50002 --seal
````

Después de buscar todos los bloques, dentro de tu consola notarás que un nuevo nodo está participando en la validación

````bash
2021-12-01T14:56:48.369+0100 [INFO]  polygon.consensus.ibft.acceptState: Accept state: sequence=4004
2021-12-01T14:56:48.369+0100 [INFO]  polygon.consensus.ibft: current snapshot: validators=5 votes=0
2021-12-01T14:56:48.369+0100 [INFO]  polygon.consensus.ibft: proposer calculated: proposer=0x8B15464F8233F718c8605B16eBADA6fc09181fC2 block=4004
````

:::info Promocionar un no validador a un validador

Naturalmente, un no validador puede convertirse en un validador mediante la votación, pero para que se incluya con éxito en el conjunto de validadores después del proceso de votación, el nodo se debe reiniciar con la bandera. `--seal`

:::

## Eliminar un validador del conjunto de validadores {#removing-a-validator-from-the-validator-set}

Esta operación es bastante simple. Para eliminar un nodo validador del conjunto de validadores, este comando se necesita realizar para la mayoría de los nodos validadores.

````bash
polygon-edge ibft propose --grpc-address 127.0.0.1:10000 --addr 0x8B15464F8233F718c8605B16eBADA6fc09181fC2 --bls 0x9952735ca14734955e114a62e4c26a90bce42b4627a393418372968fa36e73a0ef8db68bba11ea967ff883e429b3bfdf --vote drop
````

:::info Clave pública BLS

La clave pública BLS solo es necesaria si la red se ejecuta con el BLS, para la red que no se ejecuta en modo BLS `--bls`es innecesaria

:::

Después de que se realizan los comandos, observa que número de validadores se ha reducido (en este ejemplo de registro de 4 a 3).

````bash
2021-12-15T19:20:51.014+0100 [INFO]  polygon.consensus.ibft.acceptState: Accept state: sequence=2399 round=1
2021-12-15T19:20:51.014+0100 [INFO]  polygon.consensus.ibft: current snapshot: validators=4 votes=2
2021-12-15T19:20:51.015+0100 [INFO]  polygon.consensus.ibft.acceptState: we are the proposer: block=2399
2021-12-15T19:20:51.015+0100 [INFO]  polygon.consensus.ibft: picked out txns from pool: num=0 remaining=0
2021-12-15T19:20:51.015+0100 [INFO]  polygon.consensus.ibft: build block: number=2399 txns=0
2021-12-15T19:20:53.002+0100 [INFO]  polygon.consensus.ibft: state change: new=ValidateState
2021-12-15T19:20:53.009+0100 [INFO]  polygon.consensus.ibft: state change: new=CommitState
2021-12-15T19:20:53.009+0100 [INFO]  polygon.blockchain: write block: num=2399 parent=0x768b3bdf26cdc770525e0be549b1fddb3e389429e2d302cb52af1722f85f798c
2021-12-15T19:20:53.011+0100 [INFO]  polygon.blockchain: new block: number=2399 hash=0x6538286881d32dc7722dd9f64b71ec85693ee9576e8a2613987c4d0ab9d83590 txns=0 generation_time_in_sec=2
2021-12-15T19:20:53.011+0100 [INFO]  polygon.blockchain: new head: hash=0x6538286881d32dc7722dd9f64b71ec85693ee9576e8a2613987c4d0ab9d83590 number=2399
2021-12-15T19:20:53.011+0100 [INFO]  polygon.consensus.ibft: block committed: sequence=2399 hash=0x6538286881d32dc7722dd9f64b71ec85693ee9576e8a2613987c4d0ab9d83590 validators=4 rounds=1 committed=3
2021-12-15T19:20:53.012+0100 [INFO]  polygon.consensus.ibft: state change: new=AcceptState
2021-12-15T19:20:53.012+0100 [INFO]  polygon.consensus.ibft.acceptState: Accept state: sequence=2400 round=1
2021-12-15T19:20:53.012+0100 [INFO]  polygon.consensus.ibft: current snapshot: validators=3 votes=0
2021-12-15T19:20:53.012+0100 [INFO]  polygon.consensus.ibft: proposer calculated: proposer=0xea21efC826F4f3Cb5cFc0f986A4d69C095c2838b block=2400
````
