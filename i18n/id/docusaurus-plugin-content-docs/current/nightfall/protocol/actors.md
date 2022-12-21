---
id: actors
title: Aktor
sidebar_label: Actors
description: "Jenis-jenis Aktor pada Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - transactor
  - proposer
  - challenger
  - liquidity
  - provider
image: https://matic.network/banners/matic-network-16x9.png
---

Ada empat aktor yang terlibat dalam jaringan:

- [Transaktor](#transactor)
- [Pengusul](#proposer)
- [Penantang](#challenger)

## Transaktor {#transactor}
Transaktor adalah pelanggan reguler layanan. Mereka ingin membuat transaksi, yakni Setor, Transfer, dan Tarik secara pribadi.
Pelanggan ini biasanya akan menggunakan dompet web atau server khusus (Klien) untuk melakukan protokol ZK Proof yang diperlukan guna menghasilkan transaksi.

## Pengusul {#proposer}
Pengusul mengumpulkan transaksi dari pelanggan dan mengusulkan pemutakhiran baru ke kondisi
kontrak Pelindung.
Berdasarkan kondisi, yang kami maksud khususnya adalah variabel penyimpanan yang dikaitkan dengan transaksi ZKP:
root nullifier dan komitmen.
Perbarui proposal berisi beberapa transaksi yang dilakukan rollup menjadi Blok Lapisan 2. Hanya hash
kondisi akhir yang akan ada setelah semua transaksi di Blok yang diproses
sudah disimpan pada rantai. Transaksi akan menjadi final setelah 1 pekan.

Siapa saja dapat menjadi Pengusul, tetapi harus mengajukan beberapa stake. Stake tersebut untuk memberikan insentif atas perilaku baik.
Pengusul menghasilkan uang dengan menyediakan Blok yang benar, mengumpulkan biaya dari transaktor. Ini agak selaras dengan Penambang dalam blockchain konvensional.

## Penantang {#challenger}
Penantang mengawasi benar-tidaknya blok yang diusulkan dalam waktu satu pekan setelah blok dikirim. Siapa saja dapat menjadi Penantang.
Penantang mengambil stake yang diajukan oleh pengusul ketika membangun blok dan berhasil mengirim sebuah tantangan.


## Catatan {#notes}
Dalam implementasi referensi Polygon, Pengusul dan Penantang melakukan offload atas beberapa fungsionalitas ke sebuah modul umum yang disebut Optimist.
Modul Optimist ini menyediakan beberapa layanan ke sejumlah Pengusul dan Penantang, seperti menghasilkan dan menantang blok
(Pengusul dan Penantang perlu menandatangani transaksi ini), menyinkronkan peristiwa blockchain, dll.

Selain Aktor yang dijelaskan di atas, ada aktor tambahan yang disebut Klien. Klien bertindak sebagai layanan tepercaya yang mengumpulkan transaksi pengguna, melakukan protokol ZK Proof atas nama mereka, mengirim transaksi ke Pengusul, mendengarkan peristiwa Blockchain, dll. Ringkasnya, Klien bertindak sebagai penghubung terpercaya bagi sekumpulan pengguna yang ingin melakukan offload komputasi bukti berat dan saling memercayai.

Selain menggunakan Klien, kita bisa menggunakan dompet browser, layanan nirserver yang disediakan oleh Polygon. Dompet ini mengelola semua aktivitas transaksi untuk pengguna tunggal sekaligus menjaga privasi.
