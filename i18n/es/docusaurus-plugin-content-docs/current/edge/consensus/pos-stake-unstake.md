---
id: pos-stake-unstake
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - stake
  - unstake
  - validator
  - epoch
---

##  {#overview}







##  {#staking-smart-contract}





##  {#setting-up-an-n-node-cluster}







```bash
polygon-edge genesis --pos ...
```

##  {#setting-the-length-of-an-epoch}





```bash
polygon-edge genesis --epoch-size 50
```





:::info





:::

##  {#using-the-staking-smart-contract-scripts}

###  {#prerequisites}





```bash
npm install
````

###  {#setting-up-the-provided-helper-scripts}





```bash
JSONRPC_URL=http://localhost:10002
PRIVATE_KEYS=0x0454f3ec51e7d6971fc345998bb2ba483a8d9d30d46ad890434e6f88ecb97544
STAKING_CONTRACT_ADDRESS=0x0000000000000000000000000000000000001001
BLS_PUBLIC_KEY=0xa..
```



*
*
*
*

###  {#staking-funds}

:::info





:::









```bash
npm run stake
```





:::info




```bash
npm run register-blskey
```
:::

###  {#unstaking-funds}





```bash
npm run unstake
```

###  {#fetching-the-list-of-stakers}





```bash
npm run info
```
