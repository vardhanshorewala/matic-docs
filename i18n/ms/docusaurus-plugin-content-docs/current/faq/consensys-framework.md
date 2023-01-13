---
id: consensys-framework
title: Rangka Kerja Penskalaan Consensys
sidebar_label: Consensys Scaling Framework
description: Bangunkan aplikasi blok rantai anda yang seterusnya di Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

Rangka kerja ini diperolehi daripada [Empat soalan Consensys untuk Menilai sebarang penyelesaian penskalaan](https://consensys.net/?p=19015&preview=true&_thumbnail_id=19017)

## Siapakah Mengendalikannya? {#who-operates-it}
Nod pelombong pada Ethereum mainnet memindahkan atau "mengendalikan" rangkaian ke hadapan dengan menyelesaikan Bukti Pegang dan mencipta blok baharu. Penyelesaian L2 memerlukan peranan "pengendali" yang serupa pada rangkaiannya, yang setara dengan pelombong Ethereum mainnet yang boleh menggerakkan rangkaian L2 ke hadapan. Walau bagaimanapun, terdapat sedikit perbezaan. Sebagai contoh, bersama-sama dengan memproses dan membenarkan transaksi seperti pelombong, pengendali L2 juga boleh memudahkan pengguna memasuki dan keluar dari lapisan L2 itu sendiri.

### - Siapakah atau apakah yang diperlukan untuk mengendalikan rangkaian Polygon Bukti Pegang? {#who-or-what-is-required-to-operate-the-polygon-proof-of-stake-network}

Rantaian komit Polygon PoS bergantung pada satu set pengesah untuk menjamin rangkaian. Peranan pengesah adalah untuk menjalankan nod penuh; menghasilkan sekatan, mengesahkan dan mengambil bahagian dalam konsensus dan melakukan pusat pemeriksaan pada rantaian utama Ethereum. Untuk menjadi pengesah, seseorang perlu pegang token MATIC mereka dengan pegangang kontrak pengurusan yang berada pada rantaian utama Ethereum.

Untuk butiran lanjut, sila rujuk https://docs.polygon.technology/docs/validate/validator/introduction#overview

### - Bagaimanakah mereka menjadi pengendali dalam rangkaian Polygon? Apakah peraturan yang mereka patuhi? {#how-do-they-become-operators-in-the-polygon-pos-network-what-rules-do-they-abide-by}

Untuk menjadi pengesah, seseorang perlu pegang token MATIC mereka dengan pegangan kontrak pengurusan yang berada pada rantai utama Ethereum.

Ganjaran diagihkan kepada semua pemegang berkadaran dengan pegang mereka di setiap titik semak dengan pengecualian adalah pencadang mendapat bonus tambahan. Baki ganjaran pengguna akan dikemas kini dalam kontrak yang dirujuk sementara menuntut ganjaran.

Pegang adalah berisiko untuk dipotong jika nod pengesah melakukan tindakan berniat jahat seperti tandatangan berganda, masa henti pengesah yang juga mempengaruhi yang dipautkan pemberi kuasa di pusat pemeriksaan itu.

Untuk butiran lanjut sila rujuk https://docs.polygon.technology/docs/validate/validator/introduction#end-to-end-flow-for-a-matic-validator and https://docs.polygon.technology/docs/validate/validator/responsibilities/#responsibilities-of-validator﻿


### - Apakah andaian kepercayaan yang mesti dibuat oleh pengguna PoS Polygon mengenai pengendali? {#what-trust-assumptions-must-the-polygon-pos-users-make-about-the-operator}

Rantaian komit Polygon PoS bergantung pada satu set pengesah untuk menjamin rangkaian. Peranan pengesah ialah menjalankan nod penuh; menghasilkan blok, mengesahkan dan mengambil bahagian dalam konsensus dan melakukan pemeriksaan pada rantaian utama. Untuk menjadi pengesah, seseorang perlu pegang token MATIC mereka dengan memegang kontrak pengurusan yang berada di rantaian utama. Selagi ⅔ daripada pegangan wajaran pengesah adalah jujur, rantaian akan maju dengan tepat.

### - Apakah tanggungjawab pengendali? Apakah kuasa yang mereka ada? {#what-are-the-operators-responsible-for-what-power-do-they-have}

Peranan pengesah ialah menjalankan nod penuh; menghasilkan blok, mengesahkan dan mengambil bahagian dalam konsensus dan melakukan pemeriksaan pada rantaian utama.

Pengesah mempunyai kuasa untuk menghentikan kemajuan rantai, menyusun semula blok, dsb. dengan mengandaikan ⅔ daripada pengesah pegangan dengan berat adalah tidak jujur. Mereka tidak mempunyai kuasa untuk mengubah keadaan, baki aset pengguna, dll.

### - Apakah motivasi untuk menjadi pengendali PoS Polygon? {#what-are-the-motivations-to-become-an-operator-of-the-polygon-pos}

Pengesah yang pegang token MATIC mereka sebagai cagaran untuk bekerja demi keselamatan rangkaian dan sebagai pertukaran untuk perkhidmatan mereka, memperoleh ganjaran.

Sila rujuk https://docs.polygon.technology/docs/validate/economics#what-is-the-incentive untuk butiran lanjut.

## Bagaimanakah Data? {#how-s-the-data}
Secara takrifan, teknologi Lapisan 2 mesti mencipta pusat pemeriksaan data tambahan pada Lapisan 1 (Ethereum mainnet). Oleh itu, kebimbangan kami adalah dengan masa interstisial antara daftar masuk Lapisan 1 yang berkala tersebut. Secara khusus, bagaimanakah data Lapisan 2 dijana, disimpan dan diuruskan semasa berada jauh dari pelabuhan selamat Lapisan 1? Kami amat bimbang dengan perkara ini kerana ia adalah ketika pengguna yang berada paling jauh dari sekuriti tanpa amanah sesebuah mainnet awam.

### - Apakah syarat kunci untuk PoS Polygon? {#what-are-the-lock-up-conditions-for-polygon-pos}

Dalam kebanyakan corak reka bentuk token, token dicetak pada Ethereum dan boleh dihantar ke PoS Polygon. Untuk mengalihkan token sedemikian daripada Ethereum ke PoS Polygon, pengguna perlu mengunci dana dalam kontrak di Ethereum, dan token yang sepadan kemudiannya dicetak pada PoS Polygon.

Mekanisme geganti jambatan ini dijalankan oleh pengesah PoS Polygon yang perlu ⅔ bersetuju dengan acara token terkunci pada Ethereum untuk menghasilkan jumlah token yang sepadan pada PoS Polygon.

Mengeluarkan aset kembali ke ethereum ialah proses 2 langkah di mana token aset perlu dibakar terlebih dahulu pada rantaian komit PoS Polygon dan kemudian bukti transaksi pembakaran ini perlu diserahkan pada rantaian Ethereum.


Untuk butiran lanjut, rujuk https://docs.polygon.technology/docs/develop/ethereum-polygon/pos/getting-started#steps-to-use-the-pos-bridge

### - Berapa lamakah dana tersebut tersedia pada PoS Polygon? {#how-soon-are-those-funds-available-on-the-polygon-pos}

Lebih kurang ~22-30 minit. Ini dilakukan melalui mekanisme penghantaran mesej yang dipangg`state sync`il. Butiran lanjut boleh didapati di sini: https://docs.polygon.technology/docs/pos/state-sync/state-sync/

Adakah PoS Polygon menyediakan sokongan untuk pengguna yang masuk tanpa kunci L1 (iaitu dalam kes memasukkan pengguna terus ke Polygon, maka pengguna ingin keluar ke Ethereum mainnet)?

Ya, mekanisme jambatan khas digunakan untuk mencapainya. Apabila pengguna ingin keluar ke Ethereum, bukannya kaedah biasa membuka kunci token daripada kontrak khas, ianya ditempa.

Anda boleh membaca tentangnya di sini: https://docs.polygon.technology/docs/develop/ethereum-polygon/pos/mintable-assets

### - Bagaimanakah pengguna mempertikaikan transaksi PoS Polygon yang tidak sah? Buktikan transaksi PoS Polygon yang sah? {#how-would-a-user-dispute-an-invalid-polygon-pos-transaction-prove-a-valid-polygon-pos-transaction}

Pada masa ini tiada cara dalam rantaian untuk mempertikaikan transaksi PoS Polygon yang tidak sah. Walau bagaimanapun, pengesah rantaian PoS Polygon menyerahkan pusat pemeriksaan berkala ke Ethereum - anda boleh melihat butiran lanjut di sini: https://docs.polygon.technology/docs/pos/heimdall/modules/checkpoint/
Adalah mungkin untuk mengesahkan transaksi pada rantaian PoS Polygon pada Ethereum dengan membina bukti pokok Merkle dan mengesahkannya terhadap pusat pemeriksaan berkala yang berlaku pada Ethereum bagi transaksi PoS Polygon dan menerima akar pokok Merkle.

Sebaik sahaja pengguna Polygon ingin keluar, berapa lamakah dana Lapisan 1 yang kunci (tambah atau tolak sebarang keuntungan atau kerugian L2) tersedia kembali pada L1?

Lebih kurang ~1-3 jam bergantung pada kekerapan pusat pemeriksaan (https://docs.polygon.technology/docs/pos/heimdall/modules/checkpoint/). Kekerapan itu sebahagian besarnya merupakan fungsi kos yang sanggup dibelanjakan oleh pengesah untuk yuran gas ETH untuk menghantar pusat pemeriksaan.

### - Adakah anda menjangkakan terdapat Penyedia Kecairan pada Lapisan 1 bersedia memberikan dana L1 yang boleh ditebus serta-merta kepada pengguna PoS Polygon yang sedia ada? {#do-you-anticipate-there-being-liquidity-providers-on-layer-1-willing-to-provide-immediately-redeemable-l1-funds-to-existing-polygon-pos-users}

Sudah terdapat beberapa pemain seperti https://connext.network/ (sudah langsung) dan https://biconomy.io/ yang sedang atau akan menyediakan perkhidmatan ini. Terdapat pelbagai bilangan pemain lain yang juga akan disiarkan tidak lama lagi.

## Bagaimanakah Pegang? {#how-s-the-stack}
Perbandingan daripada pegang adalah penting untuk menyerlahkan apa yang Lapisan 2 telah atau tidak berubah daripada Ethereum mainnet.

### - Berapa banyakkah bahagian pegang PoS Polygon dengan pegang Ethereum mainnet? {#how-much-does-the-polygon-pos-stack-share-with-the-ethereum-mainnet-stack}

Jika anda seorang pembangun Ethereum, anda sudah pun menjadi pembangun PoS Polygon. Semua alatan yang anda biasa gunakan disokong pada PoS Polygon di luar kotak: Truffle, Remix, Web3js dan banyak lagi.

Tiada perubahan besar dalam antara muka EVM untuk PoS Polygon berbanding dengan Ethereum.

### - Di manakah PoS Polygon berbeza daripada pegang Ethereum mainnet dan apakah risiko / ganjaran yang diperkenalkan olehnya? {#where-does-the-polygon-pos-differ-from-ethereum-mainnet-stack-and-what-risks-rewards-does-that-introduce}

Tiada perubahan besar.

## Bersedia untuk yang Terburuk {#preparing-for-the-worst}
Cara sistem PoS Polygon menyediakan untuk:

### - Keluar beramai-ramai daripada pengguna? {#a-mass-exit-of-users}

Selagi ⅔ daripada pengesah jujur, dana dalam rantaian adalah selamat. Jika andaian ini tidak sah, dalam senario sedemikian rantai boleh berhenti atau penyusunan semula boleh berlaku. Konsensus sosial akan diperlukan untuk memulakan semula rantaian daripada keadaan sebelumnya - termasuk gambar keadaan PoS Polygon yang diserahkan melalui pusat pemeriksaan yang boleh digunakan untuk melakukan ini.

### - Peserta Polygon cuba untuk memainkan konsensus Polygon. Contohnya, dengan membentuk kartel? {#polygon-participants-attempting-to-game-the-polygon-consensus-for-example-by-forming-a-cartel}

Konsensus sosial akan diperlukan untuk memulakan semula rantaian daripada keadaan terdahulu dengan mengalih keluar pengesah tersebut dan memulakannya semula dengan set pengesah baharu - termasuk gambar ringkas keadaan PoS Polygon yang diserahkan melalui titik pemeriksaan yang boleh digunakan untuk melakukan ini.


### - Pepijat atau eksploitasi ditemui di bahagian kritikal sistemnya? {#a-bug-or-exploit-discovered-in-a-critical-part-of-its-system}

Penjagaan telah diambil untuk menggunakan semula komponen yang diuji pertempuran dalam binaan keluar daripada sistem. Walau bagaimanapun, jika terdapat pepijat atau eksploitasi dalam bahagian kritikal sistem, memulihkan rantaian kepada keadaan yang lebih awal melalui konsensus sosial ialah jalan penyelesaian utama.
