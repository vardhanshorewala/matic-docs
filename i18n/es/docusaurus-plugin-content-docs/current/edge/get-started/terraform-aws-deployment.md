---
id: terraform-aws-deployment
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - deployment
  - terraform
  - aws
  - script
---
:::info



:::

:::info

:::



##  {#prerequisites}

###  {#system-tools}
*
*
*

###  {#terraform-variables}


*
*
*

##  {#deployment-information}
###  {#deployed-resources}


*
*
*
*
*
*
*

###  {#fault-tolerance}





###  {#command-line-access}



###  {#base-ami-upgrade}






```shell
terraform taint module.instances[0].aws_instance.polygon_edge_instance
terraform taint module.instances[1].aws_instance.polygon_edge_instance
terraform taint module.instances[2].aws_instance.polygon_edge_instance
terraform taint module.instances[3].aws_instance.polygon_edge_instance
terraform apply
```

:::info

:::

##  {#deployment-procedure}

###  {#pre-deployment-steps}
*
*
*
*
*
*

####  {#example}
```terraform
module "polygon-edge" {
  source  = "aws-ia/polygon-technology-edge/aws"
  version = ">=0.0.1"

  account_id          = var.account_id
  premine             = var.premine
  alb_ssl_certificate = var.alb_ssl_certificate
}

output "json_rpc_dns_name" {
  value       = module.polygon-edge.jsonrpc_dns_name
  description = "The dns name for the JSON-RPC API"
}

variable "account_id" {
  type        = string
  description = "Your AWS Account ID"
}

variable "premine" {
  type        = string
  description = "Public account that will receive premined native currency"
}

variable "alb_ssl_certificate" {
  type        = string
  description = "The ARN of SSL certificate that will be placed on JSON-RPC ALB"
}
```

####  {#example-1}
```terraform
account_id          = "123456789"
premine             = "0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF"
alb_ssl_certificate = "arn:aws:acm:us-west-2:123456789:certificate/64c7f117-61f5-435e-878b-83186676a8af"
```

###  {#deployment-steps}
*
*



:::
*
*

###  {#post-deployment-steps}
*
*
  ```shell
  # BIND syntax
  # NAME                            TTL       CLASS   TYPE      CANONICAL NAME
  rpc.my-awsome-blockchain.com.               IN      CNAME     jrpc-202208123456879-123456789.us-west-2.elb.amazonaws.com.
  ```
*
  ```shell
    curl  https://rpc.my-awsome-blockchain.com -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_chainId","params":[],"id":1}'
  ```

##  {#destroy-procedure}
:::warning

:::


