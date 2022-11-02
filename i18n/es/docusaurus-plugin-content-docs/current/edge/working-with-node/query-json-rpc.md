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

Este ejemplo cubre el uso de herramientas como **curl** to query information, as well as starting the chain with a premined account,


##  {#step-1-create-a-genesis-file-with-a-premined-account}


````bash
polygon-edge genesis --premine 0x1010101010101010101010101010101010101010
````




````bash
polygon-edge genesis --premine 0x1010101010101010101010101010101010101010:0x123123
````



:::warning

:::

##  {#step-2-start-the-polygon-edge-in-dev-mode}


````bash
polygon-edge server --chain genesis.json --dev --log-level debug
````

##  {#step-3-query-the-account-balance}


````bash
curl -X POST --data '{"jsonrpc":"2.0","method":"eth_getBalance","params":["0x1010101010101010101010101010101010101010", "latest"],"id":1}' localhost:8545
````


````bash
{
  "id":1,
  "result":"0x100000000000000000000000000"
}
````

##  {#step-4-send-a-transfer-transaction}



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
