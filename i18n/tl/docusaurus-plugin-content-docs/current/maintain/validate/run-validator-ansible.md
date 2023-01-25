---
id: run-validator-ansible
title: Patakbuhin ang Validator Node gamit ang Ansible
description: "Gamitin ang Ansible para i-set up ang validator node mo."
keywords:
  - docs
  - matic
  - polygon
  - ansible
  - node
  - validator
  - sentry
slug: run-validator-ansible
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

:::tip

Kabilang sa mga hakbang sa gabay na ito ang paghihintay na ganap na mag-sync ang mga serbisyo ng **Heimdall** and **Bor**.
Tumatagal nang ilang araw para makumpleto ang prosesong ito. Bilang alternatibo, puwede kang gumamit ng isang maintained snapshot, na babawasan ang tagal ng pag-sync nang ilang oras. Para sa mga detalyadong tagubilin, tingnan ang [<ins>Mga Tagubilin para sa Snapshot para sa Heimdall at Bor</ins>](../../develop/network-details/snapshot-instructions-heimdall-bor).

Para sa mga download link ng snapshot, tingnan ang [Polygon Chains Snapshots](https://snapshots.matic.today/).

May limitadong espasyo para sa pagtanggap ng mga bagong validator. Makakasali lang ang mga bagong validator sa active na set kapag nag-unbond ang isang kasalukuyang active na validator.

:::

Ginagabayan ka ng seksyong ito sa pagsisimula at pagpapatakbo ng validator node sa pamamagitan ng Ansible playbook.

Para sa mga kinakailangan ng system, tingnan ang [Validator Node System Requirements](validator-node-system-requirements).

Kung gusto mong mag-start at mag-run ang validator node mula sa mga binary, tingnan ang [Mag-run ng Validator Node mula sa mga Binary](run-validator-binaries).

## Mga Prerequisite {#prerequisites}

* Tatlong machine—isang local machine kung saan papatakbuhin mo ang Ansible playbook; dalawang remote machine—isang [sentry](../glossary#sentry) at isang [validator](../glossary#validator).
* Sa local machine, naka-install ang [Ansible](https://www.ansible.com/).
* Sa local machine, naka-install ang [Python 3.x](https://www.python.org/downloads/).
* Sa mga remote machine, tiyaking *hindi* naka-install ang Go.
* Sa mga remote machine, nasa mga remote machine ang pampublikong key ng SSH ng local machine mo para magbigay-daan sa Ansible na kumonekta sa mga ito.
* May available kaming Bloxroute bilang relay network. Kung kailangan mo ng gateway na idadagdag bilang Trusted Peer mo, makipag-ugnayan sa [Delroy on Discord](http://delroy/#0056).


## Pangkalahatang-ideya {#overview}

Para magkaroon ng tumatakbong validator node, gawin ang sumusunod:

1. Ihanda ang tatlong machine.
1. I-set up ang sentry node gamit ang Ansible.
1. I-set up ang validator node gamit ang Ansible.
1. I-configure ang sentry node.
1. I-start ang sentry node.
1. I-configure ang validator node.
1. I-set ang key ng may-ari at key ng signer.
1. I-start ang validator node.
1. I-check ang kalusugan ng node sa tulong ng komunidad.

:::note

Dapat mong sundin ang **tumpak na naka-outline na pagkakasunod-sunod ng mga aksyon**, kung hindi ay magkakaroon ka sa mga isyu.

Halimbawa, kailangang naka-set up palagi ang sentry node bago ang validator node.

:::

## I-set up ang sentry node {#set-up-the-sentry-node}

Sa local machine mo, i-clone ang [node-ansible repository](https://github.com/maticnetwork/node-ansible):

```sh
git clone https://github.com/maticnetwork/node-ansible
```

Palitan ng na-clone na repository:

```sh
cd node-ansible
```

Ilagay ang mga IP address ng mga remote machine na gagawing sentry node at validator node sa `inventory.yml` file.

```yml
all:
  hosts:
  children:
    sentry:
      hosts:
        xxx.xxx.xx.xx: # <----- Add IP for sentry node
        xxx.xxx.xx.xx: # <----- Add IP for second sentry node (optional)
    validator:
      hosts:
        xxx.xxx.xx.xx: # <----- Add IP for validator node
```

Halimbawa:

```yml
all:
  hosts:
  children:
    sentry:
      hosts:
        188.166.216.25:
    validator:
      hosts:
        134.209.100.175:
```

I-check kung nakakagawa ng koneksyon sa remote sentry machine. Sa local machine, i-run ang:

```sh
$ ansible sentry -m ping
```

Ganito dapat ang makuha mong output:

```sh
xxx.xxx.xx.xx | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

I-test run ang set up ng sentry node:

```sh
ansible-playbook -l sentry playbooks/network.yml --extra-var="bor_branch=v0.2.16 heimdall_branch=v0.2.11  network_version=mainnet-v1 node_type=sentry/sentry heimdall_network=mainnet" --list-hosts
```

Ganito ang magiging output:

```sh
playbook: playbooks/network.yml
  pattern: ['all']
  host (1):
    xx.xxx.x.xxx
```

I-run ang setup ng sentry node nang may sudo priviledges:

```sh
ansible-playbook -l sentry playbooks/network.yml --extra-var="bor_branch=v0.2.16 heimdall_branch=v0.2.11  network_version=mainnet-v1 node_type=sentry/sentry heimdall_network=mainnet" --ask-become-pass
```

Kapag kumpleto na ang pag-setup, may makikita kang mensahe sa terminal na kumpleto na ito.

:::note

Kung magkakaroon ka ng issue at gustong mong simulan ulit, i-run ang:

```sh
ansible-playbook -l sentry playbooks/clean.yml
```

:::

## I-set up ang validator node {#set-up-the-validator-node}

Sa puntong ito, naka-set up na ang sentry node mo.

Sa local machine mo, mayroon ka ring Ansible playbook na naka-set up para patakbuhin ang validator node setup.

I-check kung nakakagawa ng koneksyon sa remote validator machine. Sa local machine, i-run ang `ansible validator -m ping`:

```sh
$ ansible validator -m ping
```

Ganito dapat ang makuha mong output:

```sh
xxx.xxx.xx.xx | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```

I-test run ang set up ng validator node:

```sh
ansible-playbook -l validator playbooks/network.yml --extra-var="bor_branch=v0.2.16 heimdall_branch=v0.2.11 network_version=mainnet-v1 node_type=sentry/validator heimdall_network=mainnet" --list-hosts
```

Ganito dapat ang makuha mong output:

```sh
playbook: playbooks/network.yml
  pattern: ['all']
  host (1):
    xx.xxx.x.xxx
```

I-run ang setup ng validator node nang may sudo priviledges:

```sh
ansible-playbook -l validator playbooks/network.yml --extra-var="bor_branch=v0.2.16 heimdall_branch=v0.2.11  network_version=mainnet-v1 node_type=sentry/validator heimdall_network=mainnet" --ask-become-pass
```

Kapag kumpleto na ang pag-setup, may makikita kang mensahe sa terminal na kumpleto na ito.

:::note

Kung magkakaroon ka ng issue at gustong mong simulan ulit, i-run ang:

```sh
ansible-playbook -l validator playbooks/clean.yml
```

:::

## I-configure ang sentry node {#configure-the-sentry-node}

Mag-log in sa remote sentry machine.

### I-configure ang Serbisyo ng Heimdall {#configure-the-heimdall-service}

Buksan ang `config.toml` para i-edit ang `vi ~/.heimdalld/config/config.toml`.

Baguhin ang sumusunod:

* `moniker` — anumang pangalan. Halimbawa: `moniker = "my-full-node"`.
* `seeds` — ang mga address ng seed node na naglalaman ng node ID, IP address, at port.

  Gamitin ang mga sumusunod na value:

  ```toml
  seeds="f4f605d60b8ffaaf15240564e58a81103510631c@159.203.9.164:26656,4fb1bc820088764a564d4f66bba1963d47d82329@44.232.55.71:26656,2eadba4be3ce47ac8db0a3538cb923b57b41c927@35.199.4.13:26656,3b23b20017a6f348d329c102ddc0088f0a10a444@35.221.13.28:26656,25f5f65a09c56e9f1d2d90618aa70cd358aa68da@35.230.116.151:26656"
  ```

* `pex` — i-set ang value sa `true` para i-enable ang peer exchange. Halimbawa: `pex = true`.
* `private_peer_ids` — ang node ID ng Heimdall na naka-set up sa validator machine.

  Para makuha ang node ID ng Heimdall sa validator machine:

  1. Mag-log in sa validator machine.
  1. I-run ang `heimdalld tendermint show-node-id`.

  Halimbawa: `private_peer_ids = "0ee1de0515f577700a6a4b6ad882eff1eb15f066"`.

* `prometheus` — i-set ang value sa `true` para i-enable ang Prometheus metrics. Halimbawa: `prometheus = true`.
* `max_open_connections` — i-set ang value sa `100`. Halimbawa: `max_open_connections = 100`.

I-save ang mga binago sa `config.toml`.

Buksan para sa i-edit ang `vi ~/.heimdalld/config/heimdall-config.toml`.

Sa `heimdall-config.toml`, baguhin ang RPC endpoint to point sa isang ganap na na-sync na Ethereum mainnet node:

`eth_rpc_url = <insert Infura or any full node RPC URL to Ethereum>`

Halimbawa: `eth_rpc_url = "https://nd-123-456-789.p2pify.com/60f2a23810ba11c827d3da642802412a"`


I-save ang mga binago sa `heimdall-config.toml`.

### I-configure ang Serbisyo ng Bor {#configure-the-bor-service}

Buksan para sa i-edit ang `vi ~/node/bor/start.sh`.

Sa `start.sh`, idagdag ang mga boot node address na naglalaman ng isang node ID, isang IP address, at isang port sa pamamagitan ng pagdaragdag ng sumusunod na linya sa dulo:

```config
--bootnodes "enode://0cb82b395094ee4a2915e9714894627de9ed8498fb881cec6db7c65e8b9a5bd7f2f25cc84e71e89d0947e51c76e85d0847de848c7782b13c0255247a6758178c@44.232.55.71:30303,enode://88116f4295f5a31538ae409e4d44ad40d22e44ee9342869e7d68bdec55b0f83c1530355ce8b41fbec0928a7d75a5745d528450d30aec92066ab6ba1ee351d710@159.203.9.164:30303,enode://3178257cd1e1ab8f95eeb7cc45e28b6047a0432b2f9412cff1db9bb31426eac30edeb81fedc30b7cd3059f0902b5350f75d1b376d2c632e1b375af0553813e6f@35.221.13.28:30303,enode://16d9a28eadbd247a09ff53b7b1f22231f6deaf10b86d4b23924023aea49bfdd51465b36d79d29be46a5497a96151a1a1ea448f8a8666266284e004306b2afb6e@35.199.4.13:30303,enode://ef271e1c28382daa6ac2d1006dd1924356cfd843dbe88a7397d53396e0741ca1a8da0a113913dee52d9071f0ad8d39e3ce87aa81ebc190776432ee7ddc9d9470@35.230.116.151:30303"
```

I-save ang mga binago sa `start.sh`.

Buksan para sa i-edit ang `vi ~/.bor/data/bor/static-nodes.json`.

Sa `static-nodes.json`, baguhin ang sumusunod:

* `"<replace with enode://validator_machine_enodeID@validator_machine_ip:30303>"` — sa node ID at IP address ng Bor set up sa validator machine.

  Para makuha ang node ID ng Bor sa validator machine:

  1. Mag-log in sa validator machine.
  1. I-run ang `bootnode -nodekey ~/.bor/data/bor/nodekey -writeaddress`.

  Halimbawa: `"enode://410e359736bcd3a58181cf55d54d4e0bbd6db2939c5f548426be7d18b8fd755a0ceb730fe5cf7510c6fa6f0870e388277c5f4c717af66d53c440feedffb29b4b@134.209.100.175:30303"`.

I-save ang mga binago sa `static-nodes.json`.

### I-configure ang firewall {#configure-firewall}

Kailangang ibukas sa mundo ng sentry machine ang mga sumusunod na port `0.0.0.0/0`:

* 26656- Ikokonekta ng iyong serbisyo ng Heimdall ang node mo sa iba pang node gamit ang serbisyo ng Heimdall.

* 30303- Ikokonekta ng iyong serbisyo ng Bor ang node mo sa iba pang node gamit ang serbisyo ng Bor.

* 22- Para makapag-ssh ang validator nasaan man siya.

:::note

Pero kapag gumamit sila ng VPN connection, puwede lang nilang payagan ang mga paparating na ssh connection mula sa VIP IP address.

:::

## I-start ang sentry node {#start-the-sentry-node}

Sisimulan mo muna ang serbisyo ng Heimdall. Kapag nag-sync ang serbisyo ng Heimdall, sisimulan mo na ang serbisyo ng Bor.

:::note

Tumatagal nang ilang araw ang serbisyo ng Heimdall para ganap na mag-sync mula sa simula.

Bilang alternatibo, puwede kang gumamit ng isang maintained snapshot, na babawasan ang tagal ng pag-sync nang ilang oras. Para sa mga detalyadong tagubilin, tingnan ang <ins>Mga Tagubilin para sa Snapshot para sa Heimdall at Bor</ins>.

Para sa mga download link ng snapshot, tingnan ang [Polygon Chains Snapshots](https://snapshots.matic.today/).

:::

### Simulan ang serbisyo na Heimdall {#start-the-heimdall-service}

Ang pinakabagong bersyon, ang [Heimdall v.0.2.11](https://github.com/maticnetwork/heimdall/releases/tag/v0.2.11), ay naglalaman ng ilang pagpapahusay tulad ng:
1. Paglilimita sa laki ng data sa state sync txs sa:
    * **30Kb** kapag kinakatawan sa **bytes**
    * **60Kb** kapag kinakatawan sa **string**.
2. Pagpapahaba ng **tagal ng pagkaantala** sa pagitan ng mga contract event ng iba't ibang validator para matiyak na hindi napakabilis na mapupuno ang mempool kung sakaling magkaroon ng napakarming event na makakapigil sa pag-usad ng chain.

Ipinapakita ng sumusunod na halimbawa kung paano nililimitahan ang laki ng data:

```
Data - "abcd1234"
Length in string format - 8
Hex Byte representation - [171 205 18 52]
Length in byte format - 4
```

Simulan ang serbisyo ng Heimdall:

```sh
sudo service heimdalld start
```

Simulan ang rest server ng Heimdall:

```sh
sudo service heimdalld-rest-server start
```

I-check ang mga service log ng Heimdall:

```sh
journalctl -u heimdalld.service -f
```

:::note

Sa mga log, posibleng makita mo ang mga sumusunod na error:

* `Stopping peer for error`
* `MConnection flush failed`
* `use of closed network connection`

Nangangahulugan ito na tinanggihan ng isa sa mga node sa network ang isang koneksyon sa node mo. Wala kang kailangang gawin sa mga error na ito. Hintaying mag-crawl ang node mo ng mas maraming node sa network.

:::

I-check ang mga rest-server log ng Heimdall:

```sh
journalctl -u heimdalld-rest-server.service -f
```

I-check ang status ng pag-sync ng Heimdall:

```sh
curl localhost:26657/status
```

Sa output, ang value ng `catching_up` ay:

* `true` — nagsi-sync ang serbisyo ng Heimdall.
* `false` — ang serbisyo ng Heimdall ay ganap na naka-sync.

Hintaying ganap na mag-sync ang serbisyo ng Heimdall.

### I-start ang Serbisyo ng Bor {#start-the-bor-service}

Kapag ang serbisyong Heimdall ay ganap nang na-sync, i-start ang serbisyo ng Bor.

I-start ang serbisyo ng Bor:

```sh
sudo service bor start
```

I-check ang mga log ng serbisyo ng Bor:

```sh
journalctl -u bor.service -f
```

## I-configure ang validator node {#configure-the-validator-node}

:::note

Upang makumpleto ang seksyong ito, dapat ay mayroon kang RPC endpoint ng iyong ganap na naka-sync na Ethereum mainnet node na handa.

:::

### I-configure ang Serbisyo ng Heimdall {#configure-the-heimdall-service-1}

Mag-log in sa remote validator machine.

Buksan ang `config.toml` para i-edit ang `vi ~/.heimdalld/config/config.toml`.

Baguhin ang sumusunod:

* `moniker` — anumang pangalan. Halimbawa:`moniker = "my-validator-node"`.
* `pex` — I-set ang value sa`false`upang ma-disable ang peer exchange. Halimbawa:`pex = false`.
* `private_peer_ids` — i-comment ang value upang ma-disable ito. Halimbawa:`# private_peer_ids = ""`.


Upang makuha ang node ID ng Heimdall sa sentry machine:

  1. Mag-login sa sentry machine.
  1. I-run ang `heimdalld tendermint show-node-id`.

Halimbawa: `persistent_peers = "sentry_machineNodeID@sentry_instance_ip:26656"`

* `prometheus` — i-set ang value sa `true` upang i-enable ang Prometheus metrics. Halimbawa:`prometheus = true`.

I-save ang mga nabago sa`config.toml`.

Buksan para sa i-edit ang `vi ~/.heimdalld/config/heimdall-config.toml`.

Sa`heimdall-config.toml`baguhin ang sumusunod:

* `eth_rpc_url` — isang RPC endpoint para sa isang ganap na na-sync na Ethereum mainnet node, iyon ay Infura. `eth_rpc_url =<insert Infura or any full node RPC URL to Ethereum>`

Halimbawa:: `eth_rpc_url = "https://nd-123-456-789.p2pify.com/60f2a23810ba11c827d3da642802412a"`


I-save ang mga nabago sa`heimdall-config.toml`.

### I-configure ang Serbisyo ng Bor {#configure-the-bor-service-1}

Buksan para sa i-edit ang `vi ~/.bor/data/bor/static-nodes.json`.

Sa`static-nodes.json`baguhin ang sumusunod:

* `"<replace with enode://sentry_machine_enodeID@sentry_machine_ip:30303>"` — sa node ID at IP address ng Bor na naka-set up sa sentry machine.

Upang makuha ang node ID ng Bor sa sentry machine:

  1. Mag-log in sa sentry machine.
  1. I-run ang `bootnode -nodekey ~/.bor/data/bor/nodekey -writeaddress`.

Halimbawa:`"enode://a8024075291c0dd3467f5af51a05d531f9e518d6cd229336156eb6545581859e8997a80bc679fdb7a3bd7473744c57eeb3411719b973b2d6c69eff9056c0578f@188.166.216.25:30303"`.

I-save ang mga nabago sa`static-nodes.json`.

## I-set ang owner at signer key {#set-the-owner-and-signer-key}

Sa Polygon, dapat mong panatilihing magkaiba ang owner at signer key.

* Ang signer — ang address na nag-sa-sign [sa mga transaksyon ng checkpoint](../glossary#checkpoint-transaction). Ang rekomendasyon ay panatilihin ang hindi bababa sa 1 ETH sa address ng pumirma.
* Ang Owner — ang address na ginagawa ang mga transaksyon sa pag-stake. Ang rekomendasyon ay panatilihin ang mga token ng MATIC sa address ng owner.

### Mag-generate ng pribadong key ng Heimdall {#generate-a-heimdall-private-key}

Dapat kang mag-generate ng pribadong key ng Heimdall sa validator machine lamang. **Huwag mag-generate ng Heimdall pribadong key sa sentry machine.**

Upang ma-generate ang pribadong key i-run ang:

```sh
heimdallcli generate-validatorkey ETHEREUM_PRIVATE_KEY
```

:::note
* ETHEREUM_PRIVATE_KEY — ang iyong pribadong key ng wallet ng Ethereum.

:::

Ige-generate nito ang`priv_validator_key.json` Ilipat ang nabuong JSON file sa Heimdall configuration directory:

```sh
mv ./priv_validator_key.json ~/.heimdalld/config
```

### Mag-generate ng keystore file ng Bor {#generate-a-bor-keystore-file}

Dapat kang mag-generate ng Bor keystore file lamang sa validator machine. **Huwag kang mag-generate ng Bor keystore file sa sentry machine.**

Upang ma-generate ang pribadong key i-run ang:

```sh
heimdallcli generate-keystore ETHEREUM_PRIVATE_KEY
```

:::note

ETHEREUM_PRIVATE_KEY — ang iyong Ethereum wallet address.

:::

Kapag na-prompt, mag-set up ng password sa keystore file.

Ito ay mag-ge-generate ng`UTC-<time>-<address>` keystore file.

Ilipat ang na-generate na keystore file sa Bor configuration directory:

```sh
mv ./UTC-<time>-<address> ~/.bor/keystore/
```

### Idagdag ang password.txt {#add-password-txt}

Siguraduhing nakalikha ng isang `password.txt`file pagkatapos ay idagdag ang Bor keystore file password sa mismong `~/.bor/password.txt`file.

### idagdag ang iyong Ethereum address {#add-your-ethereum-address}

Buksan para sa i-edit ang `vi /etc/matic/metadata`.

Sa `metadata`idagdag ang iyong Ethereum address. Halimbawa:`VALIDATOR_ADDRESS=0xca67a8D767e45056DC92384b488E9Af654d78DE2`.

I-save ang mga nabago sa`metadata`.

## I-start ang validator node {#start-the-validator-node}

Sa puntong ito, dapat mayroon kang:

* Ang serbisyong Heimdall sa sentry machine ay ganap na naka-sync at umaandar.
* Ang serbisyong Bor sa sentry machine ay umaandar.
* Ang serbisyong Heimdall at ang serbisyo ng Bor sa validator machine ay na-configure.
* Na-configure na ang iyong mga key ng owner at signer.

### I-start ang Serbisyong Heimdall {#start-the-heimdall-service-1}

Sisimulan mo na ngayon ang serbisyong Heimdall sa validator machine. Kapag nag-sync ang serbisyo ng Heimdall, sisimulan mo ang serbisyo ng Bor sa validator machine.

:::note

Ang serbisyo ng Heimdall ay tumatagal ng ilang araw upang ganap na mag-sync mula sa simula.

Bilang kahalili, maaari kang gumamit ng pinananatili na snapshot, na magbabawas sa oras ng pag-sync ng ilang oras. Para sa mga detalyadong tagubilin, tingnan ang <ins>Snapshot na mga Tagubilin para sa Heimdall at Bor</ins>.

Para sa snapshot na mga download link, tingnan ang [Polygon Chains Snapshots](https://snapshots.matic.today/).

:::

I-start ang serbisyo ng Heimdall:

```sh
sudo service heimdalld start
```

I-start ang rest server na Heimdall:

```sh
sudo service heimdalld-rest-server start
```

I-start ang bridge ng Heimdall:

```sh
sudo service heimdalld-bridge start
```

I-check ang mga log ng serbisyo ng Heimdall:

```sh
journalctl -u heimdalld.service -f
```

I-check rest server log ng Heimdall:

```sh
journalctl -u heimdalld-rest-server.service -f
```

I-check ang mga log ng Heimdall bridge:

```sh
journalctl -u heimdalld-bridge.service -f
```

I-check ang estado ng pag-sync ng Heimdall:

```sh
curl localhost:26657/status
```

Sa output, ang`catching_up`value ay:

* `true` — ang serbisyo ng Heimdall ay nagsi-sync.
* `false` — ang serbisyo ng Heimdall ay ganap na naka-sync.

Hintaying ganap na mag-sync ang serbisyo ng Heimdall.

### I-start ang Serbisyo ng Bor {#start-the-bor-service-1}

Sa sandaling ang serbisyo ng Heimdall sa validator machine ay ganap nang na-sync, simulan ang Bor service sa validator machine.

I-start ang serbisyo ng Bor:

```sh
sudo service bor start
```

I-check ang mga log ng serbisyo ng Bor:

```sh
journalctl -u bor.service -f
```

## I-check ang node para sa kalusugan sa komunidad {#check-node-health-with-the-community}

Ngayon na ang iyong sentry at validator node ay naka-sync at umaandar, pumunta sa [Discord](https://discord.com/invite/0xPolygon) at hilingin sa komunidad na i-check ang iyong mga node.

## Magpatuloy sa pag-stake {#proceed-to-staking}

Ngayong na-check mo na ang iyong sentry at validator node, magpatuloy sa [Pag-stake](../validator/core-components/staking).
