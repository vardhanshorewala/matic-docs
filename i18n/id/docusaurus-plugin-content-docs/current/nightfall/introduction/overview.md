---
id: overview
title: Ikhtisar
sidebar_label: Overview
description: Ikhtisar tentang Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - privacy
  - rollup
  - zk
image: https://matic.network/banners/matic-network-16x9.png
---

Polygon meyakini visi yang melihat beragam perusahaan akan berinteraksi satu sama dalam waktu dekat
melalui kontrak cerdas untuk mengeksekusi logika bisnis dan mengelola bursa barang dan jasa.

Bekerja sama dengan [Ernst & Young](https://blockchain.ey.com/), Polygon menawarkan solusi rollup Lapisan 2 publik yang berfokus privasi yang bernama Polygon Nightfall untuk memungkinkan aksesibilitas dan privasi bagi perusahaan yang ingin
menggunakan Ethereum.

## Protokol ZK-Proof untuk Perusahaan {#a-zk-proof-protocol-for-enterprises}

Polygon Nightfall adalah bagian dari paket solusi skalabilitas Polygon yang meliputi
[Polygon Hermez](https://polygon.technology/solutions/polygon-hermez/),
[Polygon Miden](https://polygon.technology/solutions/polygon-miden/)
dan [Polygon Zero](https://polygon.technology/solutions/polygon-zero/).
Perbedaan utamanya adalah Nightfall merupakan rollup yang berfokus privasi dan dirancang untuk kasus penggunaan perusahaan dengan menggabungkan
konsep rollup optimis dan kriptografi Zero-Knowledge (ZK) untuk menawarkan transaksi privat dan dapat diskalakan.

Meskipun Nightfall memungkinkan skalabilitas, tetapi juga disiapkan untuk menghancurkan penghalang utama yang saat ini dihadapi oleh perusahaan
ketika menggunakan blockchain: kurangnya privasi transaksi. Nightfall menambahkan lapisan privasi sehingga parameter transaksi kunci (misalnya, nilai dan tujuan) tidak dapat dilacak kembali. Dua fitur ini telah menjadi solusi yang disukai perusahaan swasta yang melihat Nightfall sebagai suatu cara untuk menjalankan logika bisnis dan berkoordinasi dengan rantai pasokan dalam sebuah jaringan terdesentralisasi dengan harga yang berkelanjutan, sekaligus tetap menjaga keamanan dan privasi.

## Pilar-pilar Nightfall {#nightfall-s-pillars}

Proposisi nilai utama Polygon Nightfall adalah untuk memungkinkan transfer data secara aman, pribadi, dan berbiaya rendah
dalam sebuah jaringan yang terdesentralisasi.

![](../imgs/overview.png)

## Privasi {#privacy}

Polygon Nightfall menggunakan protokol ZK proof untuk mengirim transaksi privat. Pengguna dapat membuat protokol ZK proof dari
transaksinya tanpa mengungkapkan parameter transaksi kunci seperti tujuan atau nilai dari
transaksi tersebut. Detail lebih lanjut tentang komponen privasi Nightfall bisa dilihat di
panduan [protokol](../protocol/protocol.md).

## Keamanan {#security}

> Nightfall sedang menjalani audit keamanan dan diharapkan selesai pada pertengahan bulan Juni 2022.
> Setelah proses audit selesai, hasilnya akan diposting di sini.

> Sebagai sebuah jaringan baru yang memiliki periode bootstrap, Nightfall memiliki tindakan keamanan sementara untuk
> melindungi sistem yang bertujuan menghapus dan membuatnya menjadi terdesentralisasi sepenuhnya.

Polygon Nightfall adalah sebuah konstruksi Lapisan 2, karena memanfaatkan Ethereum dengan meminjam keamanannya sebagai sebuah
blockchain publik yang tangguh. Nightfall bergantung pada asumsi-asumsi tertentu yang menjamin pemulihan aset. Asumsi-asumsi tersebut
berdasarkan beberapa keputusan desain dan arsitektur yang bergulir di sekitar ZK-SNARKS, yang menggunakan
primitif kriptografi tertentu, seperti hash dan tanda-tangan.
Terakhir, Nightfall menanamkan peraturan operasi di berbagai kontrak cerdas untuk menjamin operator tidak memblokir
transaksi pengguna dan pengguna dapat menarik aset mereka kapan saja.

Ringkasnya, Nightfall membuat asumsi keamanan berikut:

1. Asumsi keamanan Ethereum.
2. Asumsi Groth16 (pengetahuan asumsi eksponen).
3. Asumsi kriptografi tertentu dari primitif, seperti hash (Poseidon) dan tanda-tangan.
4. Asumsi keamanan perangkat lunak yang mengandalkan desain dan implementasi yang benar.

## Efisiensi {#efficiency}

Pengusul blok mengumpulkan transaksi dari berbagai pengguna dan mengelompokkannya sebagai Blok L2.
Ukuran blok L2 biasanya mengandung sekitar 32 transaksi.

Perkiraan biaya gas yang harus dibayar untuk melakukan penyetoran, transfer, dan penarikan adalah 9.000, 1.200, dan 9.500. Biaya ini dibebankan guna menyimpan 574 Byte calldata untuk setiap transaksi, dan beberapa
calldata tetap dan komputasi untuk memproses blok L2. Biaya akan menjadi 80% lebih rendah setelah
[EIP 4488](https://eips.ethereum.org/EIPS/eip-4488).

## Transfer yang Tidak Dapat Disangkal {#non-deniable-transfers}

Sebagai bagian dari transfer transaksi ZK proof, Nightfall menyertakan enkripsi rahasia (alamat token,
nilai, id, dan salt) yang diperlukan untuk memproses komitmen yang ditransfer. Ini memaksa pengguna untuk mengenkripsi rahasia
dengan sebuah kunci yang diketahui oleh penerima. Karena kunci tersebut merupakan bagian dari ZK proof, penerima mengandalkan penyangkalan yang masuk akal
karena pengirim dapat membuktikan penggunaan kunci enkripsi yang benar.

## Desentralisasi {#decentralization}

Validator dan [Penantang](docs/nightfall/protocol/actors) adalah bagian integral dari Nightfall. Keduanya memastikan bahwa
transaksi dan blok L2 dibuat dengan benar dan tepat waktu. Mekanisme konsensus berbasis proof-of-stake (PoS)
digunakan untuk memilih [Pengusul](docs/nightfall/protocol/actors) berikutnya dalam jaringan. Di sisi lain, Penantang memantau
operasi jaringan yang benar dengan mengajukan tantangan ketika blok yang salah terdeteksi dan mempertahankan
stake yang diajukan oleh Pengusul.


## Bukti Masa Depan {#future-proof}
Berkat fleksibilitas yang disediakan oleh implementasi rollup Optimistic pada Nightfall, kita dapat memasukkan transaksi baru
di masa depan tanpa mengorbankan transaksi yang ada hanya dengan menentukan dan mendaftarkan tipe sirkuit baru yang mengimplementasikan
transaksi di ZK.

## Referensi {#references}

1. [Pendekatan Beragam Sisi untuk Penskalaan ZK](https://messari.io/article/polygon-a-multi-sided-approach-to-zk-scaling)
2. [Pendapat Paul Brody tentang Nightfall](https://www.linkedin.com/pulse/say-hello-nightfall-paul-brody-1f/)
