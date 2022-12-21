---
id: secrets
title: Distribusi Rahasia In Band
sidebar_label: In Band Secret Distribution
description: "Sebuah solusi untuk mengenkripsi rahasia dan memastikan dekripsinya."
keywords:
  - docs
  - polygon
  - nightfall
  - secret
  - encryption
  - key
image: https://matic.network/banners/matic-network-16x9.png
---
import katex from 'katex';

## Ikhtisar {#overview}

Untuk memastikan penerima menerima informasi rahasia yang dibutuhkan untuk menggunakan komitmen mereka, pengirim
mengenkripsi rahasia (*salt*, *nilai*, *Id token*, *ercAddress*) dari komitmen yang dikirim ke penerima dan
membuktikan dengan ZKP yang dienkripsi dengan benar menggunakan kunci publik penerima. Paradigma enkripsi hibrida [**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf) digunakan.

## Enkripsi Hibrida KEM-DEM {#kem-dem-hybrid-encryption}


### Pembuatan Kunci {#key-creation}

Gunakan kurva Elliptic (di sini kami menggunakan kurva Baby Jubjub) `E` pada sebuah bidang `Fp` yang terbatas yaitu `p` bilangan prima besar
dan generator `G`.

Alice membuat pasangan kunci asimetris acak sementara   :
$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

Kunci ini hanya digunakan sekali dan unik hanya untuk transaksi ini, memberikan kita kerahasiaan ke depan yang sempurna.

### Enkripsi {#encryption}

Proses enkripsi melibatkan 2 langkah: langkah KEM untuk mendapatkan kunci enkripsi simetris dari rahasia yang dibagikan dan langkah DEM untuk mengenkripsi teks menggunakan kunci enkripsi.

### Metode Enkapsulasi Kunci (Enkripsi) {#key-encapsulation-method-encryption}
Menggunakan kunci privat asimetris yang dihasilkan sebelumnya, kita mendapatkan rahasia bersama, $key_{DH}$, menggunakan Diffie-Hellman standar. Kunci ini di-hash bersama kunci publik sementara untuk mendapatkan kunci enkripsi.

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


di mana  
   adalah kunci publik penerima  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### Metode Enkapsulasi Data (Enkripsi) {#data-encapsulation-method-encryption}
Untuk efisiensi sirkuit, enkripsi yang digunakan adalah sebuah sandi blok dalam mode sangkalan dengan algoritme sandi hash mimc. Mengingat kunci sementara yang unik untuk setiap transaksi, maka tidak perlu menambahkan nonce. Enkripsi pesan $i^{th}$ adalah sebagai berikut:

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

di mana  

$Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

Kemudian pengirim memberikan penerima dengan $(Q_e, \text{ciphertexts})$. Ini termasuk bagian dari struktur transaksi yang dikirim secara on-chain.

### Dekripsi {#decryption}
Untuk melakukan dekripsi, penerima melakukan langkah KEM-DEM dengan versi yang sedikit dimodifikasi.

### Metode Enkapsulasi Kunci (Dekripsi) {#key-encapsulation-method-decryption}
Mengingat $Q_e$, penerima dapat menghitung kunci enkripsi secara lokal dengan melakukan langkah berikut.

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

di mana  
  adalah kunci publik sementara  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### Metode Enkapsulasi Data (Dekripsi) {#data-encapsulation-method-decryption}
Dengan $key_{enc}$ and an array of ciphertexts, the $i_{th}$, teks dapat dipulihkan dengan berikut ini:

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

di mana  

$Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## Derivasi dan pembuatan berbagai kunci yang terlibat dalam enkripsi, kepemilikan komitmen, dan penggunaan {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

Menggunakan BIP39, buatlah 12 kata `mnemonic`, kemudian buatlah `seed` dengan memanggil `mnemonicToSeedSync`.
Kemudian mengikuti standar BIP32 dan BIP44, buat `rootKey` berdasarkan `seed` dan `path` ini.

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

Jika `rootKey` atau `mnemonic` telah disusupi, maka lawannya dapat menghitung `zkpPrivateKey` dan `nullifierKey`.
`zkpPrivateKey` dapat digunakan untuk mendekripsi rahasia komitmen, sedangkan `nullifierKey` dapat digunakan untuk menggunakan komitmen.
Maka dari itu, `rootKey` dan `mnemonic` harus disimpan dengan sangat aman.

Aplikasi yang akan menggunakan `ZkpKeys` untuk membuat kunci ini dapat menyimpan `rootKey` dalam perangkat yang berbeda dengan memecah
kunci ini menjadi beberapa bagian menggunakan Shamir Secret Sharing.

Sebaiknya, Anda juga menyimpan `zkpPrivateKey` dan `nullifierKey` secara terpisah guna menghindari pencurian komitmen jika salah satu darinya
disusupi.

Gambar di bawah ini menampilkan langkah-langkah untuk mendapatkan kunci yang berbeda di Nightfall
![](../imgs/key-derivation.png)
