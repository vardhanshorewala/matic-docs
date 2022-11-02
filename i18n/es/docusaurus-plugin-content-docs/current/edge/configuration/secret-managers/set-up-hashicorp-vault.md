---
id: set-up-hashicorp-vault
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - hashicorp
  - vault
  - secrets
  - manager
---

##  {#overview}


*
*

:::warning

:::











:::info

:::


##  {#prerequisites}






*
*

##  {#step-1-generate-the-secrets-manager-configuration}





```bash
polygon-edge secrets generate --dir <PATH> --token <TOKEN> --server-url <SERVER_URL> --name <NODE_NAME>
```


*
*
*
*

:::caution





:::

##  {#step-2-initialize-secret-keys-using-the-configuration}



```bash
polygon-edge secrets init --config <PATH>
```



##  {#step-3-generate-the-genesis-file}




```bash
polygon-edge genesis --ibft-validator <VALIDATOR_ADDRESS> ...
```

##  {#step-4-start-the-polygon-edge-client}




```bash
polygon-edge server --secrets-config <PATH> ...
```

