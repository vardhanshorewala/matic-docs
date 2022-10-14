---
id: bls
title: BLS
description: "Explicación e instrucciones relativas al modo BLS."
keywords:
  - docs
  - polygon
  - edge
  - bls
---

## Resumen {#overview}

BLS es un esquema de firma que puedes agregar varias firmas. En el Polygon Edge BLS se utiliza por defecto para proporcionar mejor seguridad en el modo consensus IBFT. BLS puedes agregar firmas en un solo array de bytes y reducir el tamaño del encabezado del bloque Cada cadena puede elegir si se debe usar BLS o no. La clave ECDSA se utiliza independientemente de si el modo BLS está habilitado o no.

## Cómo configurar una nueva cadena usando BLS {#how-to-setup-a-new-chain-using-bls}

Consulte las secciones [Configuración Local](/docs/edge/get-started/set-up-ibft-locally) / [Configuración de la Nube](/docs/edge/get-started/set-up-ibft-on-the-cloud)para obtener instrucciones de configuración detalladas.

## Cómo migrar desde una existente cadena ECDSA PoA a la cadena BLS PoA {#how-to-migrate-from-an-existing-ecdsa-poa-chain-to-bls-poa-chain}

Esta sección describe cómo usar el modo BLS en una cadena existente de PoA. los siguientes pasos son necesarios para habilitar BLS en una cadena PoA.

1. Detén todos los nodos
2. Genera las claves BLS para validadores
3. Agrega una configuración de bifurcación en genesis.json
4. Reinicie todos los nodos

### 1. Detenga todos los nodos {#1-stop-all-nodes}

Termine todos los procesos de los validadores presionando Ctrl + c (Control + c). Recuerde la altura del bloque más reciente (el número de secuencia más alto en el registro comprometido de bloques).

### 2. Genera la clave BLS {#2-generate-the-bls-key}

`secrets init` con la `--bls`genera la clave BLS. Para mantener la clave ECDSA y de red existente y agregar una nueva clave BLS,`--ecdsa` y `--network`es necesario desactivarlas.

```bash
polygon-edge secrets init --bls --ecdsa=false --network=false

[SECRETS INIT]
Public key (address) = 0x...
BLS Public key       = 0x...
Node ID              = 16...
```

### 3. Agrega la configuración de la bifurcación {#3-add-fork-setting}

`ibft switch`El comando agrega una configuración de bifurcación, que habilita BLS en la cadena existente, en`genesis.json`.

Para las redes PoA, los validadores necesitan ser proporcionados en el comando. Al igual que con la forma de `genesis`comando, `--ibft-validators-prefix-path`o las banderas `--ibft-validator`se pueden usar para especificar el validador.

Especifica la altura a partir de la cual la cadena comienza a usar BLS con la bandera`--from`.

```bash
polygon-edge ibft switch --chain ./genesis.json --type PoA --ibft-validator-type bls --ibft-validators-prefix-path test-chain- --from 100
```

### 4. Reinicia todos los nodos {#4-restart-all-nodes}

Reinicia todos los nodos mediante el comando`server`. Después de crear el bloque en el`from` especificado en el paso anterior, la cadena habilita el BLS y muestra los registros como se muestra a continuación:

```bash
2022-09-02T11:45:24.535+0300 [INFO]  polygon.ibft: IBFT validation type switched: old=ecdsa new=bls
```

También los registros muestran qué modo de verificación se utiliza para generar bloque después de que bloque se crea.

```
2022-09-02T11:45:28.728+0300 [INFO]  polygon.ibft: block committed: number=101 hash=0x5f33aa8cea4e849807ca5e350cb79f603a0d69a39f792e782f48d3ea57ac46ca validation_type=bls validators=3 committed=3
```

## Cómo migrar desde una existente cadena ECDSA PoA a la cadena BLS PoA {#how-to-migrate-from-an-existing-ecdsa-pos-chain-to-a-bls-pos-chain}

Esta sección describe cómo usar el modo BLS en una cadena existente de PoA. Los siguientes pasos los siguientes pasos son necesarios para habilitar BLS en una cadena PoA.

1. Detén todos los nodos
2. Genera las claves BLS para validadores
3. Agrega una configuración de bifurcación en genesis.json
4. Llama al contrato de participación para registrar la clave pública de BLS
5. Reinicie todos los nodos

### 1. Detenga todos los nodos {#1-stop-all-nodes-1}

Termine todos los procesos de los validadores presionando Ctrl + c (Control + c). Recuerde la altura del bloque más reciente (el número de secuencia más alto en el registro comprometido de bloques).

### 2. Genera la clave BLS {#2-generate-the-bls-key-1}

`secrets init` con la bandera `--bls`se genera la clave BLS. Para mantener la clave ECDSA y de red existente y agregar una nueva clave BLS,`--ecdsa` y `--network`es necesario desactivarlas.

```bash
polygon-edge secrets init --bls --ecdsa=false --network=false

[SECRETS INIT]
Public key (address) = 0x...
BLS Public key       = 0x...
Node ID              = 16...
```

### 3. Agrega la configuración de la bifurcación {#3-add-fork-setting-1}

`ibft switch`El comando agrega una configuración de horquilla, que habilita BLS desde la mitad de la cadena, dentro`genesis.json`.

Especifica la altura desde la que comienza la cadena utilizando el modo BLS con la bandera, `from`y la altura a la que se actualiza el contrato con la bandera `development`

```bash
polygon-edge ibft switch --chain ./genesis.json --type PoS --ibft-validator-type bls --deployment 50 --from 200
```

### 4. Registra la clave pública BLS en el contrato de participación {#4-register-bls-public-key-in-staking-contract}

Después de agregar la bifurcación y reiniciar los validadores, cada validador debe llamar `registerBLSPublicKey`en el contrato de participación para registrar la clave pública BLS. Esto debe hacerse después de la altura especificada en `--deployment`antes de la altura especificada en`--from`.

El script para registrar la clave pública BLS se define en [Replanteo de informes de contratos inteligentes](https://github.com/0xPolygon/staking-contracts).

Establecer`BLS_PUBLIC_KEY` estar registrado en el archivo`.env`. Consulta [deshacer prueba de participación](/docs/edge/consensus/pos-stake-unstake#setting-up-the-provided-helper-scripts) para obtener más detalles sobre otros parámetros.

```env
JSONRPC_URL=http://localhost:10002
STAKING_CONTRACT_ADDRESS=0x0000000000000000000000000000000000001001
PRIVATE_KEYS=0x...
BLS_PUBLIC_KEY=0x...
```

El siguiente comando registra la clave pública BLS dada en el contrato. `.env`

```bash
npm run register-blskey
```

:::warning Los validadores necesitan registrar la clave pública BLS manualmente
En el modo BLS, los validadores deben tener su propia dirección y la clave pública BLS. La capa consensus ignora a los validadores que no han registrado la clave pública BLS en el contrato cuando el consensus obtiene información del validador del contrato.
:::

### 5. Reinicia todos los nodos {#5-restart-all-nodes}

Reinicia todos los nodos mediante el comando`server`. La cadena habilita el BLS después de que el bloque en el `from`especificado en el paso anterior es creado.