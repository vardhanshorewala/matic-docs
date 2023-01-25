---
id: validator-faq
title: Mga Madalas Itanong tungkol sa Validator
description: "Mga karaniwang tanong tungkol sa mga operasyon ng validator."
keywords:
  - docs
  - matic
  - polygon
  - validator
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

## Paano ako makakapagpa-reseerve ng slot ng validator? {#how-can-i-reserve-a-validator-spot}

Kung mayroon kaming bakanteng slot ng validator, puwedeng maging validator sa system ang sinumang may stake, anuman ang halaga nito. Magkakaroon ng mga auction ng validator na regular na inoorganisa (karaniwang sa loob ng ilang araw), kung saan puwedeng palitan ng kahit sino ang sinumang kasalukuyang validator sa pamamagitan ng pagpapanukala ng mas mataas na stake. Sa madaling salita, isa itong bukas na system kung saan hindi kami puwedeng mag-reserve ng mga slot para sa sinuman.

Sa anumang sitwasyon, palaging may posibilidad ng pag-delegate ng stake sa kasalukuyang set ng validator. Puwedeng lumahok ang sinuman sa proseso gamit ang mekanismong ito at makakuha ng mga gantimpala hangga't matapat at naka-online ang kaukulang validator.

## Sa ano-anong state puwedeng lumahok ang isang validator? {#what-are-the-different-states-a-validator-can-be-in}

* **Active**: Ang validator ay nasa kasalukuyang set ng validator, gumagawa ng mga block sa Bor layer, lumalahok sa consensus ng Heimdall at nagko-commit ng mga transaksyon sa checkpoint sa Ethereum mainnet.
* **Abiso**: Nagpapadala ang validator ng transaksyon para mag-unbond. Bago simulan ang pag-unbond, kailangang nasa active state ang validator na gumagawa, lumalagda, at nagpapanukala ng mga block sa loob ng isang tiyak na panahon.
* **Pag-unbond**: Hindi active ang validator sa state na ito at hindi nakakakuha ng gantimpala. Gayunpaman, mananatiling saklaw ng pag-slash ang validator kung gumawa sila ng anumang nakapipinsalang kilos.

## May minimum na halaga ba ng MATIC na kailangang i-stake para maging validator? {#is-there-a-minimum-amount-of-matic-required-to-stake-to-become-a-validator}

Ang minimum ay 1 Matic.

Nabanggit na namin dati na pinag-iisipan naming magkaroon ng minimum na kinakailangang self stake mula sa mga validator, dahil umaasa kami na magkakaroon din ang mga validator ng pagmamalasakit sa tagumpay ng gawaing ito. Pero dahil lilipat na kami sa isang matatag na diskarte sa pagpapalit habang limitado ang bilang ng mga slot ng validator sa ngayon, hindi ito nangangailangan ng anumang minimum na kinakailangang self stake. Pero makatuwiran lang na sa paglipas ng panahon, malamang na taas at mas lalaki ang average/median na stake ng isang validator.

## Paano mapapalitan ng bagong validator ang isang kasalukuyang validator? {#how-can-a-new-validator-replace-an-existing-one}

May limitadong espasyo para sa pagtanggap ng mga bagong validator. Makakasali lang ang mga bagong validator sa active set kapag nag-unbond ang isang kasalukuyang aktibong validator.

Magpapatupad ng bagong proseso ng auction para sa pagpapalit ng validator.

## Nagpapakita ang Heimdall ng "Failed Sanity Checks" {#heimdall-shows-failed-sanity-checks}

Madalas na puwedeng balewalain ang mga `Addressbook` na babala nang walang isyu. Kung nakakonekta ang iyong node sa sapat na bilang ng mga peer, puwedeng balewalain ang mga ganitong uri ng error. Sinusubukan lang ng iyong `pex` na muling itaguyod ang mga koneksyon nito sa mga peer na naroon na sa `addrbook.json`.

## Ayos naman ang mga log ng Heimdall at Bor at  tumatakbo nang tama maging ang bridge ko, pero hindi nilalagdaan ng node ko ang anumang checkpoint {#heimdall-and-bor-logs-are-fine-and-even-my-bridge-is-running-correctly-but-my-node-is-not-signing-any-checkpoints}

Puwede itong mangyari kung nakaligtaan mong idagdag ang `ETH_RPC_URL` sa `heimdall-config.toml` file. Pakitingnan kung naidagdag mo ito. Kung hindi, tiyakin na idagdag mo ang tamang URL at saka i-restart ang iyong serbisyo ng Heimdall.

## Puwede ko bang simulan ang Bor bago ganap na ma-sync ang Heimdall? {#can-i-start-bor-before-heimdall-is-completely-synced}

Hindi mo pwedeng gawin iyon. Kung sisimulan mo ang Bor nang hindi ganap na na-sync ang Heimdall, magkakaroon ka ng mga isyu sa iyong Bor.

## Hindi makakonekta ang validator Heimdall sa mga peer {#validator-heimdall-is-unable-to-connect-to-peers}

Karaniwang nangangahulugan ito na nagkakaroon ng mga isyu ang  sentry Heimdall mo. I-check ang sentry Heimdall mo at tingnan kung tumatakbo nang maayos ang serbisyo. Kung tumigil ang serbisyo, dapat malutas ang isyung ito kapag ni-restart ang serbisyo sa sentry mo. Gayundin, pagkatapos ayusin ang sentry mo, dapat ding malutas ang problema kapag ni-restart ang serbisyo ng Heimdall mo.

## Nagpapakita ang Heimdall ng "pong timeout" {#heimdall-shows-pong-timeout}

Buong error:

```
E[2021-03-01|13:19:12.252] Connection failed @ sendRoutinemodule=p2ppeer=3d1f71344c2d3262eac724c22f8266d9b3e41925@3.217.49.94:26656 conn=MConn{3.217.49.94:26656} err="pong timeout"
```

Karaniwan, dapat malutas ang problema kapag ni-restart ang serbisyo ng Heimdall.

## Nagpapakita ang Heimdall ng "Error: Wrong Block.Header.AppHash. Inaasahang xxxx" {#heimdall-shows-error-wrong-block-header-apphash-expected-xxxx}

Karaniwang nangyayari ang error na ito kapag natigil ang serbisyo ng Heimdall sa isang block at walang magagamit na opsyon ng Rewind sa Heimdall.

**Solusyon:**
Para lutasin ito:
* Ganap na i-reset ang Heimdall
* Mag-sync ulit mula sa snapshot

### I-reset ang Heimdall {#reset-heimdall}

I-reset ang Heimdall gamit ang mga sumusunod na command:

```
sudo service heimdalld stop
heimdalld unsafe-reset-all
```

### I-sync ang Heimdall mula sa Snapshot {#sync-heimdall-from-snapshot}

Ganito mo isi-sync ang Heimdall mula sa isang Snapshot:

```
wget -c <Snapshot URL>
tar -xzvf <snapshot file> -C <HEIMDALL_DATA_DIRECTORY>
```

Pagkatapos ay simulan ulit ang mga serbisyo ng Heimdall.

Tingnan ang:

* [Magpatakbo ng Validator Node gamit ang Ansible](../run-validator-ansible)
* [Magpatakbo ng Validator Node mula sa mga Binary](../run-validator-binaries)

## Nagpapakita ang Heimdall ng "dpkg: error processing archive" {#heimdall-shows-dpkg-error-processing-archive}

Buong error:

```
dpkg: error processing archive matic-heimdall_1.0.0_amd64.deb (--install): trying to overwrite '/heimdalld-rest-server.service', which is also in package matic-node 1.0.0
```

Pangunahing nangyayari ito dahil sa dating pag-install ng Polygon sa machine mo. Para lutasin ito, puwede mong i-run ang:

`sudo dpkg -r matic-node`

## Hindi malinaw kung aling pribadong Key ang dapat kong idagdag kapag nag-generate ako ng validator key {#it-is-not-clear-which-private-key-i-should-add-when-i-generate-a-validator-key}

Ang pribadong key na gagamitin ay ang ETH address ng wallet mo kung saan naka-store ang mga Polygon token mo.

## May paraan ba para malaman kung naka-sync ang Heimdall? {#is-there-a-way-to-know-if-heimdall-is-synced}

Puwede mong i-run ang sumusunod na command para tingnan ito:

```sh
curl http://localhost:26657/status
```

Tingnan ang value ng `catching_up`. Kung ito ay `false`, naka-sync na ang node.

## Ano ang pagkakaiba ng `~.heimsdall` at `/etc/heimsdall?`

Ang `~/.heimsdall` ay ang directory ng Heimdall kapag ginamit mo ang binary na paraan ng pag-install.

Ang `/etc/heimdall` ay para sa Linux package na paraan ng pag-install.

## Saan ko mahahanap ang lokasyon ng impormasyon ng Heimdall account? {#where-can-i-find-heimdall-account-info-location}

Para sa mga binary: `~/.heimdalld/config`.

Para sa Linux package `/etc/heimdall/config`.

## Sa aling file ko idaradag ang persistent_peers? {#which-file-do-i-add-the-persistent_peers}

Puwede mong idagdag ang persistent_peers sa `~/.heimdalld/config/config.toml`.

## Nagpapakita ang Heimdall ng “Did you reset Tendermint without resetting your application's data?” {#heimdall-shows-did-you-reset-tendermint-without-resetting-your-application-s-data}

I-reset ang config data ng Heimdall at subukang i-run ulit ang pag-install:

```sh
heimdalld unsafe-reset-all
rm -rf $HEIMDALLDIR/bridge
```

## Nagpapakita ang Heimdall ng Panic error {#heimdall-shows-a-panic-error}

Buong error:

```
panic: Unknown db_backend leveldb, expected either goleveldb or memdb or fsdb
```

Gawing `goleveldb` ang config sa `config.toml`.

## Magkapareho ba ang mga pribadong key para sa Heimdall at Bor keystore? {#are-the-private-keys-the-same-for-heimdall-and-bor-keystore}

Oo, magkapareho ang pribadong key na ginagamit para sa pag-generate ng mga validator key at Bor keystore. Ang pribadong key na ginamit sa pagkakataong ito ay ang ETH address ng wallet mo kung saan naka-store ang mga Polygon token mo.

## Error: (Heimdall) Paki-repair ang WAL file bago i-restart ang module=consensus {#error-heimdall-please-repair-the-wal-file-before-restarting-module-consensus}

Nangyayari ang isyu kapag na-corrupt ang WAL file.

**Solusyon:**

I-run ang mga sumusunod na command:
```
WALFILE=~/.heimdalld/data/cs.wal/wal
cp $WALFILE ${WALFILE}.bak
git clone https://github.com/maticnetwork/tendermint.git
cd tendermint
go run scripts/wal2json/main.go $WALFILE > wal.json
rm $WALFILE
go run scripts/json2wal/main.go wal.json $WALFILE
```

## Nagpapakita ang Bor ng 'Looking for peers' at hindi makahanap ng mga peer  {#bor-shows-looking-for-peers-and-cannot-find-peers}

Puwede itong mangyari kapag nawalan ng koneksyon ang Bor sa iba pang peer. Sa kaso ng validator, nangyayari ito kapag nabigo ang koneksyon sa sentry

**Solusyon**

1. Gawin ang file na `~/node/bor/bor_config.toml` sa iyong sentry node kasama ang sumusunod na nilalaman:

    ```bash
    [Node.P2P]
    TrustedNodes = ["enode://<enode_id_of_validator_node>"]
    ```

2. Magandang pagkakataon din ito para ilipat sa `~/.bor/data/bor/static-nodes.json` ang listahan ng mga static node na nauna mo nang na-configure dahil mababawasan na ang file na ito sa darating na bersyon ng Bor. Kaya parang ganito ang magiging hitsura ng `~/node/bor/bor_config.toml` file mo:

    ```bash
    [Node.P2P]
    StaticNodes = ["enode://static_node_enode1@ip:port", "enode://static_node_enode2@ip:port", ... ]
    TrustedNodes = ["enode://<enode_id_of_validator_node>"]
    ```

3. Sa `~/node/bor/start.sh`, idagdag ang sumusunod na linya sa Bor invocation command, kasama ang mga natitirang flag na naroon na:

    ```bash
    --config ~/node/bor/bor_config.toml \
    ```

    Pakitandaan ang `\` sa dulo ng linya kung hindi ito ang huling linya ng bor invocation command.

4. Ngayon, i-restart ang Bor: `sudo service bor restart`
5. Sundin ang parehong mga hakbang sa validator node mo at sa halip na `enode_id_of_validator_node`, kailangan mong ibigay ang `enode_id_of_sentry_node` sa `TrustedNodes`.


:::note

Kung hindi gumana ang mga hakbang sa itaas, makipag-ugnayan sa Validator Team para sa tulong. Puwedeng isa itong isyu sa genesis file.

:::

## Nagpapakita ang sentry Bor ng 'Looking for peers' at hindi makahanap ng mga peer {#sentry-bor-shows-looking-for-peers-and-cannot-find-peers}

Puwede itong mangyari kapag nawalan ng koneksyon ang Bor sa iba pang peer. Karaniwan, dapat mong makita ang mga bootnode mo kapag tiningnan mo ang `~/node/bor/start.sh` file. Tingnan kung nakalagay nang tama ang mga bootnode nang walang anumang isyu sa formatting. Kung gumawa ka ng anumang pagbabago sa file, paki-restart ang iyong serbisyo ng Bor at tingnan kung nalutas ang isyu.

Kung magpapatuloy ang isyu, makipag-ugnayan sa team ng suporta sa [Discord](https://discord.com/invite/0xPolygon).

## Nagpapakita ang Bor ng "Failed to prepare header mining at block 0" {#bor-shows-failed-to-prepare-header-mining-at-block-0}

Nangyayari ito dahil sa isang isyu sa formatting sa `~/.bor/data/bor/static-nodes.json` file mo. Tiyakin na walang puwang at walang karagdagang character tulad ng < / > . Kung gumawa ka ng anumang pagbabago sa file, paki-restart ang serbisyo ng Bor at dapat kang makakita ng mga log na nagpi-print.

## Nagpapakita ang Bor ng "30303 or invalid command: /home/ubuntu/.bor/password.txt" {#bor-shows-30303-or-invalid-command-home-ubuntu-bor-password-txt}

Ito ay dahil hindi mo nagawa ang Bor keystore at ang file ng password para dito. Tiyakin na sundin ang lahat ng hakbang mula sa gabay sa pag-setup.

## Nagpapakita ang Bor ng "Impossible reorg, please file an issue" {#bor-shows-impossible-reorg-please-file-an-issue}

Hayaan lang ang mga log na ito. Hindi dapat mahirapan ang node mo nang dahil dito at dapat na awtomatikong malutas ang isyu.

Kung nahihirapan ang node mo dahil dito, makipag-ugnayan sa team ng suporta sa [Discord](https://discord.com/invite/0xPolygon).

## Nagpapakita ang Bor ng "Failed to prepare mining for header" {#bor-shows-failed-to-prepare-mining-for-header}

Hindi error ang mensaheng ito.

Ipinapahiwatig ng mensaheng ito na hindi ang Bor node ang siyang gumagawa ng mga block sa ngayon.

## Nagpapakita ang Bor ng "Invalid Merkle root" o "Retrieved hash chain is Invalid" {#bor-shows-invalid-merkle-root-or-retrieved-hash-chain-is-invalid}

Karaniwan, nangyayari ang isyung ito dahil sa 2 dahilan. Mukhang nag-crash ang Bor mo at nagsimulang ibigay sa iyo ang mga error na ito o nawala ang pagka-sync nito sa Heimdall.

Para lutasin ito, may 2 paraan para gawin ito:

* I-restart ang iyong serbisyo ng Bor at tingnan kung nalutas ang isyu. Karaniwan, dapat malutas ang isyu kapag ni-restart ang iyong serbisyo ng Bor.
* Tingnan kung tumatakbo nang tama ang iyong Heimdall. Kung tumigil ang Heimdall mo, i-restart ang iyong serbisyo ng Heimdall at hayaang magsimulang mag-sync ang Bor mo at dapat malutas nito ang isyu.

Kung hindi nalutas ang isyu, makipag-ugnayan sa team ng suporta sa [Discord](https://discord.com/invite/0xPolygon).

## Nagpapakita ang Bor ng "Address is required as argument" {#bor-shows-address-is-required-as-argument}

Nangangahulugan ito na hindi mo idinagdag ang [signer address](../../glossary#signer-address) mo sa metadata. Puwede mo itong idagdag gamit ang path na ito `/etc/matic/metadata`. Kapag naidagdag na ang address, puwede mo nang i-restart ang serbisyo ng Bor at ayos na dapat ang lahat.

## Nagpapakita ang Bor ng "Failed to unlock account (0x...) No key for given address or file" {#bor-shows-failed-to-unlock-account-0x-no-key-for-given-address-or-file}

Nangyayari ang error na ito dahil hindi tama ang path para sa `password.txt` file.

Para ayusin:

1. Kopyahin ang file ng Bor keystore papunta sa `/etc/bor/dataDir/keystore`
1. Kopyahin ang `password.txt` file papunta sa `/etc/bor/dataDir/`
1. Siguraduhin na naidagdag mo ang tamang address sa `/etc/bor/metadata`

Para sa mga binary:

1. Kopyahin ang file ng Bor keystore papunta sa `~/.bor/keystore/`
1. Kopyahin ang `password.txt` file papunta sa `~/.bor/password.txt`

## Hindi nilalagdaan ng node ang anumang checkpoint {#node-is-not-signing-any-checkpoints}

Ang hindi paglagda ng node mo sa mga checkpoint ay posibleng dulot ng maraming dahilan:

1. Tingnan kung tumatakbo nang tama ang iyong serbisyo ng Heimdall sa mga sentry at validator node mo. Kung tumigil bigla ang serbisyo o nakakakita ka ng anumang error, subukang i-restart ang iyong serbisyo ng Heimdall at tingnan kung bumalik ito sa normal. Kung magpapatuloy ang isyu, makipag-ugnayan sa team ng suporta sa [Discord](https://discord.com/invite/0xPolygon).
1. I-check ang iyong serbisyo ng Bor at tingnan kung ito bigla itong tumigil o may anumang error sa mga log. Subukang i-restart ang iyong serbisyo ng Bor para malutas ang isyung ito. Kung magpapatuloy ang isyu, makipag-ugnayan sa team ng suporta sa [Discord](https://discord.com/invite/0xPolygon).
1. Tingnan kung tumatakbo o hindi ang Heimdall Bridge mo o kung mayroon itong anumang error sa mga log. Subukang i-restart ang serbisyo at tingnan kung malulutas ang isyu. Kung magpapatuloy ang isyu, makipag-ugnayan sa team ng suporta sa [Discord](https://discord.com/invite/0xPolygon).

Kung wala sa mga ito ang isyu, makipag-ugnayan sa team ng suporta sa [Discord](https://discord.com/invite/0xPolygon).

## Paano mag-set up ng validator node sa mainnet? {#how-to-set-up-a-validator-node-on-the-mainnet}

Tingnan ang [Pagsisimula](../validator-index)

## Paano mag-set up ng non-validating node? {#how-to-set-up-a-non-validating-node}

Tingnan ang:

* [Magpatakbo ng Validator Node gamit ang Ansible](../run-validator-ansible)
* [Magpatakbo ng Validator Node mula sa mga Binary](../run-validator-binaries)

## Bakit ko kailangang magpanatili ng ETH sa aking signer account? {#why-do-i-have-to-keep-eth-in-my-signer-account}

Kinakailangan ang ETH sa iyong [signer account](../../glossary#signer-address) para sa pagsusumite ng mga checkpoint sa Ethereum, nangangailangan ng ETH ang lahat ng transaksyon para gamitin bilang gas. Kaya naman kinakailangan ng ETH sa iyong signer account.

## Ang pagse-set up ng node gamit ang Ansible ay nagkaka-error ng "Hindi natagpuan ang host" {#setting-up-a-node-with-ansible-errors-out-with-host-not-found}

Ito ay puwedeng dahil sa may ilang isyu sa formatting ang `inventory.yml` file mo. Itama ang mga ito gamit ang wastong indentation at saka subukan ulit.

## Bilang validator, kailangan ko bang magpatakbo ng sentry at validator node? {#as-a-validator-do-i-need-to-run-both-a-sentry-and-a-validator-node}

Oo, kailangan mong magpatakbo ng sentry at validator node.

Hinihingi ng ecosystem at arkitektura ng Polygon na magpatakbo ka ng sentry + validator setup para matiyak na hindi nalalantad sa publiko ang validator node mo at ang sentry node mo lang ang nalalantad.

Kumukuha ang sentry node mo ng impormasyon / mga block mula sa network at saka nire-relay ang mga ito sa validator para sa pag-validate.

## Ano ang minimum na disk space na kinakailangan para magpatakbo ng Validator node? {#what-is-the-minimum-disk-space-required-to-run-a-validator-node}

Tingnan ang [Mga Kinakailangan ng System para sa Validator Node](../validator-node-system-requirements).

## Nagpapakita ang Bridge ng "Error while fetching mainchain receipt error=" {#bridge-shows-error-while-fetching-mainchain-receipt-error}

Mga normal na log ang mga ito. Huwag gumawa ng kahit ano sa bridge mo. Hayaan itong tumakbo nang ganito.

## Natigil nang matagal ang validator Bor sa isang block {#validator-bor-is-stuck-on-a-block-for-a-long-time}

Nangangahulugan ito na natigil din ang sentry mo dahil kumukuha ng impormasyon ang validator mo mula sa sentry mo.

Paki-check ang mga log ng Bor mo sa iyong sentry at tingnan kung ayos naman ang lahat.

I-restart ang serbisyo ng Bor sa iyong Bor at saka kasabay ring i-restart ang iyong serbisyo ng Bor sa validator mo.

## Ang pag-a-upgrade sa Bor ay nagpapakita ng "build github.com/ethereum/go-ethereum/cmd/geth cannot load hash/maphash: malformed module path "hash/maphash": missing dot in first path element" {#upgrading-bor-shows-build-github-com-ethereum-go-ethereum-cmd-geth-cannot-load-hash-maphash-malformed-module-path-hash-maphash-missing-dot-in-first-path-element}

Ito ay dahil outdated na ang Go Version mo. Ang inirerekomendang bersyon ng Go ay 1.15.x.

## Puwede ba akong magpatakbo ng maraming sentry para sa isang validator? {#can-i-run-multiple-sentries-for-a-validator}

Oo, pwede mong gawin iyon.

## Puwede ba akong magpatakbo ng maraming validator gamit ang parehong key ng signer? {#can-i-run-multiple-validators-using-the-same-signer-key}

Hindi mo puwedeng gawin iyon. Kasalukuyang hindi pinapayagan ng arkitektura ng Polygon ang mga validator na nagpapatakbo ng maraming validator node gamit ang parehong key ng signer.

## Mayroon bang paraan para magpatakbo ng light Bor node? {#is-there-a-way-to-run-a-light-bor-node}

Walang opsyon ng light node sa ngayon.

* [Magpatakbo ng Full Node sa isang binary](../../../develop/network-details/full-node-binaries)
* [Magpatakbo ng Full Node gamit ang Ansible](../../../develop/network-details/full-node-deployment)

## Ano ang kalkulasyon ng porsyento ng uptime sa dashboard sa pag-stake? {#what-is-the-uptime-percentage-calculation-on-the-staking-dashboard}

Kinakalkula ito ayon sa huling 200 checkpoint na isinumite sa mga talagang nilagdaan mo.

## Ano-anong port ang dapat panatilihing nakabukas sa sentry node? {#what-ports-are-to-be-kept-open-on-the-sentry-node}

Kakailanganin mong siguraduhin na bubuksan mo ang mga port 22, 26656, at 30303 sa mundo (0.0.0.0/0) sa firewall ng sentry node.

## Ano ang command para tingnan ang pinakahuling height ng block sa Heimdall? {#what-is-the-command-to-check-the-latest-block-height-on-heimdall}

Puwede mong i-run ang command na ito `curl localhost:26657/status`.

## Ano ang command para tingnan ang pinakahuling height ng block sa Bor? {#what-is-the-command-to-check-the-latest-block-height-on-bor}

I-run ang sumusunod na command:

```sh
curl  http://<your ip>:8545 -X POST -H "Content-Type: application/json" -d '
  {"jsonrpc":"2.0", "id":1, "method":"bor_getSigners", "params":["0x98b3ea"]}
'
```

## Nagpapakita ang Bor ng "ERROR[03-01|13:22:55.320] Block receipts missing, can't freezenumber=9397329 hash="2c38b0...cb41e7"** {#block-receipts-missing-can-t-freezenumber-9397329-hash-2c38b0-cb41e7}

Karaniwang hindi ito error at dapat na malutas nang mag-isa.

## Mga standard na command sa pag-upgrade para sa Heimdall {#standard-upgrade-commands-for-heimdall}

```sh
cd ~/heimdall
git pull
git checkout <branch tag>
make install
sudo service heimdalld restart
```

Ang pinakabagong bersyon, ang [Heimdall v.0.2.11](https://github.com/maticnetwork/heimdall/releases/tag/v0.2.11), ay naglalaman ng ilang pagpapahusay gaya ng:
1. Paglilimita ng data size sa mga transkasyon ng pag-sync ng state sa:
    * **30Kb** kapag kinakatawan sa **bytes**
    * **60Kb** kapag kinakatawan bilang **string**.
2. Pagdaragdag sa **tagal ng pagkaantala** sa pagitan ng mga event ng kontrata ng iba't ibang validator para matiyak na hindi kaagad napupuno ang mempool sakaling magkaroon ng napakaraming event na puwedeng makasagabal sa pag-usad ng chain.

Ipinapakita ng sumusunod na halimbawa kung paano pinaghihigpitan ang laki ng data:

```
Data - "abcd1234"
Length in string format - 8
Hex Byte representation - [171 205 18 52]
Length in byte format - 4
```

## Mga standard na command sa pag-upgrade para sa Bor {#standard-upgrade-commands-for-bor}

Ito ang mga command para i-upgrade ang Bor:

```sh
cd ~/bor
git pull
git checkout <branch tag>
sudo service bor stop
make bor-all
sudo service bor start
```

## Paano ko idi-delete ang mga remnant ng Heimdall at Bor? {#how-do-i-delete-remnants-of-heimdall-and-bor}

Kung gusto mong i-delete ang mga remnant ng Heimdall at Bor, puwede mong i-run ang mga sumusunod na command:

Bor:

Para sa Linux package:

```sh
sudo dpkg -i matic-bor
```

At i-delete ang directory ng Bor:

```sh
sudo rm -rf /etc/bor
```

Para sa mga Binary:

```sh
sudo rm -rf /etc/bor
```

At:

```sh
sudo rm /etc/heimdall
```

## Nagpapakita ang Bridge ng "Object "start" is unknown" {#bridge-shows-object-start-is-unknown}

Tingnan ang `which bridge` — kung `/usr/sbin/bridge` ito, hindi mo pinapatakbo ang tamang "bridge" program.

Subukan na lang ang `~/go/bin/bridge` (o `$GOBIN/bridge)`

## Error: Hindi ma-unmarshall ang config Error 1 (mga) error ang nagde-decode {#error-unable-to-unmarshall-config-error-1-error-s-decoding}

Buong error:

```
'' has invalid keys: clerk_polling_interval, matic_token, span_polling_interval, stake_manager_contract, stakinginfo_contract
```

Kadalasan itong nangyayari dahil may mga typo, ilang nawawalang bahagi, o isang lumang config file na isang pa ring remnant. Kakailanganin mong i-clear ang lahat ng remnant at saka subukang i-set up ito ulit.

## Para itigil ang mga serbisyo ng Heimdall at Bor {#to-stop-heimdall-and-bor-services}

**Para sa mga Linux package**:

Itigil ang Heimdall: `sudo service heimdalld stop`

Itigil ang Bor: `sudo service bor stop` o

1. `ps -aux | grep bor`. Kunin ang PID para sa Bor at pagkatapos ay i-run ang sumusunod na command.
1. `sudo kill -9 PID`

**Para sa mga Binary**:

Itigil ang Heimdall: `pkill heimdalld`

Itigil ang Bridge: `pkill heimdalld-bridge`

Itigil ang Bor: Pumunta sa CS-2001/bor at pagkatapos ay i-run ang, `bash stop.sh`

## Para alisin ang mga directory ng Heimdall at Bor {#to-remove-heimdall-and-bor-directories}

**Para sa mga Linux package**:

I-delete ang Heimdall: `sudo rm -rf /etc/heimdall/*`

I-delete ang Bor: `sudo rm -rf /etc/bor/*`

**Para sa mga Binary**:

I-delete ang Heimdall: `sudo rm -rf ~/.heimdalld/`

I-delete ang Bor: `sudo rm -rf ~/.bor`

## Listahan ng mga karaniwang command {#list-of-common-commands}

### Saan mahahanap ang genesis file ng Heimdall {#where-to-find-heimdall-genesis-file}

`$CONFIGPATH/heimdall/config/genesis.json`

### Saan mahahanap ang `heimdall-config.toml`

`/etc/heimdall/config/heimdall-config.toml`

### Saan mahahanap ang `config.toml`

`/etc/heimdall/config/config.toml`

### `Where to find heimdall-seeds.txt`

`$CONFIGPATH/heimdall/heimdall-seeds.txt`

### Simulan ang Heimdall {#start-heimdall}

`$ sudo service heimdalld start`

### Simulan ang rest-server ng Heimdall {#start-heimdall-rest-server}

`$ sudo service heimdalld-rest-server start`

### Simulan ang bridge-server ng Heimdall {#start-heimdall-bridge-server}

`$ sudo service heimdalld-bridge start`

### Mga log ng Heimdall {#heimdall-logs}

`/var/log/matic-logs/`

### Saan mahahanap ang genesis file ng Bor {#where-to-find-bor-genesis-file}

`$CONFIGPATH/bor/genesis.json`

### Simulan ang Bor {#start-bor}

`sudo service bor start`

### Tingnan ang mga log ng Heimdall {#check-heimdall-logs}

`tail -f heimdalld.log`

### Tingnan ang rest-server ng Heimdall {#check-heimdall-rest-server}

`tail -f heimdalld-rest-server.log`

### Tingnan ang mga log ng bridge ng Heimdall {#check-heimdall-bridge-logs}

`tail -f heimdalld-bridge.log`

### Tingnan ang mga log ng Bor {#check-bor-logs}

`tail -f bor.log`

### Tapusin ang proseso ng Bor {#kill-bor-process}

**Para sa Linux**

1. `ps -aux | grep bor`. Kunin ang PID para sa Bor at pagkatapos ay i-run ang sumusunod na command.
1. `sudo kill -9 PID`

**Para sa mga binary**

Pumunta sa `CS-2003/bor` at pagkatapos ay i-run ang, `bash stop.sh`

### Pag-diagnose kung ano ang mali sa isang node {#diagnosing-what-went-wrong-in-a-node}

Puwede mong gamitin ang [script na ito](https://github.com/maticnetwork/launch/tree/master/scripts/node_diagnostics.sh) para regular na tingnan ang status sa pag-sync ng node mo.
