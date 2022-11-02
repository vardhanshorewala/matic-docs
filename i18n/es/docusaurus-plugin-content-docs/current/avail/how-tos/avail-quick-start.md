---
id: avail-quick-start
title: Cómo utilizar Polygon Avail
sidebar_label: How to use Avail
description: Obtén información sobre cómo utilizar Polygon Avail
keywords:
  - docs
  - polygon
  - avail
  - data
  - availability
  - how-to
  - extrinsic
  - explorer
image: https://matic.network/banners/matic-network-16x9.png
slug: avail-quick-start
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import useBaseUrl from '@docusaurus/useBaseUrl';

:::note Estamos trabajando para mejorar muchas de las características actuales

Apreciamos que utilice nuestra red de prueba y lo alentamos a dar sus valiosos comentarios a través de uno de nuestros **[canales de comunidad](https://polygon.technology/community/)**.

:::

## Generar una cuenta de Avail {#generate-an-avail-account}

Puedes generar una cuenta utilizando uno de estos dos métodos:
- [Explorador de Avail](https://testnet.polygonavail.net/)
- Console/Typescript

<TabItem value="explorer"><Tabs
defaultValue="explorer"
values={[
{ label: 'Avail Explorer', value: 'explorer', },
{ label: '@polkadot/api', value: 'library', },
]
}>


Dirígete a [Explorador de Avail](https://testnet.polygonavail.net/).

<img src={useBaseUrl("img/avail/avail-explorer.png")} width="100%" height="100%"/>

:::note

**[Explorador Avail](https://testnet.polygonavail.net/)** es un bifurcador
 de **[las aplicaciones de Polkadot-JS](https://polkadot.js.org/)**. La interfaz y la navegación son los mismos si estás familiarizado con las aplicaciones de Polkadot-JS.

:::

Navega en **pestaña de Cuentas** y da clic en la **Subpestaña Cuentas**

<img src={useBaseUrl("img/avail/account.png")} width="100%" height="100%"/>

:::info Formato de dirección

A medida que Avail se implementa usando [Substrato](https://substrate.io/), direcciones de Substrato genérico
 Siempre comienza con un 5 y sigue el **[formato de dirección SS58](https://docs.substrate.io/v3/advanced/ss58/)**.

:::

En la página de cuentas, haz clic en el botón **Agregar cuenta** y sigue los pasos en la ventana emergente.

<img src={useBaseUrl("img/avail/add-account.png")} width="100%" height="100%"/>

:::caution Gestión de Claves

La frase inicial es la clave de tu cuenta, que controla tu cuenta. No debes almacenar tu frase de clave en un dispositivo que tenga o pueda tener acceso a una conexión de Internet. La frase de la clave debe escribirse y almacenarse en un medio no digital n/a

Almacenar el archivo JSON de tus cuentas no tiene que ser tan rígido como almacenar la frase de la clave, siempre y cuando uses una contraseña fuerte para encriptar el archivo. Puedes importar el archivo JSON al acceso de tu cuenta.

:::

## Recibir los tokens de la red de prueba de AVL {#receive-avl-testnet-tokens}

En el Explorador de Avail, haz clic en el icono junto al nombre de tu cuenta para copiar tu dirección. Alternativamente, puedes copiar la dirección manualmente.

<img src={useBaseUrl("img/avail/account-icon.png")} width="100%" height="100%"/>

Dirígete al [faucet de Polygon](https://faucet.polygon.technology).

En la página de faucet, selecciona`DA Network`y`DA (Test Token)`como la red y el token.
 Pegar la dirección de tu cuenta y haz clic en **Enviar**. La transferencia tendrá un máximo de un minuto para completarse.

<img src={useBaseUrl("img/avail/faucet.png")} width="100%" height="100%"/>

Tras una transferencia exitosa, tu cuenta debería tener un saldo no cero. Si enfrentas cualquier problema como el de obtener tokens del faucet, por favor contacta a la [equipo de soporte](https://support.polygon.technology/support/home).

## Enviar una nueva transacción {#submit-a-new-transaction}

En el Explorador de Avail, navega a la pestaña **Desarrollador** y haz clic en la subpestaña **de** Extrínsecos.

<img src={useBaseUrl("img/avail/developer.png")} width="100%" height="100%"/>

Selecciona tu nueva cuenta creada.

<img src={useBaseUrl("img/avail/developer-account.png")} width="100%" height="100%"/>

Hay muchos extrínsecos para elegir; sigue adelante y selecciona el `dataAvailability`extrínseco desde el **menú desplegable extrínseco**.

:::info ¿Qué son los extrínsecos?

Los extrínsecos son una forma de información externa y pueden ser inherentes, a transacciones firmadas, o transacciones no firmadas. Más detalles sobre los extrínsecos están disponibles en la [Documentación de sustratos](https://docs.substrate.io/v3/concepts/extrinsics/).

:::

Luego puedes usar el menú desplegable en el lado derecho para crear una clave de aplicación o enviar datos.

<TabItem value="key"><Tabs
defaultValue="key"
values={[
{ label: 'Create an application key', value: 'key', },
{ label: 'Submit data', value: 'data', },
]
}>


En este ejemplo, `createApplicationKey`se utiliza para crear una clave de aplicación.

<img src={useBaseUrl("img/avail/da-app-key.png")} width="100%" height="100%"/>

Ingresa el valor que deseas enviar como parte de esta transacción usando`App_ID`o
 sin un valor de clave por defecto como`0`

<img src={useBaseUrl("img/avail/da-app-data.png")} width="100%" height="100%"/>

:::note

Antes de enviar una transacción utilizando`App_ID` debes crear utilizando el `createApplicationKey`campo.

:::

Envía la transacción. Dirígete al [Explorador Avail](https://testnet.polygonavail.net/#/explorer). La lista de eventos recientes debería enumerar tu transacción. Puedes hacer clic en el evento y expandirlo para comprobar los detalles de la transacción.

</TabItem>

<TabItem value="data">

En este ejemplo, `submitBlockLengthProposal`se utiliza para enviar datos.

<img src={useBaseUrl("img/avail/extrinsic-da.png")} width="100%" height="100%"/>

Ingresa los valores a los que deseas enviar como parte de esta transacción para`row` y `col`

<img src={useBaseUrl("img/avail/da-row-col.png")} width="100%" height="100%"/>

Envía la transacción. Dirígete al [Explorador Avail](https://testnet.polygonavail.net/#/explorer). La lista de eventos recientes debería enumerar tu transacción. Puedes hacer clic en el evento y expandirlo para comprobar los detalles de la transacción.

</TabItem>
</Tabs>

:::info ¿Cómo obtener garantías de que los datos detrás de la transacción están disponibles?

Hemos resumido la cantidad meollo de la verificación de la disponibilidad de datos y hemos alojado a un cliente ligero para tu uso. Todo lo que necesitas hacer es hacer clic en el número de bloque contra la transacción deseada y ver todos los detalles del bloque.

También verás un *factor de confianza*. Si se muestra`0%` dale algo de tiempo y vuelve a revisarlo más tarde. De lo contrario, debería mostrar un nivel de confianza no cero que indique la probabilidad con la que los datos subyacentes están disponibles.

:::

</TabItem>
<TabItem value="library">

Alternativamente, puedes utilizar la console/typescript para generar una cuenta de Avail vía[`@polkadot/api`](https://polkadot.js.org/docs/) Crea una nueva carpeta y añade la Biblioteca JS utilizando `yarn add @polkadot/api`o`npm install @polkadot/api`

:::info

Asegúrate de que se agreguen dependencias de Typescript para ejecutar el script. Aquí,`@polkadot/api`  versión`7.9.1`que se usa.

Puedes usar `ts-node`para ejecutar los archivos Typescript en la consola. Sea usar`yarn add ts-node typescript '@types/node'` o`npm i ts-node typescript '@types/node'` para instalar los paquetes.

Por ejemplo, si creas un script llamado`account.ts`, puedes ejecutar el script en la línea de comandos ejecutando:

```bash

ts-node account.ts

```

También tendrás que **[conectarte a un nodo](../node/avail-node-management.md)** antes de ejecutar los scripts.

:::

Para generar una cuenta, ejecuta el siguiente script:

```typescript

const { ApiPromise, WsProvider, Keyring } = require('@polkadot/api');
const {mnemonicGenerate, cryptoWaitReady } = require('@polkadot/util-crypto');

const keyring = new Keyring({ type: 'sr25519' });

async function createApi() {

  // Create the API and wait until ready
  return ApiPromise.create({
    types: {
        AccountInfo: 'AccountInfoWithRefCount',
    },
  });
}

async function main () {
  // Create the API and wait until ready
  const api = await createApi();

  const keyring = new Keyring({ type: 'sr25519'});
  const mnemonic = mnemonicGenerate();

  const pair = keyring.createFromUri(mnemonic, { name: 'test_pair' },'sr25519');
  console.log(pair.meta.name, 'has address', pair.address, 'and the mnemonic is', mnemonic);
  process.exit(0);

}
main().catch(console.error)

```

Resultado de la muestra:

```

test_pair has address 5Gq1hKAiSKFkdmcFjTt3U8KEaxDHp613hbdSmqJCRswMkwCB and the mnemonic is decrease lunar scatter pattern spoil alpha index trend vacant sorry scatter never

```

:::info Formato de dirección

A medida que Avail se implementa usando [Substrato](https://substrate.io/), direcciones de Substrato genérico
 Siempre comienza con un 5 y sigue el **[formato de dirección SS58](https://docs.substrate.io/v3/advanced/ss58/)**.

:::

:::info algoritmo de derivación de claves y firma

Las razones para usarlo`sr25519`se señalan **[aquí](https://wiki.polkadot.network/docs/learn-cryptography#keypairs-and-signing)**

:::

Guarda la dirección y la frase mnemónica recientemente generadas para los próximos pasos.

:::caution Gestión de Claves

La frase inicial es la clave de tu cuenta, que controla tu cuenta. No debes almacenar tu frase de clave en un dispositivo que tenga o pueda tener acceso a una conexión de Internet. La frase de la clave debe escribirse y almacenarse en un medio no digital n/a

:::

## Recibir los tokens de la red de prueba de AVL {#receive-avl-testnet-tokens-1}

Dirígete al [faucet de Polygon](https://faucet.polygon.technology).

En la página del grifo, selecciona `DA (Test Token)`y `DA Network`como el token y la red, respectivamente. Pegar la dirección de tu cuenta y haz clic en **Enviar**. La transferencia tomará hasta un minuto para completarse.

<img src={useBaseUrl("img/avail/faucet.png")} width="100%" height="100%"/>

Tras una transferencia exitosa, tu cuenta debería tener un saldo no cero. Si tienes problemas para obtener tokens del faucet, por favor contacta con el [equipo de soporte](https://support.polygon.technology/support/home).

### Balance Checar con`@polkadot/api`

Utilizando el siguiente script para comprobar el saldo de la cuenta que acabas de crear:

```typescript

const { ApiPromise, WsProvider, Keyring } = require('@polkadot/api');
const {mnemonicGenerate, cryptoWaitReady } = require('@polkadot/util-crypto');

import type { ISubmittableResult} from '@polkadot/types/types';

const keyring = new Keyring({ type: 'sr25519' });

async function createApi() {
  // Initialise the provider to connect to the local node
  const provider = new WsProvider('wss://testnet.polygonavail.net/ws');

  // Create the API and wait until ready
  return ApiPromise.create({
    provider,
    types: {
        DataLookup: {
          size: 'u32',
          index: 'Vec<(u32,u32)>'
        },
        KateExtrinsicRoot: {
          hash: 'Hash',
          commitment: 'Vec<u8>',
          rows: 'u16',
          cols: 'u16'
        },
        KateHeader: {
          parentHash: 'Hash',
          number: 'Compact<BlockNumber>',
          stateRoot: 'Hash',
          extrinsicsRoot: 'KateExtrinsicRoot',
          digest: 'Digest',
          app_data_lookup: 'DataLookup'
        },
        Header: 'KateHeader',
        AppId: 'u32',
        CheckAppId: {
            extra: {
                appId: 'u32',
            },
            types: {}
        }
    },
    signedExtensions: {
      CheckAppId: {
        extrinsic: {
          appId: 'u32'
        },
        payload: {}
      },
    },
  });
}

async function main () {
  // Create the API and wait until ready
  const api = await createApi();

  // Retrieve the chain & node information information via rpc calls
  const [chain, nodeName, nodeVersion] = await Promise.all([
    api.rpc.system.chain(),
    api.rpc.system.name(),
    api.rpc.system.version()
  ]);

  console.log(`You are connected to chain ${chain} using ${nodeName} v${nodeVersion}`);

    //address which is generated from previous step👇
    let ADDRESS = '_ADDRESS_';
    console.log(ADDRESS);
    try{
      let { data: { free:balance}} = await api.query.system.account(ADDRESS)
      console.log(`${ADDRESS} has balance of ${balance}`)
    }catch (e){
      console.log(e)  
    }finally{
      process.exit(0)
    }
}
main().catch(console.error)

```

Resultado de la muestra:

```
You are connected to chain Avail-Testnet using Polygon Avail Node v3.0.0-6c8781e-x86_64-linux-gnu
5HBCFfAs5gfqYgSinsr5s1nSZY2uRCh8MhYhXXp6Y9jNRJFB
5HBCFfAs5gfqYgSinsr5s1nSZY2uRCh8MhYhXXp6Y9jNRJFB has balance of 0
```

> Deberías obtener el saldo como `0`si la cuenta que has creado recientemente y no has utilizado el faucet. También deberías ver la confirmación de la transacción.

:::tip Utilizando El Explorador de Avail

Para mayor comodidad, puedes agregar la cuenta que generó con`@polkadot/api` en la interfaz de usuario del Explorador de Avail para realizar las acciones de la cuenta.

:::

## Enviar una nueva transacción {#submit-a-new-transaction-1}

Puedes utilizar los scripts proporcionados en esta sección para firmar y enviar acciones.

:::note

Remplace `value`y `APP_ID`por los que quieres enviar. Además, remplace la cadena mnemonic con tu propia.

:::

<TabItem value="key-script"><Tabs
defaultValue="key-script"
values={[
{ label: 'Create an application key', value: 'key-script', },
{ label: 'Submit data', value: 'data-script', },
]
}>


El siguiente script crea una clave de aplicación:

```typescript

const { ApiPromise, WsProvider, Keyring } = require('@polkadot/api');
const {mnemonicGenerate, cryptoWaitReady } = require('@polkadot/util-crypto');

import type { ISubmittableResult} from '@polkadot/types/types';

const ALICE = '5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY';
const BOB = '5FHneW46xGXgs5mUiveU4sbTyGBzmstUspZC92UhjJM694ty';

const keyring = new Keyring({ type: 'sr25519' });

async function createApi() {
  // Initialise the provider to connect to the local node
  const provider = new WsProvider('ws://127.0.0.1:9944');

  // Create the API and wait until ready
  return ApiPromise.create({
    provider,
    types: {
        DataLookup: {
          size: 'u32',
          index: 'Vec<(u32,u32)>'
        },
        KateExtrinsicRoot: {
          hash: 'Hash',
          commitment: 'Vec<u8>',
          rows: 'u16',
          cols: 'u16'
        },
        KateHeader: {
          parentHash: 'Hash',
          number: 'Compact<BlockNumber>',
          stateRoot: 'Hash',
          extrinsicsRoot: 'KateExtrinsicRoot',
          digest: 'Digest',
          app_data_lookup: 'DataLookup'
        },
        Header: 'KateHeader',
        AppId: 'u32',
        CheckAppId: {
            extra: {
                appId: 'u32',
            },
            types: {}
        }
    },
    signedExtensions: {
      CheckAppId: {
        extrinsic: {
          appId: 'u32'
        },
        payload: {}
      },
    },
  });
}

async function main () {
  // Create the API and wait until ready
  const api = await createApi();

  //enter your mnemonic generated from the previous step and replace below.
  const pair = keyring.addFromUri( 'put your mnemonic', { name: 'test pair' }, 'sr25519');
  // Retrieve the chain & node information information via rpc calls
  const [chain, nodeName, nodeVersion] = await Promise.all([
    api.rpc.system.chain(),
    api.rpc.system.name(),
    api.rpc.system.version()
  ]);
  console.log(`You are connected to chain ${chain} using ${nodeName} v${nodeVersion}`);
    try{
        let KEY = 1;
        let createId = api.tx.dataAvailability.createApplicationKey(KEY);
        const unsub = await createId
            .signAndSend(
            pair,
            { app_id: 0},
            ( result: ISubmittableResult ) => {
                console.log(`Tx status: ${result.status}`);

                if (result.status.isInBlock) {
                    console.log(`Tx included at block hash ${result.status.asInBlock}`);
                } else if (result.status.isFinalized) {
                    console.log(`Tx included at blockHash ${result.status.asFinalized}`);

                    result.events.forEach(({ phase, event: { data, method, section } }) => {
                        console.log(`\t' ${phase}: ${section}.${method}:: ${data}`);
                    });
                    unsub
                    process.exit(0);
                }
            });
    }catch(e){
        console.error(e);
    }
}
main().catch(console.error)

```

</TabItem>
<TabItem value="data-script">

El siguiente script envía datos:

```typescript

const { ApiPromise, WsProvider, Keyring } = require('@polkadot/api');
const {mnemonicGenerate, cryptoWaitReady } = require('@polkadot/util-crypto');

import type { EventRecord, ExtrinsicStatus, H256, SignedBlock } from '@polkadot/types/interfaces';
import type { ISubmittableResult} from '@polkadot/types/types';

const keyring = new Keyring({ type: 'sr25519' });

async function createApi() {
  // Initialise the provider to connect to the local node
  const provider = new WsProvider('wss://testnet.polygonavail.net/ws');

  // Create the API and wait until ready
  return ApiPromise.create({
    provider,
    types: {
        DataLookup: {
          size: 'u32',
          index: 'Vec<(u32,u32)>'
        },
        KateExtrinsicRoot: {
          hash: 'Hash',
          commitment: 'Vec<u8>',
          rows: 'u16',
          cols: 'u16'
        },
        KateHeader: {
          parentHash: 'Hash',
          number: 'Compact<BlockNumber>',
          stateRoot: 'Hash',
          extrinsicsRoot: 'KateExtrinsicRoot',
          digest: 'Digest',
          app_data_lookup: 'DataLookup'
        },
        Header: 'KateHeader',
        AppId: 'u32',
        CheckAppId: {
            extra: {
                appId: 'u32',
            },
            types: {}
        }
    },
    signedExtensions: {
      CheckAppId: {
        extrinsic: {
          appId: 'u32'
        },
        payload: {}
      },
    },
  });
}

async function main () {
  // Create the API and wait until ready
  const api = await createApi();

  //enter your mnemonic generated from the previous step and replace below 👇.
  const pair = keyring.addFromUri( 'enter mnemonic here', { name: 'test pair' }, 'sr25519');
  // Retrieve the chain & node information information via rpc calls
  const [chain, nodeName, nodeVersion] = await Promise.all([
    api.rpc.system.chain(),
    api.rpc.system.name(),
    api.rpc.system.version()
  ]);

  console.log(`You are connected to chain ${chain} using ${nodeName} v${nodeVersion}`);

    try{
        let APP_ID = 1;
        let VALUE = `iucakcbak`;
        let transfer = api.tx.dataAvailability.submitData(VALUE);
        const unsub = await transfer
            .signAndSend(
            pair,
            { app_id: APP_ID},
            ( result: ISubmittableResult ) => {
                console.log(`Tx status: ${result.status}`);

                if (result.status.isInBlock) {
                    console.log(`Tx included at block hash ${result.status.asInBlock}`);
                } else if (result.status.isFinalized) {
                    console.log(`Tx included at blockHash ${result.status.asFinalized}`);

                    result.events.forEach(({ phase, event: { data, method, section } }) => {
                        console.log(`\t' ${phase}: ${section}.${method}:: ${data}`);
                    });

                    process.exit(0);
                }
            });
    }catch(e){
        console.error(e);
    }
}
main().catch(console.error)

```

</TabItem>
</Tabs>

Puedes dirigirte al [Explorador Avail](https://testnet.polygonavail.net/#/explorer), y al la lista de eventos recientes debería enumerar tu transacción. Puedes hacer clic en el evento y expandirlo para comprobar los detalles de la transacción.

:::info ¿Cómo obtener garantías de que los datos detrás de la transacción están disponibles?

Puedes utilizar la siguiente solicitud de bucle para ver el nivel de confianza. Solo tienes que sustituir el número de bloque con el que deseas obtener las garantías de disponibilidad

```bash

curl -s -H 'Content-Type: application/json' -d '{"jsonrpc":"2.0","method":"get_blockConfidence","params": {"number": block_number_here}, "id": 1}' 'https://polygon-da-light.matic.today/v1/json-rpc'

```
:::

</TabItem>
</Tabs>
