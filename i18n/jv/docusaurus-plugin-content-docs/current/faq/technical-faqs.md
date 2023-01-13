---
id: technical-faqs
title: Pitakonan Umum Teknis
description: Mbangun aplikasi blockchain panjenengan sabanjure ing Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

### 1. Apa kunci privat kanggo Heimdall lan Bor keystore padha? {#1-are-the-private-keys-same-for-heimdall-and-bor-keystore}
Ya, kunci privat sing digunakake kanggo ngasilake kunci Validator lan Bor Keystore iku padha. Kunci privat sing digunakake ing conto iki yaiku alamat ETH Dhompet panjenengan papan kanggo nyimpen token testnet Polygon panjenangan.

### 2. Dhaptar Prentah Umum {#2-list-of-common-commands}

Saiki kita duwe dhaptar sing gampang panjenengan gunakake nganggo paket Linux. Kita bakal terus nganyarake dhaptar iki kanthi rutin supaya luwih gampang.

**Kanggo Paket Linux**

#### A. Ing ngendi nemokake file genesis heimdall {#a-where-to-find-heimdall-genesis-file}

`$CONFIGPATH/heimdall/config/genesis.json`

#### B. Ing ngendi nemokake heimdall-config.toml {#b-where-to-find-heimdall-config-toml}

`/etc/heimdall/config/heimdall-config.toml`

#### C. Ing ngendi nemokake config.toml {#c-where-to-find-config-toml}

`/etc/heimdall/config/config.toml`

#### D. Ing ngendi nemokake heimdall-seeds.txt {#d-where-to-find-heimdall-seeds-txt}

`$CONFIGPATH/heimdall/heimdall-seeds.txt`

#### E. Miwiti Heimdall {#e-start-heimdall}

`$ sudo service heimdalld start`

#### F. Miwiti rest-server Heimdall {#f-start-heimdall-rest-server}

`$ sudo service heimdalld-rest-server start`

#### G. Miwiti bridge-server Heimdall {#g-start-heimdall-bridge-server}

`$ sudo service heimdalld-bridge start`

#### H. Log Heimdall {#h-heimdall-logs}

`/var/log/matic-logs/`

#### I. Ing ngendi nemokake file genesis Bor {#i-where-to-find-bor-genesis-file}

`$CONFIGPATH/bor/genesis.json`

#### J. Miwiti Bor {#j-start-bor}

`sudo service bor start`

#### K Mriksa log heimdall {#k-check-heimdall-logs}

`tail -f heimdalld.log`

#### L. Mriksa rest-server Heimdall {#l-check-heimdall-rest-server}

`tail -f heimdalld-rest-server.log`

#### M. Mriksa log jembatan Heimdall {#m-check-heimdall-bridge-logs}

`tail -f heimdalld-bridge.log`

#### N. Mriksa log bor {#n-check-bor-logs}

`tail -f bor.log`

#### O. Ngendhegake proses Bor {#o-kill-bor-process}

**Kanggo linux**:

1. `ps -aux | grep bor`. Mundhuta PID kanggo Bor banjur lakokna printah ing ngisor iki.
2. `sudo kill -9 PID`

**Kanggo Binari**:

Bukak `CS-2003/bor`lan lakokna, `bash stop.sh`

### 3. Error: Gagal mbukak kunci akun (0x...) Ora ana kunci kanggo alamat utawa file sing diwenehake {#3-error-failed-to-unlock-account-0x-no-key-for-given-address-or-file}

Error iki kedadeyan amarga path file password.txt ora bener. Panjenengan bisa nindakake langkah ing ngisor iki kanggo mbenerake:

Error iki kedadeyan amarga path file password.txt lan Keystore ora bener. Panjenengan bisa nindakake langkah ing ngisor iki kanggo mbenerake:

1. Salin file keystore bor menyang

 /etc/bor/dataDir/keystore

2. Lan password.txt menyang

 /etc/bor/dataDir/

3. Pesthekake panjenengan wis nambahake alamat sing bener `/etc/bor/metadata`

Kanggo Binari:

1. Salin file Bor keystore menyang:

`~/.bor/keystore/`

2. Lan password.txt menyang

`~/.bor/password.txt`


### 4. Error: Salah Block.Header.AppHash. Dikarepake xxxx {#4-error-wrong-block-header-apphash-expected-xxxx}

Error iki biasane kedadeyan nalika layanan Heimdall macet ing blok; ora ana cara mbalikake sing ana ing Heimdall.

Kanggo ngatasi masalah iki, panjenengan kudu ngreset kabeh Heimdall:

```bash
    sudo service heimdalld stop

    heimdalld unsafe-reset-all
```

Sawise iku, panjenengan kudu nyelarasake saka snapshot maneh:

```bash
    wget -c <Snapshot URL>

    tar -xzvf <snapshot file> -C <HEIMDALL_DATA_DIRECTORY>

```

Banjur, wiwiti layanan Heimdall maneh.


### 5. Saka ngendi aku nggawe kunci API? {#5-from-where-do-i-create-the-api-key}

Panjenengan bisa ngakses tautan iki: [https://infura.io/register](https://infura.io/register). Pesthekake panjenengan wis nyiyapake akun lan proyek, panjenengan salin kunci API kanggo Ropsten lan dudu Mainnet.

Mainnet dipilih kanthi gawan.

### 6. Heimdall ora bisa digunakake. Aku ngalami error Panik {#6-heimdall-isn-t-working-i-m-getting-a-panic-error}

**Error Sabenere**: Heimdalld-ku ora bisa digunakake. Ing log baris pisanan yaiku:
panik: db_backend leveldb ora dingerteni, samesthine goleveldb utawa memdb utawa fsdb

Ganti config dadi `goleveldb`ing config.toml


### 7. Kepiye carane mbusak remnants Heimdall lan Bor? {#7-how-do-i-delete-remnants-of-heimdall-and-bor}

Yen panjenengan pengin mbusak remnants Heimdall lan Bor, panjenengan bisa mbukak printah ing ngisor iki
Bor:

Kanggo paket Linux:

```$ sudo dpkg -i matic-bor```

Lan busak Direktori Bor:

```$ sudo rm -rf /etc/bor```

Kanggo Binari:

```$ sudo rm -rf /etc/bor```

Lan

```$ sudo rm /etc/heimdall```


### 8. Pira cacahe validator sing bisa aktif bebarengan? {#8-how-many-validators-can-be-active-concurrently}

Bisa nganti 100 validator aktif bebarengan. Kita uga bakal nggawa luwih akeh peserta yen wis tekan watesan ing tengah-tengah prastawa. Elinga yen validator aktif biasane sing nduwe uptime dhuwur. Peserta kanthi downtime dhuwur bakal dipeksa metu.

### 9. Pira akehe stake sing kudu dak pasang? {#9-how-much-should-i-stake}

"Akehe stake" lan "akehe ongkos heimdall" - kudune pira?

Paling ora perlu 10 token Matic kanggo akehe stake, dene ongkos heimdall kudu luwih saka 10. Contone, akehe stake panjenengan 400 banjur ongkos heimdall kudu 20. Disaranake supaya ongkos Heimdall tetep 20.

Nanging, elinga yen nilai sing dilebokake ing cacahe stake lan fee heimdal kudu dilebokake ing 18 desimal

Contone,

    heimdallcli stake --staked-amount 400000000000000000000 --fee-amount 1000000000000000000 --validator 0xf8d1127780b89f167cb4578935e89b8ea1de774f


### 10. Aku dipilih dadi validator nanging alamat ETH-ku salah. Apa sing kudu tak lakokake? {#10-i-was-selected-to-become-a-validator-but-my-eth-address-was-incorrect-what-do-i-do}

Yen panjenengan duwe akses menyang alamat ETH sing dikirim sadurunge panjenengan bisa nransfer token Test saka akun kasebut menyang akun sing saiki. Banjur panjenengan bisa miwiti proses nyetel node.

Yen panjenengan ora duwe akses menyang alamat ETH kasebut, kita ora bakal transfer token panjenangan pisah-pisah. Panjenengan bisa ndhaptar maneh ing formulir kasebut kanthi alamat ETH sing bener.

### 11. Aku ngalami error miwiti jembatan {#11-i-m-getting-an-error-starting-the-bridge}

**Error**: Obyek "start" ora dikenal, mangga dicoba "bridge help". Apa apik yen nglirwakake iki?

Priksa "jembatan sing endi" - Yen iki `/usr/sbin/bridge`panjenengan ora mbukak program "jembatan" sing bener.

Coba `~/go/bin/bridge`tinimbang `(or $GOBIN/bridge)`


### 12. Aku ngalami error dpkg {#12-i-m-getting-dpkg-error}

**Error**: "dpkg: error processing archive matic-heimdall_1.0.0_amd64.deb (--install): trying to overwrite '/heimdalld-rest-server.service', which is also in package matic-node 1.0.0"

Iki utamane kedadeyan amarga instalasi Matic sadurunge ing mesin panjenengan. Kanggo ngatasi, panjenengan bisa nglakokake:

`sudo dpkg -r matic-node`


### 13. Aku durung paham Kunci Privat sing endi sing kudu ditambah nalika aku ngasilake kunci validator {#13-i-m-not-clear-on-which-private-key-should-i-add-when-i-generate-validator-key}

Kunci privat sing digunakake yaiku alamat ETH Dhompet panjenangan papan panggone Token testnet Polygon panjenangan disimpen. Panjenengan bisa ngrampungake panyiapan kanthi sak pasangan kunci umum-privat ditaleni menyang alamat sing dikirim ing formulir.


### 14. Apa ana cara kanggo ngerti yen Heimdall diselarasake? {#14-is-there-a-way-to-know-if-heimdall-is-synced}

Panjenengan bisa mbukak printah ing ngisor iki kanggo mriksa:

```$ curl [http://localhost:26657/status](http://localhost:26657/status)```

Priksa nilai catching_up. Yen salah ateges kabeh node wis diselarasake.


### 15. Yen ana sing dadi 10 staker paling dhuwur, kepiye carane bakal nampa ganjaran MATIC ing pungkasan? {#15-what-if-someone-become-a-top-10-staker-how-he-will-receive-his-matic-reward-at-the-end}

Ganjaran tahap 1 ora adhedhasar stake. Pirsanana https://blog.matic.network/counter-stake-stage-1-stake-on-the-beach-full-details-matic-network/ kanggo rincian ganjaran. Peserta sing duwe stake dhuwur ora otomatis entuk ganjaran ing tahap iki.


### 16. Apa sing kudune dadi versi heimdall-ku? {#16-what-should-be-my-heimdall-version}

Kanggo mriksa versi Heimdall, panjenengan bisa mbukak:

```heimdalld version```

Versi Heimdall sing bener kanggo tahap 1 kudune `heimdalld version is beta-1.1-rc1-213-g2bfd1ac`


### 17. Nilai kaya apa sing kudu dak tambahake ing cacahe stake lan ongkos? {#17-what-values-should-i-add-in-the-stake-amount-and-fee-amount}

Paling ora perlu 10 token Matic kanggo akehe stake, dene ongkos heimdall kudu luwih saka 10. Contone, akehe stake panjenengan 400 banjur ongkos heimdall kudu 20. Disaranake supaya ongkos Heimdall tetep 20.

Nanging, elinga yen nilai sing dilebokake ing cacahe stake lan fee heimdal kudu dilebokake ing 18 desimal

Contone,

    heimdallcli stake --staked-amount 400000000000000000000 --fee-amount 1000000000000000000 --validator 0xf8d1127780b89f167cb4578935e89b8ea1de774f


### 18. Apa bedane `~.heimsdall`lan `/etc/heimsdall?`

`~/.heimsdall` iku dir heimdall nalika sampeyan nggunakake cara instalasi binari. `/etc/heimdall` iku kanggo cara instalasi paket Linux.


### 19. Nalika aku transaksi stake, Aku ngalami error "Gas Ngluwihi" {#19-when-i-make-the-stake-transaction-i-m-getting-gas-exceeded-error}

Error iki bisa kedadeyan amarga format cacahe stake utawa ongkos. Nilai sing dilebokake ing printah stake kudu 18 desimal.

Nanging, elinga yen nilai sing dilebokake ing cacahe stake lan fee heimdal kudu dilebokake ing 18 desimal

Contone,

    heimdallcli stake --staked-amount 400000000000000000000 --fee-amount 1000000000000000000 --validator 0xf8d1127780b89f167cb4578935e89b8ea1de774f


### 20. Kapan aku entuk kasempatan dadi Validator? {#20-when-will-i-get-a-chance-to-become-a-validator}

Kita terus nambah validator sajrone acara Tahap 1. Kita bakal ngetokake dhaptar validator eksternal anyar saka sithik. Dhaptar iki bakal diumumake ing saluran Discord.


### 21. Ing ngendi aku bisa nemokake lokasi info akun Heimdall? {#21-where-can-i-find-heimdall-account-info-location}

Kanggo binari:

    ~/.heimdalld/config folder

Kanggo paket Linux:

    /etc/heimdall/config


### 22. Ing file endi aku nambahake kunci API? {#22-which-file-do-i-add-the-api-key-in}

Sawise panjenangan nggawe kunci API sampeyan kudu nambahake kunci API ing file.`heimdall-config.toml` iki.


### 23. Ing file endi aku nambahake persistent_peers? {#23-which-file-do-i-add-the-persistent_peers}

Panjenengan bisa nambahake persistent_peers ing file ing ngisor iki:

    ~/.heimdalld/config/config.toml


### 24. "Apa panjenengan ngreset Tendermint tanpa ngreset data aplikasi?" {#24-did-you-reset-tendermint-without-resetting-your-application-s-data}

Ing kasus kaya mengkono panjenengan bisa ngreset data config heimdall lan nyoba nglakokake instalasi maneh.

    $ heimdalld unsafe-reset-all
    $ rm -rf $HEIMDALLDIR/bridge


### 25. Error: Unable to unmarshall config Error 1 error(s) decoding {#25-error-unable-to-unmarshall-config-error-1-error-s-decoding}

Error: `* '' has invalid keys: clerk_polling_interval, matic_token, span_polling_interval, stake_manager_contract, stakinginfo_contract`

Iki kedadeyan biasane amarga nalika ana kesalahan ketik, utawa ana sawetara bagean sing ilang utawa ana file konfigurasi lawas. Panjenengan kudu mbusak kabeh remnants banjur nyoba nyetel maneh.

### 26. Kanggo mungkasi layanan Heimdall lan Bor {#26-to-stop-heimdall-and-bor-services}

**Kanggo paket Linux**:

Ngendhegake Heimdall: `sudo service heimdalld stop`

Ngendhegake Bor: `sudo service bor stop`utawa

1. `ps -aux | grep bor`. Mundhuta PID kanggo Bor banjur lakokna printah ing ngisor iki.
2. `sudo kill -9 PID`

**Kanggo Binari**:

Ngendhegake Heimdall: `pkill heimdalld`

Ngendhegake Jembatan: `pkill heimdalld-bridge`

Ngendhegake Bor: Bukak CS-2001/bor banjur lakokake, `bash stop.sh`

### 27. Kanggo mbusak direktori Heimdall lan Bor {#27-to-remove-heimdall-and-bor-directories}

**Kanggo paket Linux**:
Mbusak Heimdall: `sudo rm -rf /etc/heimdall/*`

Mbusak Bor: `sudo rm -rf /etc/bor/*`

**Kanggo Binari**:

Mbusak Heimdall: `sudo rm -rf ~/.heimdalld/`

Mbusak Bor: `sudo rm -rf ~/.bor`

### 28. Apa sing kudu ditindakake nalika ngalami error "Wrong Block.Header.AppHash." {#28-what-to-do-when-you-get-wrong-block-header-apphash-error}

Error iki biasane kedadeyan amarga panjalukan Infura kesel. Nalika panjenengan nyetel node ing Polygon, panjenengan nambahake Kunci Infura menyang file Config (Heimdall). Miturut gawan, panjenengan diidini 100k Panjalukan saben dina, yen nganti tekan watesan iki, panjenengan bakal ngadhepi masalah kuwi. Kanggo ngatasi masalah iki, panjenengan bisa nggawe kunci API anyar lan nambahake menyang file `config.toml`iki.