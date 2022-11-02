---
id: full-node-binaries
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

<Tabs
defaultValue="mainnet"
values={[
{ label: 'Polygon-Mainnet', value: 'mainnet', },
{ label: 'Mumbai-Testnet', value: 'mumbai', },
]
}>

<TabItem value="mumbai">





:::note







:::


##  {#prerequisites}

-
-
-
- `sudo apt-get install build-essential`
-

<!-- ### To install

```bash wget https://gist.githubusercontent.com/ssandeep/a6c7197811c83c71e5fead841bab396c/raw/go-install.sh
```

```bash
go-install.sh
```

```bash
sudo ln -nfs ~/.go/bin/go /usr/bin/go
``` -->

<!-- RabbitMQ installed on both the Full Node machines. See Downloading and Installing RabbitMQ. -->

##  {#overview}

-
-
-
-
-
-

:::note

:::


###  {#install-build-essentials}

```bash
sudo apt-get install build-essential
```

###

```bash
wget https://raw.githubusercontent.com/maticnetwork/node-ansible/master/go-install.sh
bash go-install.sh
sudo ln -nfs ~/.go/bin/go /usr/bin/go
```

>

###  {#rabbitmq}









```bash
rabbitmq-server
```

##  {#install-binaries}

###  {#heimdall}



```bash
cd ~/
git clone https://github.com/maticnetwork/heimdall
cd heimdall

# Checkout to a proper version
# For eg: git checkout v0.2.1-mumbai
git checkout <TAG OR BRANCH>
make install
```



```bash
heimdalld version --long
```

###  {#bor}



```bash
cd ~/
git clone https://github.com/maticnetwork/bor
cd bor

# Checkout to a proper version

# For eg: git checkout v0.2.16

git checkout <TAG OR BRANCH>
make bor-all
sudo ln -nfs ~/bor/build/bin/bor /usr/bin/bor
sudo ln -nfs ~/bor/build/bin/bootnode /usr/bin/bootnode
```



```bash
bor version
```

##  {#set-up-node-files}

###  {#fetch-launch-repo}

```bash
cd ~/
git clone https://github.com/maticnetwork/launch
```

###  {#set-up-launch-directory}







```bash
cd ~/
mkdir -p node
cp -rf launch/<network-name>/sentry/<node-type>/* ~/node

# To setup sentry node for mumbai (testnet-v4) testnet
# cp -rf launch/testnet-v4/sentry/sentry/* ~/node
```

###  {#configure-network-directories}



```bash
cd ~/node/heimdall
bash setup.sh
```



```bash
cd ~/node/bor
bash setup.sh
```

##  {#configure-service-files}



```bash
cd ~/node
wget https://raw.githubusercontent.com/maticnetwork/launch/master/<network-name>/service.sh
# To setup sentry node for mumbai (testnet-v4) testnet
# wget https://raw.githubusercontent.com/maticnetwork/launch/master/testnet-v4/service.sh
```


```bash
sudo mkdir -p /etc/matic
sudo chmod -R 777 /etc/matic/
touch /etc/matic/metadata
```



```bash
cd ~/node
bash service.sh
sudo cp *.service /etc/systemd/system/
```

##  {#set-up-configuration-files}



-
    - `moniker=<enter unique identifier>`

```js
 seeds="4cd60c1d76e44b05f7dfd8bab3f447b119e87042@54.147.31.250:26656,b18bbe1f3d8576f4b73d9b18976e71c65e839149@34.226.134.117:26656"
```
-

    ```js
    eth_rpc_url =<insert Infura or any full node RPC URL to Goerli>
    ```

-

```bash
--bootnodes "enode://320553cda00dfc003f499a3ce9598029f364fbb3ed1222fdc20a94d97dcc4d8ba0cd0bfa996579dcc6d17a534741fb0a5da303a90579431259150de66b597251@54.147.31.250:30303"
```

##  {#start-services}



```bash
sudo service heimdalld start
sudo service heimdalld-rest-server start
```



```bash
sudo service bor start
```

##  {#logs}





```bash
journalctl -u heimdalld.service -f
```



```bash
journalctl -u heimdalld-rest-server.service -f
```



```bash
journalctl -u bor.service -f
```

###  {#to-check-if-heimdall-is-synced}

1.
2.

###






</TabItem>

<TabItem value="mainnet">





:::note







:::


##  {#prerequisites-1}

-
-
-

```bash
sudo apt-get install build-essential
- Go 1.18 installed.

## Overview

- Have the machine prepared.
- Install the Heimdall and Bor binaries on the Full Node machine.
- Set up the Heimdall and Bor services on the Full Node machine.
- Configure the Full node.
- Start the Full node.
- Check node health with the community.

:::note
You have to follow the exact outlined sequence of actions, otherwise you will run into issues.
:::

### Install build essentials

***This is required for your full node***

```bash
sudo apt-get install build-essential
```

###  {#install-go}



```bash
wget https://raw.githubusercontent.com/maticnetwork/node-ansible/master/go-install.sh
bash go-install.sh
sudo ln -nfs ~/.go/bin/go /usr/bin/go
```

>

##  {#install-binaries-1}

###  {#heimdall-1}




1.
    *
    *
2.



```
Data - "abcd1234"
Length in string format - 8
Hex Byte representation - [171 205 18 52]
Length in byte format - 4
```



```bash
cd ~/
git clone https://github.com/maticnetwork/heimdall
cd heimdall

# Checkout to a proper version
# For eg: git checkout v0.2.11-mainnet
git checkout <TAG OR BRANCH>
make install
```



```bash
heimdalld version --long
```

###  {#bor-1}





```bash
cd ~/
git clone https://github.com/maticnetwork/bor
cd bor

# Checkout to a proper version

# For eg: git checkout 0.2.16

git checkout <TAG OR BRANCH>
make bor-all
sudo ln -nfs ~/bor/build/bin/bor /usr/bin/bor
sudo ln -nfs ~/bor/build/bin/bootnode /usr/bin/bootnode
```



```bash
bor version
```

##  {#configure-node-files}

###  {#fetch-launch-repo-1}

```bash
cd ~/
git clone https://github.com/maticnetwork/launch
```

###  {#configure-launch-directory}







```bash
cd ~/
mkdir -p node
cp -rf launch/<network-name>/sentry/<node-type>/* ~/node

# To setup sentry node for Polygon mainnet
# cp -rf launch/mainnet-v1/sentry/sentry/* ~/node
```

###  {#configure-network-directories-1}



```bash
cd ~/node/heimdall
bash setup.sh
```



```bash
cd ~/node/bor
bash setup.sh
```

##  {#configure-service-files-1}



```bash
cd ~/node
wget https://raw.githubusercontent.com/maticnetwork/launch/master/<network-name>/service.sh
# To setup sentry node for mainnet (mainnet-v1)
# wget https://raw.githubusercontent.com/maticnetwork/launch/master/mainnet-v1/service.sh
```



```bash
sudo mkdir -p /etc/matic
sudo chmod -R 777 /etc/matic/
touch /etc/matic/metadata
```



```bash
cd ~/node
bash service.sh
sudo cp *.service /etc/systemd/system/
```



##  {#set-up-config-files}

-
-



    ```jsx
    moniker=<enter unique identifier> For example, moniker=my-sentry-node
    ```

    ```jsx
    seeds="f4f605d60b8ffaaf15240564e58a81103510631c@159.203.9.164:26656,4fb1bc820088764a564d4f66bba1963d47d82329@44.232.55.71:26656"
    ```

    -
    -
    -



-

```bash
--bootnodes "enode://0cb82b395094ee4a2915e9714894627de9ed8498fb881cec6db7c65e8b9a5bd7f2f25cc84e71e89d0947e51c76e85d0847de848c7782b13c0255247a6758178c@44.232.55.71:30303,enode://88116f4295f5a31538ae409e4d44ad40d22e44ee9342869e7d68bdec55b0f83c1530355ce8b41fbec0928a7d75a5745d528450d30aec92066ab6ba1ee351d710@159.203.9.164:30303"
```



```jsx
--gcmode 'archive' \
--ws --ws.port 8546 --ws.addr 0.0.0.0 --ws.origins '*' \
```

##  {#start-services-1}





```jsx
sudo service heimdalld start
```



```jsx
sudo service heimdalld-rest-server start
```



-
-



-
    -
    -



```jsx
sudo service bor start
```



-




</TabItem>

</Tabs>
