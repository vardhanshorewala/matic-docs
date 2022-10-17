---
id: pos-stake-unstake
title: Configurar y usar prueba de participación (PoS)
description: "Participar, no participar y otras instrucciones relacionadas con participación."
keywords:
  - docs
  - polygon
  - edge
  - stake
  - unstake
  - validator
  - epoch
---

## Resumen {#overview}

Esta guía entra en detalles sobre cómo configurar una red de prueba de participación con Polygon Edge, y como participar con fondos para nodos para convertirse en validadores y cómo desparticipar fondos.

Es **muy recomendable** leer y revisar
 La [Configuración Local](/docs/edge/get-started/set-up-ibft-locally)
 / [Secciones de configuración de la nube](/docs/edge/get-started/set-up-ibft-on-the-cloud) antes de continuar
 con esta guía de PoS (prueba de participación). Estas secciones describen los pasos necesarios para iniciar una prueba de autoridad (PoA) agrupada con el Polygon Edge.

Actualmente, no existe límite para la cantidad de validadores que pueden participar con fondos en el contrato de participación Smart.

## Contrato de Participación Smart {#staking-smart-contract}

El repositorio para el contrato de participación Smart se encuentra [aquí](https://github.com/0xPolygon/staking-contracts).

Este sostiene los guiones necesarios, de prueba de archivos ABI y, lo que es más importante, el contrato de participación en sí mismo.

## Configurar un grupo de nodos N {#setting-up-an-n-node-cluster}

Configurar una red con el Polygon Edge está cubierta en La [Configuración Local](/docs/edge/get-started/set-up-ibft-locally)
 / [secciones de configuración de la nube](/docs/edge/get-started/set-up-ibft-on-the-cloud).

La **única diferencia** entre configurar un PoS y un grupo PoA es en la parte de generación de genesis.

**Al generar el archivo de génesis para un grupo de PoS, es necesaria adicionar una bandera`--pos`**:

```bash
polygon-edge genesis --pos ...
```

## Establecer la duración de un epoch {#setting-the-length-of-an-epoch}

Los epochs se tratan en detalle en la [sección de bloques Epoch](/docs/edge/consensus/pos-concepts#epoch-blocks).

Para establecer el tamaño de un epoch para un grupo (en bloques), al generar el archivo de génesis, una bandera adicional es especificada`--epoch-size`:

```bash
polygon-edge genesis --epoch-size 50
```

Este valor especificado en el archivo de génesis que el tamaño de los epochs debería ser`50` bloques.

El valor por defecto para el tamaño de un epoch (en bloques) es.`100000`

:::info Reduciendo la longitud de los epoch.

Como se describe en la [sección de bloques de epoch](/docs/edge/consensus/pos-concepts#epoch-blocks),
 Los bloques de epoch son utilizados para actualizar los conjuntos de validadores para nodos.

La longitud por defecto de los epoch en los bloques (`100000`) puede tomar mucho tiempo para las actualizaciones del conjunto de validadores. Considerando que los nuevos bloques son agregados ~2s, tomaría ~55.5h para que el conjunto de validadores para posiblemente cambiarlos.

Establecer un valor inferior para la longitud de
:::

## Usando los guiones del contrato de participación Smart {#using-the-staking-smart-contract-scripts}

### Requisitos previos {#prerequisites}

El repositorio del contrato de participación Smart es un proyecto de Hardhat, que requiere NPM.

Para inicializarlo correctamente, en el directorio principal de ejecutar:

```bash
npm install
````

### Configurar los guiones de ayuda proporcionados {#setting-up-the-provided-helper-scripts}

Los guiones para interactuar con el contrato inteligente de participación Smart desplegado se encuentra en El [repositorio del contrato de participación Smart](https://github.com/0xPolygon/staking-contracts).

Crea un `.env`archivo con los siguientes parámetros en la ubicación del repositorio de contratos Smart

```bash
JSONRPC_URL=http://localhost:10002
PRIVATE_KEYS=0x0454f3ec51e7d6971fc345998bb2ba483a8d9d30d46ad890434e6f88ecb97544
STAKING_CONTRACT_ADDRESS=0x0000000000000000000000000000000000001001
BLS_PUBLIC_KEY=0xa..
```

Donde los parámetros están:

* **JSONRPC_URL** - el punto final JSON-RPC para el nodo en ejecución
* **CLAVES_PRIVADAS** - claves privadas de la dirección del participante.
* **DIRECCIÓN_DEL_CONTRATO_DE_PARTICIPACIÓN** - la dirección del contrato de participación Smart
 por defecto `0x0000000000000000000000000000000000001001`
* **CLAVE_PÚBLICA_BLS** - la clave pública BLS del participante. Solo es necesario si la red se ejecuta con BLS

### Fondos del participante {#staking-funds}

:::info Dirección del participante
El contrato Smart del participante se implementa previamente en dirección`0x0000000000000000000000000000000000001001`.

Cualquier tipo de interacción con el mecanismo de participación se realiza a través del contrato Smart del participante en la dirección especificada.

Para obtener más información sobre el contrato Smart del participante visita El [Contrato de participación Smart](/docs/edge/consensus/pos-concepts#contract-pre-deployment)
 sección.
:::

Para formar parte del grupo de validadores, una dirección debe participar con una cierta cantidad de fondos por encima de un umbral.

Actualmente, el umbral por defecto para formar parte del grupo de validadores es. `1 ETH`

La participación se puede iniciar llamando al método`stake` del contrato de participación Smart especificando un valor `>= 1 ETH`

Después del archivo`.env` mencionado en
 la [sección previa](/docs/edge/consensus/pos-stake-unstake#setting-up-the-provided-helper-scripts) se ha establecido, y una
 cadena se ha iniciado en el modo PoS, la participación se puede hacer con el siguiente comando en el repositorio del contrato de participación Smart:

```bash
npm run stake
```

El `stake`guion del Hardhat participa con una cantidad por defecto de`1 ETH`, que se puede cambiar modificando `scripts/stake.ts`
 el archivo.

Si los fondos que están participando son`>= 1 ETH` los que el validador estableció en el contrato de participan Smart se actualiza y la dirección
 forma parte del grupo de validadores a partir del siguiente epoch.

:::info Registrando las claves BLS
Si la red ejecuta en el modo BLS, para que los nodos se conviertan en validadores, ellos necesitan registrar sus claves públicas BLS después de participar

Esto se puede hacer con el siguiente comando:

```bash
npm run register-blskey
```
:::

### Fondos no participantes  {#unstaking-funds}

Las direcciones que tienen una participación pueden **solo retirar todos sus fondos** de inmediato.

Después del archivo`.env` mencionado en
 la [sección anterior](/docs/edge/consensus/pos-stake-unstake#setting-up-the-provided-helper-scripts)
 se ha configurado y una cadena se ha iniciado en el modo PoS, la participación se puede hacer con el siguiente comando en El repositorio del contrato Smart de participación:

```bash
npm run unstake
```

### Buscando la lista de los participantes {#fetching-the-list-of-stakers}

Todas las direcciones de participantes de fondos son guardadas en el contrato Smart de participación.

Después del archivo`.env` mencionado en
 la [sección anterior](/docs/edge/consensus/pos-stake-unstake#setting-up-the-provided-helper-scripts)
 se ha configurado, y una cadena se ha iniciado en el modo PoS, buscando la lista de validadores se puede hacer con los siguientes comandos en el repositorio del contrato Smart de participación:

```bash
npm run info
```
