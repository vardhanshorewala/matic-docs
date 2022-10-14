---
id: query-json-rpc
title: Consulta terminales JSON RPC
description: "Consulta datos e inicia la cadena con una cuenta preacuñada."
keywords:
  - docs
  - polygon
  - edge
  - query
  - premine
  - node
---

## Resumen {#overview}

La capa JSON-RPC de Polygon Edge proporciona a los desarrolladores con la funcionalidad de interactuar fácilmente con la cadena de bloques a través de solicitudes HTTP.

Este ejemplo cubre el uso de herramientas como un **Curl** para consultar información, así como iniciar la cadena con una cuenta preacuñada,
 y enviar una transacción.

## Paso 1: Crear un archivo génesis con una cuenta preacuñada {#step-1-create-a-genesis-file-with-a-premined-account}

Para generar un archivo de génesis, ejecutar el siguiente comando:
````bash
polygon-edge genesis --premine 0x1010101010101010101010101010101010101010
````

El indicador **premine** establece la dirección que debe incluirse con un saldo inicial en el archivo **genesis**<br />
 En este caso, la dirección`0x1010101010101010101010101010101010101010` tendrá un saldo inicial **por defecto** de
`0x3635C9ADC5DEA00000 wei`  

Si quisiéramos especificar un saldo, podemos separar el saldo y la dirección con un`:`, me gusta:
````bash
polygon-edge genesis --premine 0x1010101010101010101010101010101010101010:0x123123
````

El saldo puede ser un`hex` o`uint256` valor.

:::warning ¡Solo cuentas preacuñadas para las cuales tienes una clave privada!
Si preacuñas cuentas y no tienes una clave privada para acceder a ellas, tu saldo preacuñado no será utilizable
:::

## Paso 2: Iniciar el Polygon Edge en modo dev  {#step-2-start-the-polygon-edge-in-dev-mode}

Para iniciar Polygon Edge en modo de desarrollo, que se explica en la sección de los [Comandos CLI](/docs/edge/get-started/cli-commands)
 ejecutar lo siguiente:
````bash
polygon-edge server --chain genesis.json --dev --log-level debug
````

## Paso 3: Consulta el saldo de la cuenta {#step-3-query-the-account-balance}

Ahora que el cliente está instalado y funcionando en modo dev, usando el archivo de génesis generado en el **Paso 1**, podemos usar una herramienta como
 **Curl** para consultar el saldo de la cuenta:
````bash
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0x1010101010101010101010101010101010101010", "latest"],"id":1}' localhost:8545
````

El comando debe regresar la siguiente salida:
````bash
{
  "id":1,
  "result":"0x100000000000000000000000000"
}
````

## Paso 4: Enviar una transacción de transferencia {#step-4-send-a-transfer-transaction}

Ahora que hemos confirmado que la cuenta que configuramos como preacuñada tiene el saldo correcto, podemos transferir algún ether:

````js
var Web3 = require("web3");

const web3 = new Web3("<provider's websocket jsonrpc address>"); //example: ws://localhost:10002/ws
web3.eth.accounts
  .signTransaction(
    {
      to: "<recipient address>",
      value: web3.utils.toWei("<value in ETH>"),
      gas: 21000,
    },
    "<private key from premined account>"
  )
  .then((signedTxData) => {
    web3.eth
      .sendSignedTransaction(signedTxData.rawTransaction)
      .on("receipt", console.log);
  });

````
