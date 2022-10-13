---
id: set-up-aws-ssm
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - aws
  - ssm
  - secrets
  - manager
---

##  {#overview}


*
*











:::info

:::


##  {#prerequisites}
###  {#iam-policy}

```json
{
  "Version": "2012-10-17",
  "Statement" : [
    {
      "Effect" : "Allow",
      "Action" : [
        "ssm:PutParameter",
        "ssm:DeleteParameter",
        "ssm:GetParameter"
      ],
      "Resource" : [
        "arn:aws:ssm:<aws_region>:<aws_account_id>:parameter<ssm-parameter-path>*"
      ]
    }
  ]
}
```



*
*

##  {#step-1-generate-the-secrets-manager-configuration}





```bash
polygon-edge secrets generate --type aws-ssm --dir <PATH> --name <NODE_NAME> --extra region=<REGION>,ssm-parameter-path=<SSM_PARAM_PATH>
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



:::info

:::

##  {#step-3-generate-the-genesis-file}




```bash
polygon-edge genesis --ibft-validator <VALIDATOR_ADDRESS> ...
```

##  {#step-4-start-the-polygon-edge-client}




```bash
polygon-edge server --secrets-config <PATH> ...
```

