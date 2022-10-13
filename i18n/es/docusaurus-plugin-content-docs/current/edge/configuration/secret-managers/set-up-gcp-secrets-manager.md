---
id: set-up-gcp-secrets-manager
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - gcp
  - secrets
  - manager
---

##  {#overview}


*
*











:::info

:::


##  {#prerequisites}
###  {#gcp-billing-account}


###  {#secrets-manager-api}


###  {#gcp-credentials}



*
*

##  {#step-1-generate-the-secrets-manager-configuration}





```bash
polygon-edge secrets generate --type gcp-ssm --dir <PATH> --name <NODE_NAME> --extra project-id=<PROJECT_ID>,gcp-ssm-cred=<GCP_CREDS_FILE>
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

