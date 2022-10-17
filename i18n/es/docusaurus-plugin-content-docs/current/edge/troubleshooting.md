---
id: troubleshooting
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - troubleshooting

---

#  {#troubleshooting}

##  {#error}



1.

````bash
genesis [--chain-id CHAIN_ID]
````
2.


##  {#how-to-get-a-websocket-url}




````bash
ws://<JSON-RPC URL>:<PORT>/ws
````



````bash
wss://rpc-edgenet.polygon.technology/ws
````

##  {#error-when-trying-to-deploy-a-contract}


````bash
genesis --premine 0x3956E90e632AEbBF34DEB49b71c28A83Bc029862:1000000000000000000000
````



##  {#erc20-tokens-not-released-while-using-chainbridge}



##  {#error-when-using-chainbridge}


````bash
 $ cb-sol-cli admin set-fee --bridge <BRIDGE_ADDRESS> --fee 0 --url <JSON_RPC_URL> --privateKey <PRIVATE_KEY>
 ````






