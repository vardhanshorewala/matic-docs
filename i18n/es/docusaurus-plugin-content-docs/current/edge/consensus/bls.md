---
id: bls
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - bls
---

##  {#overview}



##  {#how-to-setup-a-new-chain-using-bls}



##  {#how-to-migrate-from-an-existing-ecdsa-poa-chain-to-bls-poa-chain}



1.
2.
3.
4.

###  {#1-stop-all-nodes}



###  {#2-generate-the-bls-key}



```bash
polygon-edge secrets init --bls --ecdsa=false --network=false

[SECRETS INIT]
Public key (address) = 0x...
BLS Public key       = 0x...
Node ID              = 16...
```

###  {#3-add-fork-setting}







```bash
polygon-edge ibft switch --chain ./genesis.json --type PoA --ibft-validator-type bls --ibft-validators-prefix-path test-chain- --from 100
```

###  {#4-restart-all-nodes}



```bash
2022-09-02T11:45:24.535+0300 [INFO]  polygon.ibft: IBFT validation type switched: old=ecdsa new=bls
```



```
2022-09-02T11:45:28.728+0300 [INFO]  polygon.ibft: block committed: number=101 hash=0x5f33aa8cea4e849807ca5e350cb79f603a0d69a39f792e782f48d3ea57ac46ca validation_type=bls validators=3 committed=3
```

##  {#how-to-migrate-from-an-existing-ecdsa-pos-chain-to-a-bls-pos-chain}



1.
2.
3.
4.
5.

###  {#1-stop-all-nodes-1}



###  {#2-generate-the-bls-key-1}



```bash
polygon-edge secrets init --bls --ecdsa=false --network=false

[SECRETS INIT]
Public key (address) = 0x...
BLS Public key       = 0x...
Node ID              = 16...
```

###  {#3-add-fork-setting-1}





```bash
polygon-edge ibft switch --chain ./genesis.json --type PoS --ibft-validator-type bls --deployment 50 --from 200
```

###  {#4-register-bls-public-key-in-staking-contract}







```env
JSONRPC_URL=http://localhost:10002
STAKING_CONTRACT_ADDRESS=0x0000000000000000000000000000000000001001
PRIVATE_KEYS=0x...
BLS_PUBLIC_KEY=0x...
```



```bash
npm run register-blskey
```

:::warning

:::

###  {#5-restart-all-nodes}

