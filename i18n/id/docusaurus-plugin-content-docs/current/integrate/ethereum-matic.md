---
id: ethereum-polygon
title: Ethereum ↔ Polygon
description: Bangun aplikasi blockchain Anda selanjutnya di Polygon.
keywords:
  - docs
  - matic
  - polygon
  - ethereum
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

# Ethereum ↔ Polygon {#ethereum-polygon}

Solusi Keamanan Plasma untuk mentransfer aset Anda dari Ethereum ke Polygon sebaliknya.
* Gunakan [matij.js](https://github.com/maticnetwork/matic.js) untuk berinteraksi dengan kontrak Plasma Polygon.

## Aliran {#flow}
Berikut adalah Aliran dengan penyebaran kontrak Anda di Polygon dan Dukungan untuk Ethereum↔Polygon.

1. Pengguna menyebarkan token matik ERC-20 Ethereum - XToken

2. Sekarang bagikan alamat kontrak Anda dengan [Polygon](https://t.me/joinchat/HkoSvlDKW0qKs_kK4Ow0hQ). Berikut adalah contoh permintaan...

> Halo semuanya, Kami adalah AwesomeDApp yang disebarkan di Polygon. Mencari solusi untuk transfer aset saya dari Ethereum ke Polygon dan sebaliknya. <br/><br/>Deskripsi singkat tentang AwesomeDApp saya...<br/><br/>
> Token_Address di Ropsten-> "0x.."<br/>
> Token_Name-> "XToken"<br/>
> Token_Symbol-> "X"<br/>
> Token_Decimals-> "18"<br/><br/>
> Meminta Anda untuk Memetakan token matik ini ke Versi Testnet Polygon.<br/>

Kami akan menyebarkan Kontrak Anak untuk Anda di Polygon yang dapat fleksibel berdasarkan persyaratan dan dipetakan ke token Ethereum ↔ Polygon.( Penyebaran di Polygon memerlukan token asli Polygon, yang dapat disetorkan dari Ethereum ke Polygon atau dapat dibeli di Pasar Sekunder.)

3. Pengguna dapat melakukan mint Xtoken dan Transfer di Ethereum. Misalnya, katakanlah 100XToken di-mint dan kemudian ditransfer ke akun lain.

4. Untuk menyediakan token matik ini di Rantai Polygon, fungsi Panggilan akan meminta dua transaksi pertama untuk disetujui dan kemudian disetor ke ERC20.

5. Sekarang 100XToken tersedia di Rantai Polygon di alamat yang sama.

6. Anda dapat mentransfer 50 XToken dari YourAddress ke NewAddress. Sekali lagi untuk transaksi Polygon yang mirip dengan Ethereum, Polygon menggunakan token matik Asli milik sendiri.

7. Jika pengguna ingin mendapatkan kembali Xtoken ini di Rantai Ethereum, panggil StartWithdraw yang akan menarik dari childTokenContract dan Membakar token matik ini di Rantai Polygon. Untuk menghindari partisipasi buruk, Satu set validasi akan ambil alih. Setelah selesai, token matik akan tersedia di Rantai Ethereum.

8. Panggil processExits() untuk menerima token matik itu kembali ke EOA atau alamat akun Anda.

9. Anda akan melihat 50 XToken di Ethereum mainnet di Alamat Akun Anda.
