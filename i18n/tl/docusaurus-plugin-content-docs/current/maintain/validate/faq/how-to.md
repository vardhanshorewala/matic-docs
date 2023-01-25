---
id: how-to
title: Mga Pre-requisite at Mga Proseso
description: "Mga tutorial tungkol sa pag-validate sa Polygon."
keywords:
  - docs
  - polygon
  - how to
  - knowledge
slug: how-to
image: https://matic.network/banners/matic-network-16x9.png
---

import useBaseUrl from '@docusaurus/useBaseUrl';

### 1. Proseso ng: Pag-setup ng Bagong Node {#1-how-to-new-node-setup}

**Tandaan:** Nasa ibaba ang ilang karagdagang impormasyon sa opisyal na dokumentasyon na makakatulong habang nagse-set up ng bagong node

Nagbibigay ang dokumentong ito ng ilang karagdagang detalye para sa pag-set up ng bagong node batay sa [Full Node Deployment](https://docs.polygon.technology/docs/integrate/full-node-deployment/)

- Kinakailangan ang pag-setup ng VPN bago magpatuloy sa alinman sa mga hakbang na ito. Puwede itong gawin sa pamamagitan ng pagsangguni sa [Gabay ng user ng Bastillion ](https://www.notion.so/Bastillion-VPN-user-guide-c04f5f26afda4fa59d5d9f6041327f43)
- Kung gumagamit ka ng Macbook, may available na Native Python 2.7 na kailangang palitan ng anumang Python 3.x
- Siguraduhing na-install nang tama ang mga pip3 package.

Kung hindi nagawa nang tama ang 2 hakbang sa itaas kahit na naka-install ang ansible, hindi nito makikilala ang mga ansible package.

Puwedeng may makita ka na gaya ng screenshot sa ibaba

<img src={useBaseUrl("img/knowledge-base/node-setup-1.png")} width="100%" height="100%"/>

- Tiyakin din na walang Go package at anumang nakaraang setup ng Bor o Heimdall

Puwede mong gamitin ang mga command sa ibaba para tingnan kung mayroon o wala ng ganitong mga package

1. Go version
2. Heimdall version
3. Bor version

Kung may alinman sa mga ito, i-run ang command sa ibaba na delete at linisin ang buong setup:

```bash
ansible-playbook -l sentry playbooks/clean.yml
```
Kung hindi, magkakaroon ng error tulad ng nasa ibaba kapag sinubukan mong i-run ang '**ansible sentry -m ping**'

<img src={useBaseUrl("img/knowledge-base/node-setup-2.png")} width="100%" height="100%"/>


- Halimbawa ng **inventory.yml**

<img src={useBaseUrl("img/knowledge-base/node-setup-3.png")} width="100%" height="100%"/>

- kailangang magkapareho ang host IP ng sentry at ng validator
    - dapat ilagay ang mga colon sa dulo ng mga linya, kasama ang mga IP
- Bago ikonekta ang remote machine gamit ang command sa ibaba, kailangang naidagdag ka sa remote machine at ganoon din ang ibibigay ng team ng DevOps

    ```bash
    ssh -i <downloaded_key_file.key> <remote_user>@<ip/host>
    ```

- Kapag nakumpirma na nila ang access sa server, dapat ay magagawa mo nang mag-ssh sa remote machine
- Nararanasan namin ang error sa ibaba na dulot ng ilang issue sa config ng Heimdall

    <img src={useBaseUrl("img/knowledge-base/node-setup-4.png")} width="100%" height="100%"/>


- Maaayos ito sa pamamagitan ng mga sumusunod na hakbang:
    - i-run ang mga command sa ibaba (sa loob ng folder na 'node-ansible'):

        ```bash
        git checkout fixing_symlinks_on_clean
        git pull https://github.com/maticnetwork/node-ansible/tree/fixing_symlinks_on_
        ```
    - I-cross check ang 'clean.yml' sa machine gamit ang [clean.yml sa github repo](https://github.com/maticnetwork/node-ansible/blob/fixing_symlinks/playbooks/clean.yml)
    - Kung may anumang pagkakaiba, palitan ang nasa machine mo at ipalit ang nasa repo
    - Dapat na nara-run mo na ngayon ang clean script at pagkatapos, mara-run mo na ang installation script
- moniker=ilagay ang unique identifier
    - puwedeng kahit ano ang unique identifier na hiningi batay sa dokumento (ibigay ang pangalan mo)
- eth_rpc_url =ilagay ang Infura o alinmang full node RPC URL sa Ethereum
    - para sa hakbang na ito
        - mag-sign in sa infura.io (mag-signup kung wala ka pang account)

        - Kopyahin ang https endpoint na makikita sa ilalim ng ethereum → keys → endpoints

        <img src={useBaseUrl("img/knowledge-base/node-setup-5.png")} width="100%" height="100%"/>


            - Ilagay ang kinopyang https endpoint bilang **eth_rpc_url**
            sa **~/.heimdalld/config/heimdall-config.toml**

### 2. Bakit kailangan kong panatilihin ang ETH sa aking signer account? {#2-why-do-i-have-to-keep-eth-in-my-signer-account}

Kinakailangan ang ETH sa signer account mo para sa pagsusumite ng mga checkpoint sa Ethereum, kailangan ang ETH sa lahat ng transaksyon para gamitin bilang Gas. Kaya kailangan ang ETH sa Signer Account mo.

### 3. Para sa isang Matic Validator, kailangan ko pa bang mag-setup ng isang Sentry at Validator node o puwede bang Validator node lang ang patakbuhin ko? {#3-for-a-matic-validator-do-i-need-to-setup-a-sentry-and-validator-node-or-can-i-just-run-the-validator-node-only}

Para sa Matic Validator, hinihiling ng aming ecosystem at architecture na mag-run ka ng setup ng Sentry + Validator. Ito ay para matiyak na hindi nakalantad sa publiko ang Validator node mo at ang Sentry node mo lang ang nakalantad.

Ang iyong Sentry node ay kumukuha ng impormasyon / mga block mula sa network at pagkatapos ay nire-relay ang mga ito sa validator para i-validate.

### 4. Paano mag-migrate sa mga bagong node at pagkatapos ay mag-cut over? {#4-how-to-migrate-to-new-nodes-and-then-cut-over}

1. Ibigay ang mga node at i-install ang lahat ng software batay sa mga tagubilin.

2. I-download ang mga pinakabagong Heimdall at Bor snapshot sa parehong mga node.

3. Ilipat ang Key at mga Keystore file sa bagong validator.

4. I-shut down ang kasalukuyang validator at sentry node.

5. Simulan ang lahat ng serbisyo sa sentry, pagkatapos ay sa validator.

### 5. Paano i-check ang heimdall version? {#5-how-to-check-the-heimdall-version}

I-run:

`heimdalld version`

### 6. Aling Pribadong Key ang dapat nating idagdag kapag bumubuo tayo ng validator key? {#6-which-private-key-should-we-add-when-we-generate-validator-key}

Ang gagamiting Pribadong key ay ang ETH address ng Wallet mo kung saan naka-store ang Matic testnet Token mo. Puwede mong kumpletuhin ang pag-setup gamit ang isang pampubilko-pribadong pares ng key na nakakonekta sa address na isinumite sa form.

### 7. Saan natin mahahanap ang lokasyon ng impormasyon ng Heimdall account {#7-where-can-we-find-heimdall-account-info-location}

Para sa binaries:

```jsx
~/.heimdalld/config folder
```

Para sa Linux package:

```jsx
/etc/heimdall/config
```

### 8. Aling file ang idaragdag natin sa API key? {#8-which-file-do-we-add-the-api-key}

Kapag nagawa mo na ang API key, kailangan mong idagdag ang API key sa `heimdall-config.toml` file.

### 9. Aling file ang idaragdag namin sa persistent_peers? {#9-which-file-do-we-add-the-persistent_peers}

Puwede mong idagdag ang persistent_peers sa sumusunod na file:

```jsx
~/.heimdalld/config/config.toml
```

### 10. Paano ihihinto ang mga serbisyo ng Heimdall at Bor? {#10-how-to-stop-heimdall-and-bor-services}

**Para sa mga Linux package**:

Itigil ang Heimdall: `sudo service heimdalld stop`

Itigil ang Bor: `sudo service bor stop` o

1. `ps -aux | grep bor`. Kunin ang PID para sa BOR at pagkatapos ay i-run ang sumusunod na command.
2. `sudo kill -9 PID`

**Para sa Binaries**:

Itigil ang Heimdall: `pkill heimdalld`

Itigil ang Bridge: `pkill heimdalld-bridge`

Itigil ang Bor:  `bash stop.sh`

### 11. Paano tanggalin ang mga directory ng Heimdall at Bor? {#11-how-to-remove-heimdall-and-bor-directories}

**Para sa mga Linux package**:

I-delete ang Heimdall: : `sudo rm -rf /etc/heimdall/*`

I-delete ang Bor: `sudo rm -rf /etc/bor/*`

**Para sa Binaries**:

I-delete ang Heimdall: : `sudo rm -rf ~/.heimdalld/`

I-delete ang Bor: `sudo rm -rf ~/.bor`

### 12. Paano bawasan ang cache sa Bor? {#12-how-to-reduce-cache-in-bor}

Sinusuportahan ng bor ang --cache parameter na makakapagpabawas sa cache para iwasang maubusan ng memory

### 13. Paano i-delete ang Bor DB data? {#13-how-to-delete-the-bor-db-data}

```
bor --datadir  ~/.bor/data removedb
cd ~/node/bor
bash setup.sh
service bor start
```
