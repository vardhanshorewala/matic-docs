---
id: pos-concepts
title: Prueba de participación
description: "Explicación e instrucciones acerca de la prueba de participación"
keywords:
  - docs
  - polygon
  - edge
  - PoS
  - stake
---

## Resumen {#overview}

Esta sección tiene como objetivo proporcionar una mejor visión general de algunos conceptos actualmente presentes en la prueba de participación (PoS) implementación del Polygon Edge.

La implementación del Polygon Edge prueba de participación (PoS) se entiende que es una alternativa a la implementación existente de PoA IBFT, dándole a los operadores de nodo la capacidad de elegir fácilmente entre los dos cuando se inicia una cadena

## Características de PoS (prueba de participación) {#pos-features}

La lógica central detrás de la implementación de una prueba de participación se encuentra dentro de [participación en un contrato Smart](https://github.com/0xPolygon/staking-contracts/blob/main/contracts/staking.sol).

Este contrato se implementa previamente cada vez que se inicializa una cadena Polygon Edge del mecanismo PoS y está disponible en la dirección
`0x0000000000000000000000000000000000001001`  desde el bloque`0`.

### Epochs {#epochs}

Epochs es un concepto introducido con la adición de PoS (prueba de participación) al Polygon Edge.

Epochs es considerado un marco de tiempo (u hora) especial (en bloques) en el que un conjunto determinado de validadores puede producir bloques. Sus longitudes son modificables, lo que significa que los operadores de nodos pueden configurar la duración de una epoch durante la generación de génesis.

Al final de cada epoch se crea un _bloque epoch_, y después de ese evento comienza un nuevo epoch. Para obtener más información acerca de los bloques epoch, ve la sección [Bloques Epoch](/docs/edge/consensus/pos-concepts#epoch-blocks).

Los conjuntos de validadores se actualizan al final de cada epoch. Los nodos consultan el conjunto de validadores del contrato de participación Smart durante la creación del bloque epoch, y guardar los datos obtenidos en el almacenamiento local. Esta consulta y el ciclo se repite al final de cada epoch.

Esencialmente, se asegura que el contrato de participación Smart tenga control completo sobre las direcciones en el conjunto de validadores, y deja a los nodos con solo 1 responsabilidad: el consultar el contrato una vez durante un epoch para obtener el validador más reciente y establecer información. Esto alivia la responsabilidad de los nodos individuales de cuidar los conjuntos de validadores.

### Participación {#staking}

Las direcciones pueden participar en fondos en el contrato de participación Smart invocando el método `stake`y especificando un valor para
 la cantidad de participación en la transacción:

````js
const StakingContractFactory = await ethers.getContractFactory("Staking");
let stakingContract = await StakingContractFactory.attach(STAKING_CONTRACT_ADDRESS)
as
Staking;
stakingContract = stakingContract.connect(account);

const tx = await stakingContract.stake({value: STAKE_AMOUNT})
````

Al participar con fondos en el contrato de participación Smart las direcciones pueden ingresar al conjunto de validadores y así poder participar en el proceso de producción de bloques.

:::info Umbral para participar

Actualmente, el umbral mínimo para ingresar al conjunto de validadores es participar `1 ETH`

:::

### No Participación (Des-participación) {#unstaking}

Las direcciones que tienen fondos de participación solo pueden **dejar de participar con todos sus fondos de participación a la vez**.

La no participación se puede invocar llamando al método`unstake` en el contrato de participación Smart:

````js
const StakingContractFactory = await ethers.getContractFactory("Staking");
let stakingContract = await StakingContractFactory.attach(STAKING_CONTRACT_ADDRESS)
as
Staking;
stakingContract = stakingContract.connect(account);

const tx = await stakingContract.unstake()
````

Después de desparticipar sus fondos las direcciones se eliminan del conjunto de validadores en el contrato de participación Smart y no ser considerados validadores durante el siguiente epoch.

## Bloques de Epoch {#epoch-blocks}

**Bloques Epoch** son un concepto introducido en la implementación de PoS de IBFT en Polygon Edge.

Esencialmente, los bloques de epoch son bloques especiales que contienen **no transacciones** y ocurren solo al **final de un epoch**.
 Por ejemplo, si el **tamaño de un epoch**se establece en`50` bloques, epoch los bloques serán considerados que son bloques`50`, `100`
  `150`y así sucesivamente.

Se utilizan para realizar una lógica adicional que no debería ocurrir durante la producción regular de bloques.

Lo que es más importante, son una indicación para el nodo que **necesita obtener la información más reciente del conjunto de validadores**
 de la participación en un contrato Smart.

Después de actualizar el conjunto de validadores en el bloque epoch, el conjunto de validadores (ya sea cambiado o sin cambios) se utiliza para los siguientes bloques `epochSize - 1`hasta que se actualiza de nuevo extrayendo la información más reciente de de participación en un contrato Smart.

Las longitudes de epoch (en bloques) se pueden modificar al generar el archivo de génesis, mediante el uso de una bandera especial`--epoch-size`:

```bash
polygon-edge genesis --epoch-size 50 ...
```

El tamaño por defecto de un epoch es`100000` bloques en el Polygon Edge.

## Pre-despliegue de contrato {#contract-pre-deployment}

El Polygon Edge _pre-desplieges_
 El [Contrato de participación Smart](https://github.com/0xPolygon/staking-contracts/blob/main/contracts/Staking.sol)
 durante **la generación de genesis** a las direcciones`0x0000000000000000000000000000000000001001`.

Lo hace sin un EVM en ejecución, modificando el estado de la cadena de bloques del contrato Smart directamente, usando el pasado en la configuración de los valores al comando genesis.
