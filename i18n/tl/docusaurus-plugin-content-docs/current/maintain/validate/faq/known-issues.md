---
id: known-issues
title: Mga Kilalang Isyu at Error
description: "Batayan ng Kaalaman ng mga karaniwang error."
keywords:
  - docs
  - polygon
  - matic
  - issues
  - errors
  - invalid
  - command
slug: known-issues
image: https://matic.network/banners/matic-network-16x9.png
---

import useBaseUrl from '@docusaurus/useBaseUrl';

### 1. Error: Bad block/Di-wastong Merkle {#1-error-bad-block-invalid-merkle}

**Paglalarawan:**
Nagkakaroon ng root error sa Bad Block o Di-wastong Merkle kapag hindi naka-sync sa isa't isa ang iyong Heimdall at Bor. Ang Heimdall ay ang consensus layer para sa Polygon POS chain, na nangangahulugan na inuutusan ng Heimdall ang Bor na gumawa ng block nang naaayon. Nagkakaroon ng Bad Block kapag nagpatuloy ang Bor na gawin ang isang block nang hindi naman inutos ng Heimdall. Kung gayon, may nagawang di-wastong hash, na nagdudulot ng error, Bad Block, o Di-wastong Merkle root.

**Solusyon 1**:
Karaniwang malulutas ang problema kapag ni-restart ang serbisyo ng Bor. Titiyakin nito na kumokonektang ulit ang iyong Bor sa Heimdall at nagsisimulang mag-sync at gumawa ng mga block nang tama.

Para i-restart ang iyong serbisyo ng Bor, maaari mong gamitin ang sumusunod na command, `sudo service bor restart`

**Solusyon 2**:
Kung hindi naayos ng pag-restart ang iyong problema, ang unang dapat mong tingnan ay ang iyong Heimdall at Rest server. Kadalasan, maaaring tumigil ang iyong serbisyo ng Heimdall na siyang naging sanhi ng isyu ng Bad block sa Bor.

Tingnan muna ang mga log para sa iyong Heimdall, `journalctl -u heimdalld -f` at tingnan kung gumagana nang tama ang lahat.

Bilang karagdagan, tingnan din ang mga log ng iyong Rest server, `journalctl -u heimdalld-rest-server -f`

Kung nakita mo na hindi tumatakbo nang tama ang alinman sa mga serbisyong ito, paki-restart ang mga serbisyo sa itaas at hayaang mag-sync ang mga ito. Dapat na awtomatikong malutas ng iyong Bor ang problema.

**Solusyon 3**:
Kung hindi malutas ng pag-restart ng iyong mga serbisyo ng Bor at Heimdall ang problema, malamang na natigil ang iyong Bor sa isang block. Kapuna-puna ang numero ng block sa mga log. Para tingnan ang iyong mga log para sa Bor, maaari mong patakbuhin ang command na ito, `journalctl -u bor -f`

Ipapakita ang Bad block sa ganitong paraan sa iyong mga log.
<img src={useBaseUrl("img/knowledge-base/bad_block.png")} width="75%" height="100%"/>

Kapag alam mo na ang numero ng Bad block, maaari mong i-roll back ang iyong Blockchain nang ilang daang block at i-sync muli mula sa isang nakaraang block. Upang magawa ito, kakailanganin mo munang i-convert ang numero ng Block sa hexadecimal. Maaari mong gamitin ang [https://www.rapidtables.com/convert/number/decimal-to-hex.html](https://www.rapidtables.com/convert/number/decimal-to-hex.html) para sa pagko-convert ng mga decimal papunta sa mga hexadecimal.

Kapag naihanda mo na ang iyong Hexadecimal, maaari mong patakbuhin ang mga sumusunod na command

```jsx
bor attach ./.bor/data/bor.ipc
> debug.setHead("0xE92570")
```

Ang `debug.setHead` ay ang function na magbibigay-daan sa iyong Bor na itakda ang tip sa partikular na taas ng Block.

Sa sandaling patakbuhin mo ang mga command na ito, ang output para dito ay magiging `null` . Mabuti ang ibig sabihin ng null at nilalayon ito. Maaari mo na ngayong simulang subaybayang muli ang iyong mga log para sa Bor at tingnan kung makakalampas ito sa numero ng block na iyon. Pinakamabuti sana, dapat itong makalampas.

Kung sakaling hindi gumagana ang mga solusyon na ito, mangyaring makipag-ugnayan kaagad sa team ng Suporta ng Polygon.

### 2. Error: Hindi Nagawa ang Mga Sanity Check {#2-error-failed-sanity-checks}

**Paglalarawan:**
`Addressbook` ang mga babala ay kadalasang maaaring balewalain nang walang isyu. Kung nakakonekta ang iyong node sa sapat na bilang ng mga peer, maaaring balewalain ang mga ganitong uri ng error. Sinusubukan lang ng iyong `pex` na muling itatag ang mga koneksyon nito sa mga peer na naroon na sa `addrbook.json`

### 3. Isyu: Mabagal ang pag-synchronize ng Bor {#3-issue-bor-synchronisation-is-slow}

**Paglalarawan:**
Kung mabagal ang pag-synchronize ng Bor, maaaring ito ay dahil sa alinman sa mga kadahilanan sa ibaba:

- Tumatakbo ang node sa isang fork - ibig sabihin na sa isang tiyak na punto, ginawa ang pag-produce ng block sa pamamagitan ng pag-fork sa isang naiibang block at nakaapekto ito sa karagdagang pag-produce ng block
- Hindi gumagana ang machine sa mga pinakamabuting antas ng kalagayan at maaaring may hindi sapat na mga mapagkukunan.
    - Maaari itong matugunan sa pamamagitan ng pagsisiyasat sa:
        - IOPS
            - Ang ibig sabihin ng IOPS ay Input/Output state of cycle
            - Ang rate ng pagbasa ay karaniwang mas mataas kaysa sa bilis ng pagsulat
            - 6000 ang inirerekomendang saklaw para sa IOPS
        - Lakas ng Pagpoproseso
            - Ang processor ay kailangang 8 o 16 core
            - RAM: 32 GB ang minimum; 64 GB ang inirerekomenda
            - Ang pag-import ng block ay dapat na higit sa 2 block para sa bawat segundo
        - Ang rate ng pag-sync ng node ay dapat na 15-20 block bawat 8 segundo


**Solusyon:**
Dahil ang isyu ay mas nauukol sa kakulangan ng mga mapagkukunan ng hardware, subukang i-upgrade ito sa doble ng mga kasalukuyang espesipikasyon.

### 4. Hindi nilalagdaan ng node ang anumang checkpoint {#4-node-is-not-signing-any-checkpoints}

**Paglalarawan:**
Una sa lahat, ang hindi paglalagda ng iyong node sa mga checkpoint ay maaaring bunsod ng maraming kadahilanan.

**Solusyon 1:**
Tingnan muna kung tumatakbo nang tama ang iyong serbisyo ng Heimdall sa iyong Sentry at Validator node. Kung tumigil bigla ang serbisyo o nakakakita ng anumang error, subukang i-restart ang iyong serbisyo ng Heimdall at saksihang bumalik ito sa normal.

**Solusyon 2:**
I-check ang iyong serbisyo ng Bor at tingnan kung ito ay biglang tumigil o may anumang error sa mga log. Subukang i-restart ang iyong serbisyo ng Bor para malutas ang isyung ito.

**Solusyon 3:**
Tingnan kung tumatakbo o hindi ang iyong Heimdall Bridge o kung mayroon itong anumang error sa mga log. Subukang i-restart ang serbisyo at tingnan kung malulutas ang isyu.

### 5. Isyu: Hindi makakonekta ang Validator Heimdall sa mga Peer {#5-issue-validator-heimdall-is-unable-to-connect-to-peers}

**Paglalarawan:**
Karaniwang nangangahulugan ito na nagkakaroon ng mga isyu ang iyong Sentry Heimdall.

**Solusyon:**
- I-check ang iyong Sentry Heimdall at tingnan kung tumatakbo nang maayos ang serbisyo.
- Kung itinigil ang serbisyo, dapat malutas ang isyung ito kapag ni-restart ang serbisyo sa iyong Sentry.
- Sa katulad na paraan, pagkatapos ayusin ang iyong sentry, dapat ding malutas ang problema kapag ni-restart ang iyong serbisyo ng Heimdall.

### 6. Error: Error habang fine-fetch ang mainchain receipt error {#6-error-error-while-fetching-mainchain-receipt-error}

**Paglalarawan:** Ang mga ito ay mga normal na log. Huwag gawin ang kahit ano sa iyong bridge.

### 7. Natigil nang matagal ang Validator Bor sa block {#7-validator-bor-is-stuck-on-block-for-a-long-time}

**Paglalarawan:**
Nangangahulugan ito na natigil rin ang iyong Bor sa iyong Sentry dahil kumukuha ng impormasyon ang iyong Validator mula sa iyong Sentry.

**Solusyon:**

- Paki-check ang iyong mga log ng Bor sa iyong sentry at tingnan kung ayos ang lahat.
- Siguro ay i-restart ang serbisyo ng Bor una sa iyong Bor at saka kasabay ding i-restart ang iyong serbisyo ng Bor sa iyong Validator.

### 8. Error (habang ina-upgrade ang Bor): bumuo ng [github.com/ethereum/go-ethereum/cmd/geth:](http://github.com/ethereum/go-ethereum/cmd/geth:) hindi ma-load ang hash/maphash: malformed module path "hash/maphash": nawawalang tuldok sa unang path element {#cannot-load-hash-maphash-malformed-module-path-hash-maphash-missing-dot-in-first-path-element}

**Paglalarawan:**
Ito ay dahil medyo lipas na ang iyong Bersyon ng Go.

**Solusyon:**
Ang inirerekomendang bersyon ng Go ay 1.15.x at pataas

### 9. Isyu: Nahihirapan ang Sentry Bor sa 'Naghahanap ng mga peer' at hindi nagtatagumpay ang mga Peer {#9-issue-sentry-bor-is-still-struggling-with-looking-for-peers-and-peers-are-not-succeeding}

**Paglalarawan:**
Maaaring mangyari ito kapag nawalan ng koneksiyon ang Bor sa iba pang peer.

**Solusyon:**

- Tingnan ang `[start.sh](http://start.sh)` file (~/node/bor/start.sh) at dapat nitong ipakita sa iyo ang iyong mga bootnode.
- Tingnan kung nakalagay nang tama ang mga bootnode nang walang anumang isyu sa formatting.
- Kung gumawa ka ng anumang pagbabago sa file, paki-restart ang iyong serbisyo ng Bor at tingnan kung nalutas ang isyu.

Kung wala sa mga ito ang gumagana, mangyaring makipag-ugnayan kaagad sa **Team ng Suporta** para sa tulong.

### 10. Error: (sa Bor) "Nabigong maghanda ng header mining sa block 0" {#10-error-in-bor-failed-to-prepare-header-mining-at-block-0}

**Paglalarawan:**
Nangyayari ito dahil sa isyu sa formatting sa iyong `static-nodes.json` file (~/.bor/data/bor/static-nodes.json).

**Solusyon:**

- Tiyakin na walang puwang at walang karagdagang character tulad ng < / > .
- Kung gumawa ka ng anumang pagbabago sa file, paki-restart ang serbisyo ng Bor at dapat na makakita ka ng mga log na nagpi-print.

### 11. Error: "30303" o di-wastong command {#11-error-30303-or-invalid-command}

**Paglalarawan:**
Ito ay dahil hindi mo nagawa ang bor keystore at ang file ng password para dito.

**Solusyon:**

Tiyakin na sundin mo ang lahat ng hakbang mula sa gabay sa pag-setup.

### 12. Error: Imposibleng reorg, mangyaring mag-file ng isyu {#12-error-impossible-reorg-please-file-an-issue}

**Paglalarawan:**
Hayaan na lang ang mga log na ito. Hindi dapat mahirapan ang iyong node nang dahil dito at dapat na awtomatikong malutas ang isyu.

Kung nahihirapan ang iyong node nang dahil dito, mangyaring makipag-ugnayan kaagad sa team ng suporta.

### 13. Error: "Hindi natagpuan ang host" habang nagse-set up ng node gamit ang Ansible {#13-error-host-not-found-while-setting-up-a-node-using-ansible}

**Paglalarawan:**
Maaaring ito ay dahil may ilang isyu sa formatting ang iyong `inventory.yml` file.

**Solusyon:**
Itama ang mga ito gamit ang wastong indentation at saka subukang muli

### 14. Isyu: "Nabigo ang pag-dial" sa Heimdall {#14-issue-dialling-failed-in-heimdall}

**Paglalarawan:**
May kinalaman ito sa koneksiyon at mas partikular na problemang may kaugnayan sa port

**Solusyon:**

- Tingnan kung ipinapakita pa rin ang parehong block sa curl localhost:26657/status
- Subukan ang Pag-restart ng Heimdall.
- Siguraduhin na nakabukas ang koneksiyon sa port 26656 na ito.
- Subukang magdagdag ng mga peer sa vi ~/.heimdalld/config/config.toml
- Itakda sa 100 ang parameter na max_open_connection.

### 15. Isyu: Naghahanap ng mga Peer o Itinitigil ang Peer para sa error {#15-issue-looking-for-peers-or-stopping-peer-for-error}

**Solusyon:**

- buksan ang `config.toml` file sa iyong Sentry node.

`~/.heimdalld/config/config.toml`

- At saka hanapin ang parameter na `external_address`. Kapag nahanap mo na ito, dapat mo itong i-update sa

`tcp://<my_elastic_ip>:26656`

- Kung saan ang `my_elastic_ip` ay ang pampublikong IP ng iyong Sentry.
- Kapag na-update mo na ito, ang kailangan mo na lang gawin ay i-restart ang iyong serbisyo ng Heimdall sa iyong Sentry

`sudo service heimdalld restart`

- Tiyakin na ginagawa mo lang ito sa iyong sentry.

Sundin ang mga hakbang sa ibaba para sa pagdaragdag ng mga karagdagang peer sa `vi ~/.heimdalld/config/config.toml`

- Itigil ang serbisyo ng heimdalld

    ```
    sudo service heimdalld stop
    ```

- I-clear ang iyong addrbook

    ```
    sudo service heimdalld stop
    cp ~/.heimdalld/config/addrbook.json ~/.heimdalld/config/addrbook.json.bkp
    rm ~/.heimdalld/config/addrbook.json
    ```

- Dagdagan ang max_num_inbound_peers at max_num_outbound_peers sa `~/.heimdalld/config/config.toml`:

    ```
    max_num_inbound_peers = 300
    max_num_outbound_peers = 100
    ```

- Simulan ang serbisyo ng heimdalld:

    ```
    sudo service heimdalld start
    ```


### 16. Error: Error habang nagfe-fetch ng data mula sa URL {#16-error-error-while-fetching-data-from-url}

**Halimbawang error:**

```bash
module=span service=processor error="Error while fetching data from url:
[http://0.0.0.0:1317/bor/prepare-next-span?chain_id=137&proposer=0x29f265b54a298df0c1b762f688e7e7c09d8790ea&span_id=2863&start_block=18317056](http://0.0.0.0:1317/bor/prepare-next-span?chain_id=137&proposer=0x29f265b54a298df0c1b762f688e7e7c09d8790ea&span_id=2863&start_block=18317056), status: 400"
Aug 23 12:07:23 US-CA-SN01 bridge[2340]: E[2021-08-23|12:07:23.158] Unable to fetch next span details            
module=span service=processor lastSpanId=2862
```

**Solusyon:**

Kailangang i-restart ang Heimdall Bridge.

### 17. Error: walang code ng kontrata sa ibinigay na address {#17-error-no-contract-code-at-the-given-address}

**Solusyon**

1. Kunin ang mga tamang config mula sa Github at kopyahin ang mga ito sa ~/.heimdalld/config at
2. Paki-reset ang heimdall gamit ang heimdall unsafe-reset-all.

### 18. Isyu: Mga problema sa pagsisimula sa Bor {#18-issue-problems-in-starting-bor}

**Isyu:**
Kinakailangan ng address bilang argument.


**Solusyon:**

Kailangang idagdag ang address

```bash
/etc/matic/metadata
```

### 19. Error: Nabigong ma-unlock ang account (0x...) Walang key para sa ibinigay na address o file {#19-error-failed-to-unlock-account-0x-no-key-for-given-address-or-file}

**Paglalarawan:**

Nangyayari ang error na ito dahil may mali sa paraan para sa password.txt record. Maaari mong sundin ang mga hakbang sa ibaba para baguhin ito.

**Solusyon:**

Para sa mga Linux package

Wakasan ang proseso ng Bor

**Para sa linux**:

1. `ps -aux | grep bor`. Kunin ang PID para sa Bor at saka patakbuhin ang sumusunod na command.
2. `sudo kill -9 PID`

**Para sa Ansible:**

1. Kopyahin ang keystore file ng bor sa

    ```jsx
    /etc/bor/dataDir/keystore
    ```

2. At password.txt sa

    ```jsx
    /etc/bor/dataDir/
    ```

3. Tiyaking naidagdag mo ang tamang address sa `/etc/bor/metadata`

**Para sa mga Binary:**

1. Kopyahin ang file ng Bor keystore sa:

    ```jsx
    ~/.bor/keystore/
    ```

2. At password.txt sa

    ```jsx
    ~/.bor/password.txt
    ```


### 20. Mga kahihinatnan sa pagkakamintis ng validator sa checkpoint at mga punto na iimbestigahan mula sa aming panig {#20-consequences-of-validator-missing-a-checkpoint-and-points-to-investigate-from-our-side}

- Ekonomiks
    - Hindi magandang reputasyon para sa Validator
    - Hindi makukuha ang mga gantimpala para sa Delegator
- imbestigasyon
    - Hihingin ang mga kamakailang log

### 21. Error: dpkg: error sa pagpoproseso ng archive na matic-heimdall-xxxxxxxxxx {#21-error-dpkg-error-processing-archive-matic-heimdall-xxxxxxxxxx}

**Halimbawa:**

```bash
 "dpkg: error processing archive matic-heimdall_1.0.0_amd64.deb (--install): trying to overwrite '/heimdalld-rest-server.service', which is also in package matic-node 1.0.0"
```

**Solusyon:**

Pangunahing nangyayari ito dahil sa dating pag-install ng Matic sa machine. Para malutas, maaari mong patakbuhin ang:

`sudo dpkg -r matic-node`

### 22. Isyu: Naka-rest ang Tendermint nang hindi nire-reset ang data ng application {#22-issue-tendermint-was-rest-without-resetting-application-s-data}

**Solusyon:**

- I-reset ang config data ng heimdall at subukang patakbuhin muli ang pag-install

    ```jsx
    $ heimdalld unsafe-reset-all
    ```

    ```jsx
    $ rm -rf $HEIMDALLDIR/bridge
    ```


### 23. Error: "Maling Block.Header.AppHash." {#23-error-wrong-block-header-apphash}

**Paglalarawan:**
Karaniwang nangyayari ang error na ito dahil sa naubos na ang mga kahilingan sa Infura. Kapag nagse-setup ka ng node sa Matic, nagdaragdag ka ng Infura Key sa Config file (Heimdall). Bilang default, pinapayagan ka ng 100k na Kahilingan bawat araw. Kung malagpasan ang limitasyong ito, mahaharap ka sa mga ganitong problema.

**Solusyon**
Para malutas ito, maaari kang gumawa ng bagong API key at idagdag ito sa `config.toml` file.

### 24. Isyu: Nag-crash ang Bor {#24-issue-bor-crashed}

**Solusyon:**

- Subukang mag-upgrade para doblehin ang laki ng RAM
- Halimbawa, ang kanilang kasalukuyang kapasidad ng RAM ay 16 GB, maaari itong i-upgrade sa 32 GB

### 25. Error: err="insufficient na mga pondo para sa presyo ng gas * + value" {#25-error-err-insufficient-funds-for-gas-price-value}

**Paglalarawan:**

Lumalabas ang mga log na ito kapag walang sapat na ETH sa iyong signer wallet.

**Solusyon:**
Inirerekomendang [](http://wallet.it/)magkaroon ng 1 ETH sa iyong signer wallet ngunit maaari kang magpanatili ng .5-.75 sa loob nito kung madalas mo naman itong tingnan.
