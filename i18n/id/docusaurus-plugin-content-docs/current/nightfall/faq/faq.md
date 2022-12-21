---
id: faq
title: FAQ
sidebar_label: FAQ
description: Pertanyaan umum tentang Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip
Jika tidak menemukan pertanyaan Anda dalam daftar ini, kirim pertanyaan di <ins>**[server discord Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR)**</ins>.

:::

## Di mana saya dapat menemukan Kontrak Cerdas? {#where-can-i-find-the-smart-contracts}

Kontrak Polygon Nightfall telah disebarkan di [testnet Goerli](../deployments/testnet.md) dan [mainnet](../deployments/mainnet.md).

## Bagaimana kondisi audit keamanan Polygon Nightfall? {#what-s-the-state-of-polygon-nightfall-s-security-audit}
Polygon Nightfall sedang menjalani audit keamanan yang rencananya akan selesai selama K3. Sementara itu, beberapa pembatasan telah ditambahkan ke protokol:

- Pengusul tunggal berjalan dan dikelola oleh Polygon
- [Jumlah penyetoran dan penarikan yang dibatasi](../tools/nightfall-wallet.md#deposit-and-withdraw-restrictions)

## Bagaimana cara menyiapkan Dompet Nightfall? {#how-do-i-set-up-my-nightfall-wallet}
Tutorial dompet lengkap bisa dilihat [di sini](../tools/nightfall-wallet.md) dengan semua perincian tentang cara memulai dompet Polygon Nightfall.

## Bagaimana cara menghubungkan Perangkat Keras Dompet Ledger ke Dompet Nightfall? {#how-do-i-connect-a-ledger-hardware-wallet-to-nightfall-wallet}
Ada bagian dalam tutorial dompet yang menjelaskan [cara menghubungkan Perangkat Keras Dompet dengan Metamask](../tools/nightfall-wallet.md#how-to-connect-a-ledger-hardware-wallet-to-nightfall).

## Berapa lama waktu transfer yang diperlukan Jaringan Polygon Nightfall dari awal hingga akhir? {#how-long-do-transfers-take-on-polygon-nightfall-network-from-start-to-finish}
Pengusul saat ini mengambil transaksi dari pengguna dan membuat blok hingga 32 transaksi. Begitu transaksi yang dikumpulkan cukup untuk membangun sebuah blok, transaksi akan diproses.

Selain itu, ada batas atas pada periode pembuatan blok sehingga setidaknya satu blok diusulkan setiap 6 jam (terlepas jumlah transaksi yang dikumpulkan oleh pengusul tersebut).

## Siapa yang dapat bertransaksi dengan saya? {#who-can-i-transact-with}
Untuk mentransfer aset dalam Polygon Nightfall, Anda hanya membutuhkan `Destination Wallet Address`. Baca tutorial dompet untuk memahami [cara berbagi Alamat Dompet](../tools/nightfall-wallet.md#your-wallet-address) guna menerima dana.

## Di mana komitmen didukung? {#where-are-commitments-backed-up}

Protokol zero knowledge proof dikomputasi di browser, sehingga kunci rahasia Anda tetap ada pada Anda dan dompet akan tetap melacak komitmen apa pun yang Anda miliki dalam IndexedDb. Siapa pun yang memiliki akses ke data ini dapat mengetahui komitmen mana yang Anda miliki, meskipun mereka tidak dapat mencurinya tanpa kunci Anda. Kunci hanya didekripsi ketika Anda memasukkan mnemonik. Jadi, Anda hanya perlu menggunakan dompet pada mesin yang Anda percaya.

Untuk saat ini, data tidak diekspor ke mana pun. Jadi, jika Anda menggunakan browser pada mesin yang berbeda, Anda tidak akan memiliki akses ke komitmen kecuali Anda mentransfer isi IndexedDB. Kami menyediakan mekanisme untuk mengekspor dan mengimpor komitmen melalui dompet.

## Privasi transaksi {#privacy-of-transactions}
Penting untuk memahami bahwa transaksi Setor dan Tarik bersifat tidak pribadi. Karena transaksi itu berinteraksi dengan Lapisan 1 dan Lapisan 1 bukan lapisan privat. Artinya, semua orang tahu bahwa Anda membuat komitmen Lapisan 2 dan jumlah isinya. Demikian juga, jika Anda mengembalikan token ke Lapisan 1 dengan memusnahkan komitmen Lapisan 2, semua orang juga akan tahu siapa yang menerima dan berapa jumlahnya.

Privasi sepenuhnya berasal dari transfer dalam Lapisan 2. Dari sudut pandang blockchain Ethereum, ini sepenuhnya pribadi. Satu-satunya data yang bocor adalah alamat IP Anda ketika Anda mengirim transaksi transfer ke Pengusul Blok. Untuk Beta awal, Polygon menjalankan satu-satunya Pengusul.


## Bagaimana cara menarik dana? {#how-to-withdraw-funds}
Dana dapat ditarik dengan dompet Polygon Nightfall. Penarikan memiliki periode finalisasi **satu pekan** yang dimulai sejak blok yang berisi transaksi penarikan dibuat. Setelah periode waktu ini telah berakhir, Anda dapat menyelesaikan penarikan untuk membuat dana dikirim ke akun Ethereum.

## Berapa biaya transaksi yang akan dikenakan di Nightfall? {#how-much-will-transactions-cost-on-nightfall}
Ada dua jenis transaksi yang dikenakan biaya berbeda:

- Transaksi on-chain: Transaksi ini dikirim ke kontrak cerdas dan membutuhkan biaya gas di Ethereum untuk bisa ditambang. Pengusul mana pun dapat mengambil transaksi ini dan meletakkannya di sebuah blok. Saat ini, `deposit` dan `finalize withdrawal` merupakan jenis transaksi on-chain.
- Transaksi off-chain: Transaksi ini dikirim langsung ke pengusul. Saat ini, semua `transfer` dan `withdrawals` dikonfigurasi sebagai transaksi off-chain.

## Token mana yang dapat saya gunakan di Jaringan Nightfall? {#which-tokens-can-i-use-on-nightfall-network}
Token berikut bisa beroperasi di Nightfall:

- MATIC
- WETH
- DAI
- USDC

## Apakah saya membutuhkan token MATIC untuk menggunakan Nightfall? {#do-i-need-matic-tokens-to-use-nightfall}
Ya. Anda harus menyetorkan beberapa token MATIC di Nightfall untuk bisa melakukan pembayaran untuk `transfers` dan `withdrawals`.

## Di mana saya dapat mengirimkan laporan bug atau menghubungi Nightfall untuk meminta bantuan tambahan? {#where-can-i-submit-a-bug-report-or-contact-nightfall-for-additional-help}
Cara terbaik adalah bergabung dengan [server discord Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR) dan mengirimkan pertanyaan Anda.
