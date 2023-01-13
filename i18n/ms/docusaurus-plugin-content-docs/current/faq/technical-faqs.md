---
id: technical-faqs
title: Soalan Lazim Teknikal
description: Bangunkan aplikasi blok rantai anda yang seterusnya di Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

### 1. Adakah kekunci peribadi sama untuk kekunci simpan Heimdall dan Bor? {#1-are-the-private-keys-same-for-heimdall-and-bor-keystore}
Ya, kekunci peribadi yang digunakan untuk menjana kunci Pengesah dan Kekunci simpan Bor adalah sama. Kekunci peribadi yang digunakan dalam kejadian ini ialah alamat dompet ETH anda tempat token testnet Polygon Qanda disimpan.

### 2. Senarai Arahan Biasa {#2-list-of-common-commands}

Pada masa ini kami mempunyai senarai mudah untuk menyelam untuk anda untuk pakej Linux. Kami akan terus mengemas kini senarai ini dengan kerap untuk kemudahan yang lebih.

**Untuk pakej Linux**

#### A. Di mana untuk mencari fail genesis heimdall {#a-where-to-find-heimdall-genesis-file}

`$CONFIGPATH/heimdall/config/genesis.json`

#### B. Di mana untuk mencari heimdall-config.toml {#b-where-to-find-heimdall-config-toml}

`/etc/heimdall/config/heimdall-config.toml`

#### B. Di mana untuk mencari config.toml {#c-where-to-find-config-toml}

`/etc/heimdall/config/config.toml`

#### B. Di mana untuk mencari heimdall-seeds.txt {#d-where-to-find-heimdall-seeds-txt}

`$CONFIGPATH/heimdall/heimdall-seeds.txt`

#### E. Mulakan Heimdall {#e-start-heimdall}

`$ sudo service heimdalld start`

#### F. Mulakan pelayan rehat Heimdall {#f-start-heimdall-rest-server}

`$ sudo service heimdalld-rest-server start`

#### G. Mulakan pelayan penghubung Heimdall {#g-start-heimdall-bridge-server}

`$ sudo service heimdalld-bridge start`

#### H. Log Heimdall {#h-heimdall-logs}

`/var/log/matic-logs/`

#### I. Di mana untuk mencari fail genesis Bor {#i-where-to-find-bor-genesis-file}

`$CONFIGPATH/bor/genesis.json`

#### J. Mulakan Bor {#j-start-bor}

`sudo service bor start`

#### K. Semak log heimdall {#k-check-heimdall-logs}

`tail -f heimdalld.log`

#### L. Semak pelayan semak Heimdall {#l-check-heimdall-rest-server}

`tail -f heimdalld-rest-server.log`

#### M. Semak log penghubung Heimdall {#m-check-heimdall-bridge-logs}

`tail -f heimdalld-bridge.log`

#### N. Semak log bor {#n-check-bor-logs}

`tail -f bor.log`

#### O. Proses Bunuh Bor {#o-kill-bor-process}

**Untuk linux**:

1. `ps -aux | grep bor`. Dapatkan PID untuk Bor dan kemudian jalankan arahan berikut.
2. `sudo kill -9 PID`

**Untuk Binari**:

Pergi `CS-2003/bor`dan kemudian jalankan,`bash stop.sh`

### 3. Ralat: Gagal membuka kunci akaun (0x...) Tiada kekunci untuk alamat atau fail yang diberikan {#3-error-failed-to-unlock-account-0x-no-key-for-given-address-or-file}

Ralat ini berlaku kerana laluan untuk fail password.txt tidak betul. Anda boleh mengikuti langkah-langkah di bawah untuk membetulkannya:

Ralat ini berlaku kerana laluan untuk fail password.txt dan Kekunci simpan tidak betul. Anda boleh mengikuti langkah-langkah di bawah untuk membetulkannya:

1. Salin fail kekunci simpan bor ke

 /etc/bor/dataDir/keystore

2. Dan password.txt to

 /etc/bor/dataDir/

3. Pastikan anda telah menambah alamat yang betul dalam `/etc/bor/metadata`

Untuk Binari:

1. Salin fail kekunci simpan Bor ke:

`~/.bor/keystore/`

2. Dan password.txt to

`~/.bor/password.txt`


### 4. Ralat: Blok Salah.Header.AppHash. Dijangka xxxx {#4-error-wrong-block-header-apphash-expected-xxxx}

Ralat ini biasanya berlaku apabila perkhidmatan Heimdall tersekat pada blok; tiada kaedah pembalikan yang tersedia di Heimdall.

Untuk menyelesaikan masalah ini, anda perlu menetapkan semula Heimdall sepenuhnya:

```bash
    sudo service heimdalld stop

    heimdalld unsafe-reset-all
```

Selepas itu, anda hendaklah menyegerakkan dari syot kilat semula:

```bash
    wget -c <Snapshot URL>

    tar -xzvf <snapshot file> -C <HEIMDALL_DATA_DIRECTORY>

```

Kemudian, mulakan perkhidmatan Heimdall sekali lagi.


### 5. Dari mana saya boleh mencipta kekunci API? {#5-from-where-do-i-create-the-api-key}

Anda boleh mengakses pautan ini: [https://infura.io/register](https://infura.io/register). Pastikan bahawa sebaik sahaja anda telah menyediakan akaun dan projek anda, anda menyalin kekunci API untuk Ropsten dan bukan Mainnet.

Mainnet terpilih secara lalai.

### 6. Heimdall tidak berfungsi. Saya mendapat ralat Panik {#6-heimdall-isn-t-working-i-m-getting-a-panic-error}

**Ralat Sebenar**: Heimdall saya tidak berfungsi. Dalam log baris pertama ialah: panik: db_backend leveldb tidak diketahui, dijangka sama ada goleveldb atau memdb atau fsdb

Tukar konfigurasi kepada `goleveldb`dalam config.toml


### 7. Bagaimanakah cara saya memadamkan sisa Heimdall dan Bor? {#7-how-do-i-delete-remnants-of-heimdall-and-bor}

Jika anda ingin memadamkan sisa Heimdall dan Bor maka anda boleh menjalankan arahan berikut Bor:

Untuk pakej Linux:

```$ sudo dpkg -i matic-bor```

Dan padamkan Direktori Bor:

```$ sudo rm -rf /etc/bor```

Untuk Binari:

```$ sudo rm -rf /etc/bor```

Dan

```$ sudo rm /etc/heimdall```


### 8. Berapakah bilangan pengesah yang boleh aktif secara serentak? {#8-how-many-validators-can-be-active-concurrently}

Akan ada sehingga 100 pengesah aktif pada satu masa. Kami akan membawa lebih ramai peserta jika had telah dicapai pada pertengahan acara juga. Ambil perhatian bahawa pengesah aktif kebanyakannya adalah mereka yang masa operasinya adalah tinggi. Peserta yang mempunyai masa henti yang tinggi akan dipaksa keluar.

### 9. Berapa banyak yang perlu saya pegangkan? {#9-how-much-should-i-stake}

"amaun pegangan" dan "amaun-bayaran-heimdall" - berapakah amaun yang sepatutnya?

Sekurang-kurangnya 10 token Matic diperlukan untuk amaun pegangan manakala bayaran heimdall hendaklah lebih besar daripada 10. Contohnya, amaun pegangan anda ialah 400 maka bayaran heimdall hendaklah 20. Kami mencadangkan untuk mengekalkan bayaran Heimdall sebagai 20.

Walau bagaimanapun, sila ambil perhatian bahawa nilai yang dimasukkan dalam amaun pegangan dan amaun bayaran heimdal perlu dimasukkan dalam 18 perpuluhan

Sebagai contoh,

    pegangan heimdall --amaun dipegangkan 400000000000000000000 --amaun bayaran 1000000000000000000 --pengesah 0xf8d1127780b89f167cb4578935e89b8ea1de774f

### 10. Saya telah terpilih untuk menjadi pengesah tetapi alamat ETH saya tidak betul. Apakah yang saya buat? {#10-i-was-selected-to-become-a-validator-but-my-eth-address-was-incorrect-what-do-i-do}

Jika anda mempunyai akses kepada alamat ETH yang anda serahkan lebih awal, maka anda boleh pindahkan token Ujian daripada akaun tersebut ke akaun semasa. Dan kemudian anda boleh memulakan proses anda untuk menyediakan nod anda.

Jika anda tidak ada akses kepada alamat ETH itu, kami tidak akan memindahkan token anda secara berasingan. Anda boleh mendaftar semula dalam borang sekali lagi dengan alamat ETH yang betul.

### 11. Saya mendapat ralat semasa memulakan penghubung {#11-i-m-getting-an-error-starting-the-bridge}

**Ralat**: Objek "mula" tidak diketahui, cuba "bantuan penghubung". Adakah masih boleh mengabaikan perkara ini?

Semak "penghubung mana" - `/usr/sbin/bridge`jika anda tidak menjalankan program "penghubung" yang betul.

Cuba`~/go/bin/bridge` sebaliknya`(or $GOBIN/bridge)`


### 12. Saya mendapat ralat dpkg {#12-i-m-getting-dpkg-error}

**Ralat**: "dpkg: ralat memproses arkib matic-heimdall_1.0.0_amd64.deb (--pasang): cuba menulis ganti '/heimdalld-rest-server.service', yang juga terdapat dalam pakej nod matic 1.0.0"

Ini berlaku terutamanya kerana pemasangan Matic pada mesin anda sebelum ini. Untuk menyelesaikannya anda boleh jalankan:

`sudo dpkg -r matic-node`


### 13. Saya tidak jelas mengenai Kekunci Peribadi yang perlu saya tambahkan apabila saya menjana kekunci pengesah {#13-i-m-not-clear-on-which-private-key-should-i-add-when-i-generate-validator-key}

Kekunci Peribadi yang akan digunakan ialah alamat Dompet ETH anda tempat Token testnet Polygon anda disimpan. Anda boleh melengkapkan persediaan dengan satu pasangan kekunci awam-swasta yang terikat pada alamat yang diserahkan pada borang.


### 14. Adakah terdapat cara untuk mengetahui sama ada Heimdall disegerakkan? {#14-is-there-a-way-to-know-if-heimdall-is-synced}

Anda boleh menjalankan arahan berikut untuk menyemaknya:

```$ curl [http://localhost:26657/status](http://localhost:26657/status)```

Semak nilai catching_up. Jika ia palsu maka nod semuanya disegerakkan.


### 15. Bagaimana jika seseorang menjadi Pegangan 10 Teratas, bagaimana dia akan menerima ganjaran MATICnya pada akhirnya? {#15-what-if-someone-become-a-top-10-staker-how-he-will-receive-his-matic-reward-at-the-end}

Ganjaran peringkat 1 tidak berdasarkan pegangan. Sila rujuk https://blog.matic.network/counter-stake-stage-1-stake-on-the-beach-full-details-matic-network/ untuk butiran ganjaran. Peserta yang mempunyai pegangan tinggi tidak layak secara automatik untuk ganjaran dalam peringkat ini.


### 16. Apakah versi heimdall saya yang sepatutnya? {#16-what-should-be-my-heimdall-version}

Untuk semak versi Heimdall anda, anda hanya boleh jalankan:

```heimdalld version```

Versi Heimdall yang betul untuk peringkat 1 sepatutnya`heimdalld version is beta-1.1-rc1-213-g2bfd1ac`


### 17. Apakah nilai yang perlu saya tambah dalam amaun pegangan dan amaun bayaran? {#17-what-values-should-i-add-in-the-stake-amount-and-fee-amount}

Sekurang-kurangnya 10 token Matic diperlukan untuk amaun pegangan manakala bayaran heimdall hendaklah lebih besar daripada 10. Contohnya, amaun pegangan anda ialah 400 maka bayaran heimdall hendaklah 20. Kami mencadangkan untuk mengekalkan bayaran Heimdall sebagai 20.

Walau bagaimanapun, sila ambil perhatian bahawa nilai yang dimasukkan dalam amaun pegangan dan amaun bayaran heimdal perlu dimasukkan dalam 18 perpuluhan

Sebagai contoh,

    pegangan heimdall --amaun dipegangkan 400000000000000000000 --amaun bayaran 1000000000000000000 --pengesah 0xf8d1127780b89f167cb4578935e89b8ea1de774f

### 18. Apakah perbezaan antara `~.heimsdall`dan `/etc/heimsdall?`

`~/.heimsdall`ialah dir heimdall apabila anda menggunakan kaedah pemasangan binari. `/etc/heimdall` adalah untuk kaedah pemasangan pakej Linux.


### 19. Apabila saya membuat transaksi pegangan, saya mendapat ralat "Gas Melebihi" {#19-when-i-make-the-stake-transaction-i-m-getting-gas-exceeded-error}

Ralat ini mungkin berlaku kerana format amaun pegangan atau bayaran. Nilai yang dimasukkan semasa parahan pegangan perlu mempunyai 18 perpuluhan.

Walau bagaimanapun, sila ambil perhatian bahawa nilai yang dimasukkan dalam amaun pegangan dan amaun bayaran heimdal perlu dimasukkan dalam 18 perpuluhan

Sebagai contoh,

    pegangan heimdall --amaun dipegangkan 400000000000000000000 --amaun bayaran 1000000000000000000 --pengesah 0xf8d1127780b89f167cb4578935e89b8ea1de774f

### 20. Bilakah saya akan mendapat peluang untuk menjadi Pengesah? {#20-when-will-i-get-a-chance-to-become-a-validator}

Kami sedang menambah pengesah secara berperingkat sepanjang acara Peringkat 1. Kami akan mengeluarkan senarai pengesah luaran baharu secara beransur-ansur. Senarai ini akan diumumkan di saluran Discord.


### 21. Di manakah saya boleh mencari lokasi maklumat akaun Heimdall? {#21-where-can-i-find-heimdall-account-info-location}

Untuk binari:

    folder ~/.heimdalld/config
Untuk pakej Linux:

    /etc/heimdall/config

### 22. Fail manakah saya menambah kekunci API? {#22-which-file-do-i-add-the-api-key-in}

Setelah anda membuat kekunci API, anda perlu menambahkan kekunci API dalam `heimdall-config.toml` fail.


### 23. Fail manakah yang saya tambah persisten_peers? {#23-which-file-do-i-add-the-persistent_peers}

Anda boleh menambah persistent_peers dalam fail berikut:

    ~/.heimdalld/config/config.toml

### 24. “Adakah anda menetapkan semula Tendermint tanpa menetapkan semula data aplikasi anda?” {#24-did-you-reset-tendermint-without-resetting-your-application-s-data}

Dalam kes sedemikian, anda boleh menetapkan semula data konfigurasi heimdall dan cuba jalankan pemasangan sekali lagi.

    $ heimdalld tidak selamat-set-semula-semua HEIMDALLDIR/penghubung

### 25. Ralat: Tidak dapat menyahmarshall konfigurasi Ralat 1 ralat penyahkodan {#25-error-unable-to-unmarshall-config-error-1-error-s-decoding}

Ralat:`* '' has invalid keys: clerk_polling_interval, matic_token, span_polling_interval, stake_manager_contract, stakinginfo_contract`

Ini berlaku kebanyakannya kerana apabila terdapat kesilapan menaip, atau beberapa bahagian yang hilang atau fail konfigurasi lama yang masih tinggal. Anda perlu mengosongkan semua baki dan kemudian cuba menyediakannya semula.

### 26. Untuk menghentikan perkhidmatan Heimdall dan Bor {#26-to-stop-heimdall-and-bor-services}

**Untuk pakej Linux**:

Hentikan Heimdall: `sudo service heimdalld stop`

Hentikan Bor: `sudo service bor stop`atau

1. `ps -aux | grep bor`. Dapatkan PID untuk Bor dan kemudian jalankan arahan berikut.
2. `sudo kill -9 PID`

**Untuk Binari**:

Hentikan Heimdall: `pkill heimdalld`

Hentikan Penghubung: `pkill heimdalld-bridge`

Hentikani Bor: Pergi ke CS-2001/bor dan kemudian jalankan, `bash stop.sh`

### 27. Untuk mengalih keluar direktori Heimdall dan Bor {#27-to-remove-heimdall-and-bor-directories}

**Untuk pakej Linux**: Padamkan Heimdall: `sudo rm -rf /etc/heimdall/*`

Padamkan Bor: `sudo rm -rf /etc/bor/*`

**Untuk Binari**:

Padamkan Heimdall: `sudo rm -rf ~/.heimdalld/`

Padamkan Bor: `sudo rm -rf ~/.bor`

### 28. Perkara yang perlu dilakukan apabila anda mendapat "Salah Blok.Header.AppHash." ralat {#28-what-to-do-when-you-get-wrong-block-header-apphash-error}

Ralat ini biasanya berlaku kerana permintaan Infura semakin habis. Apabila anda menyediakan nod pada Polygon, anda menambah Kekunci Infura pada fail Konfigurasi (Heimdall). Secara lalai anda dibenarkan 100k Permintaan setiap hari, jika had ini terlewati, maka anda akan menghadapi masalah sedemikian. Untuk menyelesaikan masalah ini, anda boleh mencipta kekunci API`config.toml`baharu dan menambahkannya pada fail.