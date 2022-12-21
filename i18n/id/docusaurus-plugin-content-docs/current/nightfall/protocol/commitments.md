---
id: commitments
title: Komitmen dan Pembatal
sidebar_label: Commitment and Nullifiers
description: "Transfer tunggal dan transfer ganda."
keywords:
  - docs
  - polygon
  - nightfall
  - commitment
  - nullifier
image: https://matic.network/banners/matic-network-16x9.png
---


## Apa itu Komitmen? {#what-are-commitments}
Komitmen adalah primitif kriptografi yang memungkinkan pengguna melakukan commit pada nilai yang dipilih,
tetapi tersembunyi bagi yang lain, dengan kemampuan mengungkapkan nilai yang dibuat komitmen nantinya.
Kerahasiaan nilai dan penerima dapat dicapai dengan cara ini.

Setiap kali pengguna melakukan transaksi menggunakan Nightfall, dompet browser mengomputasi Zero Knowledge Proof (ZKP) dan menciptakan (atau membatalkan) sebuah komitmen.
Misalnya, Anda membuat komitmen ketika melakukan penyetoran atau transfer dan membatalkan komitmen ketika
melakukan transfer atau penarikan.

Komputasi ZKP bergantung pada [sirkuit](../protocol/circuits.md) yang menentukan aturan yang
harus dipatuhi transaksi agar benar.

Komitmen ini digunakan untuk menyembunyikan properti berikut:
- **Alamat ERC token**
- **Id Token**
- **Nilai**
- **Pemilik**

Komitmen disimpan dalam struktur *Pohon Merkle*. Root dari *Pohon Merkle* ini disimpan secara on-chain.

![](../imgs/commitment.png)

### UTXO {#utxo}
Komitmen dibuat selama penyetoran dan transfer, serta digunakan selama transfer dan transaksi penarikan. **Komitmen tidak digabungkan**. Ketika menggunakan komitmen, nilai komitmen yang dihabiskan digunakan pada nilai yang dimiliki oleh dua komitmen tersebut.

Sirkuit transfer dan penarikan ZKP yang digunakan saat ini pada Nightfall terbatas pada 2 input - 2 output (komitmen transfer/penarikan dan perubahan) tidak termasuk pembayaran.
Jika serangkaian komitmen transaktor sebagian besar mengandung komitmen dengan nilai rendah (dust), komitmen itu mungkin kesulitan melakukan transfer nantinya.

Perhatikan serangkaian nilai berikut

- **Set A**: [1, 1, 1, 1, 1, 1]
- **Set B**: [2, 2, 2]
- **Set C**: [2, 4]

Meskipun ketiga rangkaian tersebut memiliki jumlah total yang sama, tetapi transfer nilai maksimum yang dapat ditransfer oleh set *A*, *B*, dan *C* masing-masing adalah 2, 4, dan 6. Ini adalah salah satu alasan nilai komitmen yang besar lebih disukai. Strategi pemilihan komitmen yang digunakan akan memitigasi risiko ini dengan memprioritaskan penggunaan komitmen bernilai kecil sekaligus meminimalkan komitmen dust yang tercipta.


## Apa itu Pembatal? {#what-are-nullifiers}
**Pembatal** adalah hasil kombinasi komitmen dan kunci pembatal. Setelah pembatal disiarkan on-chain, komitmennya dianggap telah digunakan.
Pembatal disimpan on-chain sebagai bagian dari data panggilan selama pengusulan blok.

![](../imgs/nullifier.png)



