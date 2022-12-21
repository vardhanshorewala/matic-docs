---
id: circuits
title: Sirkuit dan Transaksi
sidebar_label: Circuits and Transactions
description: "Jenis-jenis Sirkuit pada Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - circuits
  - deposit
  - transfer
image: https://matic.network/banners/matic-network-16x9.png
---

Sirkuit digunakan untuk menentukan aturan yang harus dipatuhi oleh transaksi agar transaksi tersebut dianggap benar. Secara luas, ada tiga jenis sirkuit, satu sirkuit untuk setiap jenis transaksi:

- [Penyetoran](#deposit)
- [Transfer](#transfer)
- [Penarikan](#withdraw)

Setiap transaksi memasukkan ZK Proof setelah batas ditentukan di sirkuit-sirkuit tersebut. Pengguna membangun bukti ini menggunakan Dompet
atau melalui server Klien.
Sebuah bukti dihasilkan hanya jika semua kasus berikut benar:

- [Komitmen](./commitments#what-are-commitments) baru valid
- [Komitmen](./commitments#what-are-commitments) lama valid dan dimiliki oleh pengirim
- [Nullifier] (./commitments#what-are-nullifiers) valid
- Path/root Pohon Merkle valid
- Ciphertext yang berisi komitmen valid


## Penyetoran {#deposit}
Penyetoran mengubah token ERC yang terlihat secara publik menjadi komitmen token yang memiliki nilai yang sama atau id token yang sama seperti token aslinya
dan kunci publik Nightfall dari pemilik komitmen yang dimaksud.

Penyetoran dengan ZK Proof membuktikan bahwa pembukti telah menciptakan komitmen $Z_A$ with a public key $pk_A$ yang valid.

Kemudian, sirkuit memeriksa $Z_A$ == H(@ | ɑ | $pk_A$ itu | σ)
Informasi transaksi penyetoran yang dibocorkan termasuk alamat yang mencetak komitmen baru dan alamat serta nilai token ERC yang digunakan.

![](../imgs/deposit.png)

## Transfer {#transfer}
Transfer memungkinkan transmisi hingga dua komitmen aset yang sama antara dua pihak dengan membatalkan komitmen sebelumnya dan membuat hingga dua komitmen baru:
- Satu komitmen akan dikirim ke penerima, yang berisi nilai jumlah yang ditransfer
- Komitmen yang lain akan dibuat dengan nilai perubahan (perbedaan antara jumlah nilai dari komitmen yang digunakan, dikurangi nilai yang ditransfer) dan yang dimiliki oleh pengirim.

Transfer ZK Proof membuktikan bahwa pembukti telah membatalkan hingga dua komitmen lama yang ada di Pohon Merkle, menciptakan satu komitmen baru, dan mengenkripsi informasinya untuk penerima.

Dalam kedua kasus tersebut, informasi yang dibocorkan yakni alamat Ethereum telah membatalkan komitmen
di antara kumpulan komitmen yang dimiliki oleh pengirim dan komitmen baru telah dibuat.
Informasi tentang pemilik baru, yang menerima komitmen atau jumlah yang ditransfer, akan bersifat pribadi.

Diagram pertama membahas langkah-langkah tentang membatalkan komitmen yang ada (atau beberapa komitmen) dan menambahkan informasi ke struktur data `transaction`.

![](../imgs/transfer_a.png)

Diagram kedua membahas langkah-langkah yang diperlukan untuk membuat dan mengenkripsi komitmen yang baru dibuat.


![](../imgs/transfer_b.png)

## Penarikan {#withdraw}
Penarikan adalah operasi untuk membatalkan komitmen Nightfall yang ada dan mengubahnya menjadi token ERC yang terlihat secara publik dengan nilai dan Id token yang sama sebagai komitmen yang terbakar. Penarikan adalah operasi yang berlawanan dengan operasi Penyetoran. Demikian pula untuk transfer, penarikan menerima hingga dua komitmen sebagai input.

Penarikan ZK Proof membuktikan bahwa pembukti telah membatalkan hingga dua komitmen lama yang ada di Pohon Merkle.

Informasi yang dibocorkan selama penarikan termasuk alamat dari alamat yang menarik komitmen dan nilai/Id token dan alamat token yang ditarik.

![](../imgs/withdraw.png)

### Periode pendinginan {#cooling-off-period}

Penarikan memerlukan periode `COOLING OFF` selama satu pekan untuk diselesaikan. Hal ini disebabkan sifat optimis Nightfall, karena blok baru dianggap benar sampai ada penantang yang mengajukan bukti penipuan. Dana akan disimpan sampai satu pekan berlalu, kemudian dana tersebut dapat ditarik ke L1.

# Biaya {#fees}

Pengusul mengambil transaksi yang masuk dan melakukan roll ke blok L2 dalam bursa untuk biaya. Ada dua jenis biaya yang dibayar untuk usulan sesuai dengan transaksinya:
- Penyetoran harus membayar biaya ETH langsung di L1.
- Transfer dan Penarikan harus membayar biaya dalam MATIC di L2.
