---
id: nightfall-wallet
title: Dompet Nightfall
sidebar: Nightfall Wallet
description: "Panduan tentang dompet Polygon Nightfall."
keywords:
  - docs
  - matic
  - polygon
  - nightfall
  - wallet
image: https://matic.network/banners/matic-network-16x9.png

---

Dompet Polygon Nightfall adalah sebuah dompet browser yang dapat berinteraksi dengan
rilis beta mainnet Nightfall.

:::info Gunakan dompet Nightfall untuk melakukan penyetoran, transfer, dan penarikan

### Pembatasan {#restrictions}

Ketika Nightfall mencapai kondisi matang, pembatasan berikut diterapkan:


| Token ERC20 | Setoran Maks | Penarikan Maks |
|-------------|-------------|--------------|
| MATIC | 250 MATIC | 1.000 MATIC |
| WETH | 0,25 WETH | 1 WETH |
| DAI | 250 DAI | 1.000 DAI |
| USDT | 250 USDT | 1.000 USDT |
| USDC | 250 USDC | 1000 USDC |

:::

:::caution Tindakan keamanan

Dompet Nightfall diuji di browser Chrome. Selama versi Beta, hasilnya dapat berbeda di browser
lainnya.

**Sebaiknya, Anda menggunakan Nightfall di Chrome**.

:::



## Memulai {#getting-started}

Kunjungi [dompet mainnet](https://wallet-beta.polygon.technology) Polygon atau
[dompet testnet](https://wallet.testnet.polygon-nightfall.technology/), hubungkan akun MetaMask Anda
dan pilih Dompet Polygon di sebelah kiri. Jika Anda perlu bantuan dengan MetaMask, lihat
[dokumentasi Polygon di MetaMask](../../develop/metamask/tutorial-metamask.md)

![](../imgs/tools-wallet/polygon-wallet-click-nf.png)

Pada titik ini, dompet akan meminta Anda untuk Beralih ke Jaringan Polygon, dan popup MetaMask akan
meminta konfirmasi peralihan itu.

![](../imgs/tools-wallet/polygon-network.png)

Berikutnya, pada bagian atas dompet, klik menu Menurun dan pilih `Polygon Nightfall`, maka
permintaan baru untuk beralih ke Ethereum Mainnet akan muncul. Harap terima untuk beralih ke Ethereum mainnet
untuk beroperasi dengan Polygon Nightfall.

![](../imgs/tools-wallet/polygon-network-dropdown-nf.png)

Jika Anda menggunakan testnet, URL dompet akan langsung mengarahkan Anda ke halaman utama dompet Polygon Nightfall.

![](../imgs/tools-wallet/wallet-main-screen.png)

Pada kunjungan pertama, dompet Nightfall harus dibuat. Pop-up akan muncul untuk membuat mnemonik dan dompet. Klik `Generate Mnemonic`, kemudian `Create Wallet`. **Perlu diperhatikan bahwa Anda hanya dapat menggunakan dompet ini di perangkat yang Anda gunakan saat ini**.

![](../imgs/tools-wallet/generate-mnemonic-create-wallet.png)

:::caution Buat dan simpan salinan komitmen dan mnemonik Anda

Kunci dompet dan transaksi Anda disimpan di browser (IndexedDb). Sama seperti mnemonik yang Anda buat ketika mengakses Dompet Nightfall untuk pertama kalinya.

Pastikan Anda menyimpan mnemonik ini di tempat yang aman. Ini satu-satunya cara untuk dapat membuat bukti yang kompatibel dengan dana Anda di L2. Begitu juga dengan komitmen Anda: pastikan tersimpan aman dengan menekan `export commitments`ketika Anda menggunakan browser atau komputer lain.

:::

**Jika komitmen hilang, dana Anda juga hilang selamanya**


Saat ini, seharusnya Anda sudah dapat melihat alamat Metamask dan dompet Nightfall (di kanan atas).

**Tunggu beberapa menit lagi hingga pengaturan dompet selesai sebelum mulai melakukan transaksi**.

Di sudut kiri bawah dompet, status dompet akan ditampilkan sebagai `Syncing Nightfall`. Dalam kondisi ini, dompet akan mengambil
sirkuit ZK dan kondisi jaringan yang diperlukan untuk melakukan transaksi.

![](../imgs/tools-wallet/wallet-state-syncing.png)

Harap tunggu hingga status dompet berubah menjadi `Nightfall Synced`

![](../imgs/tools-wallet/wallet-state-synced.png)


## Cara menghubungkan Dompet Perangkat Keras Ledger ke Nightfall {#how-to-connect-a-ledger-hardware-wallet-to-nightfall}
Anda dapat melihat panduan untuk menghubungkan Dompet Perangkat Keras Ledger dengan Metamask di situs resmi Metamask [di sini](https://support.ledger.com/hc/en-us/articles/4404366864657-How-to-access-your-Ledger-Ethereum-ETH-account-via-Metamask?docs=true).

Pastikan Anda menghubungkan Aplikasi Ethereum dalam dompet dan aktifkan "blind signing" di pengaturan Aplikasi Ethereum.


### Alamat dompet Anda {#your-wallet-address}
Dapatkan alamat dompet Nightfall dari halaman Aset Nightfall dengan mengklik `Receive`.

![](../imgs/tools-wallet/nightfall-wallet-address.png)

## Cara melakukan penyetoran {#how-to-make-deposits}
Dari halaman Aset Nightfall, klik tombol `Deposit` yang ada di sebelah kanan aset yang Anda pilih atau buka halaman Jembatan L2.

1. Periksa apakah mode Transfer diatur ke `Deposit`
2. Periksa apakah token yang diinginkan sudah dipilih (WETH, MATIC, dsb.)
3. Masukkan nilai yang akan disetorkan di Dompet Nightfall, lalu klik `Transfer`
4. Tinjau transaksi di pop-up
5. Klik `Create Transaction`

![](../imgs/tools-wallet/deposit-click-transfer.png)

Sebuah proses akan dimulai untuk mengomputasi ZKP dan menyiapkan transaksi - berikan akses ke saldo akun Anda pada Metamask. Saat ini selesai, klik `Send Transaction` - berikan izin lebih lanjut kepada Metamask untuk interaksi kontrak.

![](../imgs/tools-wallet/deposit-tx-created-and-ready-to-be-sent.png)

Buka halaman Transaksi untuk [melihat setoran Anda](#view-transactions).

### Informasi penting tentang setoran {#important-information-about-deposits}
- [Jumlah setoran dibatasi](#note-the-following-deposit-and-withdrawal-restrictions) untuk versi Beta

## Cara melakukan transfer {#how-to-make-transfers}
Dari halaman Aset Nightfall, klik tombol `Send` yang ada di sebelah kanan aset yang dipilih.

1. Masukkan alamat yang valid yang ada di Polygon Nightfall L2
2. Periksa apakah token yang diinginkan sudah dipilih (WETH, MATIC, dsb.)
3. Masukkan nilai yang akan ditransfer dari dompet Nightfall, klik `Continue`

![](../imgs/tools-wallet/send-nf.png)

Sebuah proses akan dimulai untuk mengomputasi ZKP dan mempersiapkan transaksi. Jika sudah selesai, klik `Send Transaction`.

Buka halaman Transaksi untuk [melihat transfer Anda](#view-transactions).

### Informasi penting tentang transfer {#important-information-about-transfers}
Sirkuit transfer ZKP sedang digunakan di Nightfall membatasi jumlah transfer agar sama persis dengan nilai salah satu
komitmen yang ada atau kombinasi linier dari dua komitmen yang ada.

Untuk menggambarkan pembatasan transfer dengan sebuah contoh, amati serangkaian komitmen berikut:

- Set A: [1, 1, 1, 1, 1, 1]
- Set B: [2, 2, 2]
- Set C: [2, 4]

Meskipun ketiga set di atas memiliki jumlah total yang setara, yaitu 6, tetapi hanya transfer berikut yang tersedia:

- Set A: Transfer antara 0 dan 2 (keduanya dikecualikan)
- Set B: Transfer antara 0 dan 4 (keduanya dikecualikan)
- Set C: Transfer antara 0 dan 6 (keduanya dikecualikan)

Tetap dengan contoh tersebut, jika Alex memiliki komitmen Set C, transfer yang tersedia menyertakan jumlah antara 0 dan 6, yang mengecualikan nilai-nilai batasnya. Jika Alex memutuskan untuk mentransfer 3,5 ke Bob, maka Alex pada akhirnya akan memiliki sebuah komitmen tunggal bernilai 2,5 dan Bob akan menerima komitmen 3,5 setelah bloknya diusulkan.

Di sisi lain, jika Alex memutuskan untuk melakukan transfer bernilai 6 ke Bob, maka ZK proof akan gagal karena tidak akan ada kombinasi komitmen yang valid.

**Perlu diperhatikan bahwa nilai-nilai ini mewakili komitmen yang dimiliki**, bukan setoran, misalnya. Informasi lebih lanjut tersedia di bagian [komitmen](../protocol/commitments.md) dalam dokumen ini.

## Cara melakukan penarikan {#how-to-make-withdrawals}
Dari halaman Aset Nightfall, klik tombol `Withdraw` yang ada di sebelah kanan aset yang dipilih atau buka halaman Jembatan L2.

1. Periksa apakah mode Transfer diatur ke `Withdraw`
2. Periksa apakah token yang diinginkan sudah dipilih (WETH, MATIC, dsb.)
3. Masukkan nilai yang akan ditarik dari dompet Nightfall, klik `Transfer`
4. Tinjau transaksi di pop-up
5. Klik `Create Transaction`

Sebuah proses akan dimulai untuk mengomputasi ZKP dan mempersiapkan transaksi. Jika sudah selesai, klik `Send Transaction`.

Buka halaman Transaksi untuk [melihat penarikan Anda](#view-transactions). Setelah periode finalisasi satu pekan berakhir, pengguna akan
dapat menyelesaikan dan mengklaim jumlah penarikan.

### Informasi penting tentang penarikan {#important-information-about-withdrawals}
- Nilai penarikan harus sama persis sesuai jumlah dalam salah satu komitmen yang dimiliki (lebih lanjut [tentang komitmen](#learn-about-commitments))
- Penarikan memiliki periode finalisasi **satu pekan** sejak mulai dibuatnya blok yang berisi transaksi penarikan. Setelah periode waktu ini telah berakhir, Anda dapat menyelesaikan penarikan untuk membuat dana Anda dikirim ke akun Ethereum.
- [Jumlah penarikan dibatasi](#note-the-following-deposit-and-withdrawal-restrictions) ketika mengunakan versi Beta
- Penarikan adalah transaksi onchain dan harus membayar biaya gas selama permintaan transaksi serta ketika penarikan difinalisasi.

![](../imgs/tools-wallet/cooling-off-vs-ready.png)

## Melihat transaksi {#view-transactions}
Periksa status setoran, transfer, dan penarikan di halaman Transaksi. Perlu diperhatikan bahwa setiap transaksi diproses setelah ada transaksi yang cukup untuk menghasilkan blok atau dalam waktu 6 jam.

![](../imgs/tools-wallet/transactions.png)
