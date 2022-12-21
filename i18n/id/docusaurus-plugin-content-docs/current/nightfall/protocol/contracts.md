---
id: contracts
title: Kontrak Cerdas
sidebar_label: Smart Contracts
description: "Pelindung, pengusul, tantangan, dan Komputasi Pohon Merkle."
keywords:
  - docs
  - polygon
  - nightfall
  - smart
  - contracts
  - shield
image: https://matic.network/banners/matic-network-16x9.png
---

Kontrak menentukan peraturan yang harus diikuti oleh setiap aktor Nightfall untuk beroperasi di jaringan.
Kontrak Cerdas meliputi:

- [Shield.sol](#shield)
- [Proposers.sol](#proposers)
- [Challenges.sol](#challenges)
- [MerkleTree_Computations.sol](#merkletree_computations)

## Pelindung {#shield}
Kontrak ini memungkinkan pengguna mengirimkan transaksi untuk diproses oleh Pengusul. Jika transaksinya adalah Transaksi setor, maka kontrak tersebut akan mengambil pembayaran.
Kontrak tersebut juga memungkinkan siapa pun untuk meminta kondisi kontrak Pelindung (daftar pembatal dan root komitmen) diperbarui.
Ketika kondisi sudah diperbarui, setiap penarikan dalam pembaruan akan diproses.

Tidak ada kebutuhan mendasar untuk mengajukan transaksi transfer atau tarik ke blockchain: ini hanya sebagai papan pesan bagi
pengusul untuk mengambil transaksi dan memasukkannya ke Blok Lapisan 2.

Karena Nightfall berinteraksi dengan kontrak ERC nyata, pemeriksaan berikut tidak dapat dibuat privat:

- Selama **Penyetoran/Penarikan**, alamat token ERC valid.
- Selama **Penyetoran**, pengguna memiliki saldo atau mempunyai token untuk membuat komitmen.

## Pengusul {#proposers}
Kontrak mencakup fungsionalitas untuk melakukan pendaftaran, membatalkan pendaftaran, membayar dan merotasi pengusul, serta mengusulkan Blok Lapisan 2 yang baru ke blockchain.
Nightfall versi pertama hanya menerima Pengusul Boot tunggal yang dioperasikan oleh Polygon. Dalam versi mendatang, pembatasan ini akan dicabut ketika beberapa pengusul diizinkan.

## Tantangan {#challenges}
Fungsionalitas yang memungkinkan sebuah Blok ditantang sebagai hal yang salah.

## MerkleTree_Stateless {#merkletree_stateless}
Versi independen (fungsi murni) dari `MerkleTree.sol` asli, digunakan oleh `Challenges.sol` untuk membantu komputasi tantangan blok on-chain.

## Kontrak lain {#other-contracts}
- `Utils.sol` - mengumpulkan fungsionalitas bersama-sama baik fungsionalitas yang digunakan dalam beberapa kontrak atau fungsionalitas yang akan memengaruhi keterbacaan kode jika dibiarkan sejajar.
- `Config.sol` - menyimpan konstanta, sama seperti file konfig Node.js.
- `Structures.sol` - menentukan variabel struktur global, enum, peristiwa, pemetaan, dan variabel kondisi global. Sehingga lebih mudah ditemukan.

## Kemampuan peningkatan {#upgradability}
Setidaknya, di awal, Polygon mempertahankan kemampuan untuk meningkatkan kontrak Nightfall setelah penyebaran.
Kami menggunakan [Plugin Peningkatan](https://docs.openzeppelin.com/upgrades-plugins/1.x/) Openzeppelin yang akan digunakan Truffle.

Polygon menggunakan modul [penyebar](https://github.com/EYBlockchain/nightfall_3/tree/master/nightfall-deployer) untuk meningkatkan kontrak.
`deployer` menyimpan 4 migrasi dalam folder migrasinya.
Tiga migrasi pertama melakukan penyebaran 'normal' dari paket kontrak Polygon Nightfall. Namun,
hal itu memastikan semua kontrak (tetapi bukan pustaka) telah disebarkan dengan proksi agar dapat
ditingkatkan di kemudian hari. Migrasi keempat digunakan untuk meningkatkan kontrak.
