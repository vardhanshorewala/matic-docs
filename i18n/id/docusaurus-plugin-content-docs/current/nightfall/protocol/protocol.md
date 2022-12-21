---
id: protocol
title: Protokol Nightfall
sidebar_label: Nightfall Protocol
description: "Proses Nightfall."
keywords:
  - docs
  - polygon
  - nightfall
  - protocol
  - chain
  - block
  - structure
  - layer
image: https://matic.network/banners/matic-network-16x9.png
---

Kami berasumsi bahwa setidaknya 1 Pengusul telah terdaftar dengan sistem yang mengajukan Stake minimum.

## Pengajuan transaksi {#transaction-posting}
Ada dua mekanisme untuk mengajukan transaksi baru:

- [On-chain](#on-chain)
- [Off-chain](#off-chain)

### On-chain {#on-chain}
Proses dimulai ketika Transaktor menciptakan sebuah transaksi dengan memanggil `submitTransaction` di `Shield.sol`. Transaktor membayar biaya kontrak Pelindung untuk Transaksi tersebut, yang jumlahnya diputuskan Transaktor. Jumlah tersebut akan dibayarkan kepada Pengusul yang memasukkan Transaksi dalam sebuah Blok. Saat ini, pengusul dan instans Optimist yang mendasarinya kemungkinan besar akan memilih biaya yang lebih tinggi untuk memasukkan dalam sebuah blok, persis seperti yang dilakukan penambang.
Panggilan Transaksi menyebabkan peristiwa blockchain akan diajukan yang berisi detailnya. Jika itu transaksi Setor, kontrak Pelindung akan mengambil pembayaran token ERC Lapisan 1 yang bersangkutan.

### Off-chain {#off-chain}
Transaksi Transfer dan Penarikan memiliki pilihan untuk dikirim langsung ke pengusul yang mendengarkan, bukan dikirim on-chain melalui proses di atas.
Transaksi off-chain ini akan menghemat pengiriman biaya setor on-chain Transaktor (~45k gas), tetapi membutuhkan tingkat kepercayaan yang lebih besar antara transaktor dan pengusul yang dipilih untuk terhubung. Lebih mudah bagi pengusul dengan performa buruk untuk melakukan sensor transaksi yang diterima secara off-chain daripada yang diterima secara on-chain, karena transaksi-transaksi ini tidak disiarkan ke semua pengusul yang mendengarkan. Dalam kasus ini, transaktor hanya perlu mempertimbangkan sebuah transaksi yang dapat dipercaya ketika periode pendinginan (1 pekan) berlalu.

## Penerimaan transaksi {#transaction-acceptance}
Ketika Pengusul menerima transaksi apa pun, mereka melakukan serangkaian pemeriksaan untuk memvalidasi bahwa transaksi tersebut terbentuk dengan semestinya dan bukti memverifikasi hash masukan publik.
Jika semua pemeriksaan lolos, transaksi akan ditambahkan ke mempool Pengusul untuk dipertimbangkan dalam suatu Blok.

## Perakitan blok dan pengajuan {#block-assembly-and-submission}
Pengusul menunggu sampai kontrak Pelindung menunjuknya sebagai pengusul saat ini.
Pengusul saat ini menerima, dari instans Optimist internalnya, sebuah blok baru yang berisi transaksi dari mempool. Untuk masing-masing transaksi, blok akan mengomputasi komitmen baru Pohon Merkle yang akan ada jika transaksi ini ditambahkan ke kontrak Pelindung.

Dengan demikian, Blok ini berisi, hash Transaksi yang disertakan dalam Blok dan root Pohon Merkle komitmen, karena hash itu akan ada setelah memproses semua transaksi dalam Blok (Root Komitmen). Kemudian Pengusul mengirim blok ini ke kontrak cerdas Kondisi.

Ketika sebuah blok diusulkan, informasi berikut direkam secara on-chain:

- Struktur data blok
```
  struct Block {
    uint48 leafCount; // note this is defined to be the number of leaves BEFORE the commitments in this block are added
    address proposer;
    bytes32 root; // the 'output' commitment root after adding all commitments
    uint256 blockNumberL2;
    bytes32 previousBlockHash;
    bytes32 transactionHashesRoot;
  }
```
- Transaksi dalam blok
```
    struct Transaction {
        uint112 value;
        uint112 fee;
        TransactionTypes transactionType;
        TokenType tokenType;
        uint64[2] historicRootBlockNumberL2; // number of L2 block containing historic root
        uint64[2] historicRootBlockNumberL2Fee; //number of L2 block containing historic root fee
        bytes32 tokenId;
        bytes32 ercAddress;
        bytes32 recipientAddress;
        bytes32[2] commitments;
        bytes32[2] nullifiers;
        bytes32[1] commitmentFee;
        bytes32[2] nullifiersFee;
        bytes32[2] compressedSecrets;
        uint256[4] proof;
    }
```

## Tantangan {#challenges}
Blok akan dapat ditantang dalam antrean sepekan. Selama itu, kebenarannya dapat ditantang dengan memanggil salah satu fungsi yang menantang. Tantangan yang dapat dibuat adalah:

- **INVALID_PROOF** - bukti yang diberikan dalam sebuah transaksi tidak diverifikasi sebagai bukti yang benar;
- **INVALID_PUBLIC_INPUT_HASH** - hash masukan publik dari sebuah transaksi bukan hash yang benar dari masukan publik;
- **HISTORIC_ROOT_EXISTS** - root Pohon Merkle komitmen yang digunakan untuk membuat bukti transaksi yang tidak pernah ada;
- **DUPLICATE_NULLIFIER** - sebuah pembatal yang diberikan sebagai bagian dari sebuah Transaksi, terdapat dalam daftar pembatal yang digunakan;
- **HISTORIC_ROOT_INVALID** - root komitmen diperbarui karena hasil pemrosesan transaksi dalam Blok itu tidak benar;
- **DUPLICATE_TRANSACTION** - sebuah transaksi identik yang disertakan dalam blok ini telah dimasukkan dalam blok sebelumnya;
- **TRANSACTION_TYPE_INVALID** - transaksi tidak terbentuk dengan baik berdasarkan jenis transaksi (misalnya, Penyetoran, Transfer, Penarikan).

Jika tantangan berhasil, yakni komputasi on-chain, menunjukkan bahwa sebuah tantangan valid, maka tindakan berikut dilakukan:

- Hash dari Blok yang bersangkutan dan semua Blok setelahnya dihapus dari antrean.
- Stake Blok, yang dikirimkan oleh Pengusul, dibayarkan kepada Penantang.
- Transaktor dengan Transaksi dalam Blok akan diganti dengan biaya yang akan mereka bayar ke Pengusul dan dana escrow ditahan oleh kontrak Pelindung dalam kasus transaksi Penyetoran.

