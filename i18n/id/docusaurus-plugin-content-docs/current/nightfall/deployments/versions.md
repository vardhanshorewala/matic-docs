---
id: versions
title: Riwayat
sidebar_label: History of changes
description: "Versi yang disebarkan"
keywords:
  - docs
  - polygon
  - nightfall
  - changelog
image: https://matic.network/banners/matic-network-16x9.png
---


## Beta 1.0 {#beta-1-0}
Beta 1.0 dirilis pada 17 Mei 2022. Versi ini disertai mekanisme dasar untuk menyebarkan proof of concept milik Nightfall. Versi ini mendukung implementasi transaksi `Proposer` tunggal dan `coarse` pertama. Versi tersebut juga menyediakan versi awal
dompet pengguna.
Versi yang disebarkan dapat ditemukan [di sini](https://github.com/EYBlockchain/nightfall_3/commit/bc3e475de3e2877f14430f9599e5b38ea960765b)

## Beta 2.0 {#beta-2-0}
Versi yang disebarkan dapat ditemukan [di sini](https://github.com/EYBlockchain/nightfall_3/commit/4c2af01ac95af5ea6f5b40071d73a1624f06ba46)
Beberapa perbaikan yang telah dilakukan:
- **Mengumpulkan Biaya**

Kemampuan yang dimiliki pengusul untuk mengumpulkan biaya transaksi yang dikumpulkan. Fitur ini akan memberikan insentif kepada beberapa pengusul.
- **Penyebaran Penantang**

Kini, Jaringan mencakup penantang yang memantau blok-blok milik pengusul.
- **Transaksi Sirkuit**

Fleksibilitas yang lebih baik dan performa yang lebih unggul ketika membuat ZKP dari transaksi apa pun. Baik  `transfer` ataupun `withdrawal` menerima hingga dua komitmen dan menghasilkan perubahan.
Terkait kinerja, kini transaksi telah dioptimalkan sehingga membutuhkan waktu yang lebih  singkat untuk pembuktian.

| Operasi | Batasan sebelum | Batasan sesudah |
|-----------|--------------------|------------------|
| Setoran | 84.766 | 1.277 |
| Transfer | 499.119 | 67.694 |
| Penarikan | 168.883 | 53.348 |

Bagian dari optimisasi telah dimungkinkan dengan beralih ke Poseidon

- **Enkripsi rahasia**

Kami telah berpindah dari El-Gamal ke proses enkripsi [KEM-DEM](../protocol/secrets) yang telah memberikan beberapa manfaat:
- Penyederhanaan proses enkripsi/dekripsi
- Pengurangan batasan dan biaya gas on-chain.

- **Penyebaran penantang**

