---
id: full-node-deployment
title:
description:

keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import useBaseUrl from '@docusaurus/useBaseUrl';

<TabItem value="mumbai"><Tabs
defaultValue="mainnet"
values={[
{ label: 'Polygon-Mainnet', value: 'mainnet', },
{ label: 'Polygon-Testnet', value: 'mumbai', },
]
}>


##  {#full-node-deployment-mumbai-testnet}





-
    -
-
-
-
-

```bash
Data - "abcd1234"
Length in string format - 8
Hex Byte representation - [171 205 18 52]
Length in byte format - 4

```

##  {#full-node-setup-for-testnetv4-mumbai-testnet}

-
-
-
-
-
-

```bash

ansible-playbook -l sentry playbooks/network.yml --extra-var="bor_branch=v0.2.16 heimdall_branch=v0.2.11 network_version=testnet-v4 node_type=sentry/sentry heimdall_network=mumbai" --list-hosts

```



<img src={useBaseUrl("img/network/full-node-mumbai.png")} />

-

```bash

    ansible-playbook -l sentry playbooks/network.yml --extra-var="bor_branch=v0.2.16 heimdall_branch=v0.2.11 network_version=testnet-v4 node_type=sentry/sentry heimdall_network=mumbai"

```

-

`ansible-playbook -l sentry playbooks/clean.yml`

-
-
    - `moniker=<enter unique identifier>`
    - `seeds="4cd60c1d76e44b05f7dfd8bab3f447b119e87042@54.147.31.250:26656"`
-
    - `eth_rpc_url =<insert Infura or any full node RPC URL to Goerli>`
-

```bash
--bootnodes "enode://320553cda00dfc003f499a3ce9598029f364fbb3ed1222fdc20a94d97dcc4d8ba0cd0bfa996579dcc6d17a534741fb0a5da303a90579431259150de66b597251@54.147.31.250:30303"
```

-
    - `--gcmode 'archive'`

-
    - `sudo service heimdalld start`
    - `sudo service heimdalld-rest-server start`



    - `sudo service bor start`

-
    -
    -
    -

-
    -
    -

</TabItem>
<TabItem value="mainnet">

##  {#full-node-deployment-polygon-mainnet}





-
    -
-
-
-
-

```bash

Data - "abcd1234"
Length in string format - 8
Hex Byte representation - [171 205 18 52]
Length in byte format - 4
```

##  {#full-node-set-up-for-polygon-mainnet}

-
-
- `cd node-ansible`
-
-
-

```bash
ansible-playbook -l sentry playbooks/network.yml --extra-var="bor_branch=v0.2.16 heimdall_branch=v0.2.11 network_version=mainnet-v1 node_type=sentry/sentry heimdall_network=mainnet" --list-hosts
```



<img src={useBaseUrl("img/network/full-node-mainnet.png")} />


-


`ansible-playbook -l sentry playbooks/network.yml --extra-var="bor_branch=v0.2.16 heimdall_branch=v0.2.11 network_version=mainnet-v1 node_type=sentry/sentry heimdall_network=mainnet"`

-

`ansible-playbook -l sentry playbooks/clean.yml`

-
-
    - `moniker=<enter unique identifier>`
    - `seeds="f4f605d60b8ffaaf15240564e58a81103510631c@159.203.9.164:26656,4fb1bc820088764a564d4f66bba1963d47d82329@44.232.55.71:26656,2eadba4be3ce47ac8db0a3538cb923b57b41c927@35.199.4.13:26656,3b23b20017a6f348d329c102ddc0088f0a10a444@35.221.13.28:26656,25f5f65a09c56e9f1d2d90618aa70cd358aa68da@35.230.116.151:26656"`
-
    - `eth_rpc_url =<insert Infura or any full node RPC URL to Ethereum>`
-

```bash
--bootnodes "enode://0cb82b395094ee4a2915e9714894627de9ed8498fb881cec6db7c65e8b9a5bd7f2f25cc84e71e89d0947e51c76e85d0847de848c7782b13c0255247a6758178c@44.232.55.71:30303,enode://88116f4295f5a31538ae409e4d44ad40d22e44ee9342869e7d68bdec55b0f83c1530355ce8b41fbec0928a7d75a5745d528450d30aec92066ab6ba1ee351d710@159.203.9.164:30303"
```

-
    - `--gcmode 'archive'`

-
    - `sudo service heimdalld start`
    - `sudo service heimdalld-rest-server start`



    - `sudo service bor start`

-
    -
    -
    -

-
    -
    -

</TabItem>
</Tabs>
