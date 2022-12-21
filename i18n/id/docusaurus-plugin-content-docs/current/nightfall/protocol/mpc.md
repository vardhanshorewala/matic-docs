
# Seremoni MPC {#mpc-ceremony}
Zero-Knowledge Proof memerlukan pengaturan yang tepercaya. Pengaturan ini menghasilkan sesuatu yang disebut "limbah beracun" yang berpotensi memungkinkan terciptanya bukti yang palsu. Untuk menghindari hal ini, sebuah seremoni harus diadakan yaitu pengaturan ini dibuat melalui komputasi multipihak (MPC).

Nightfall menjalankan Komputasi Multi-Pihak (MPC) mengikuti prinsip-prinsip yang sama dari Kekuatan Abadi Seremoni Tau. Proses tersebut dimulai dengan kontribusi 72 dari Kekuatan Abadi Seremoni Tau untuk Kurva BN254. Anda dapat menemukan [kontribusi](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response) ini di sini.

Karena Nightfall menggunakan skema pembuktian Groth16, maka diperlukan MPC fase kedua untuk setiap sirkuit. Ada 4 kontribusi pribadi sebagai bagian dari fase 2 ini:

1. [Darko Macesic (github ID: dark64)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna (github ID: jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody (EY Global Blockchain Leader)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor (github ID: iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

Setelah kontribusi terakhir, kami menerapkan suar acak untuk 4 sirkuit tersebut. Untuk suar ini, kami membuat [transaksi](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1) mainnet dengan muatan data 0xe095cb (14718411 dalam angka desimal).

Transaksi ini dimasukkan dalam nomor blok [14711908](https://etherscan.io/block/14711908), yang
mendarat pada 5 Mei 2022 pukul 17:00:27 +UTC dan memiliki blockhash
`0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3`.
Kemudian, hash ini dilakukan hash secara rekursif sebanyak 1.024 kali. Keluarannya adalah `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`.

Hash terakhirnya dikomputasi dengan program ini:

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

Informasi lengkap tentang fase 2 dapat ditemukan [di sini](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md).

