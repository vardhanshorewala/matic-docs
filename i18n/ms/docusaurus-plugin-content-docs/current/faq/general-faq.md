---
id: general-faq
title: Soalan Lazim Umum
description: Soalan lazim mengenai rangkaian Polygon.
keywords:
  - docs
  - matic
  - polygon
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

## Apakah Rangkaian Polygon? {#what-is-polygon-network}

Rangkaian Polygon ialah penyelesaian penskalaan Lapisan 2 yang mencapai skala dengan menggunakan rantaian sisi untuk pengiraan luar rantaian, sambil memastikan sekuriti aset dan desentralisasi melalui pengesah Bukti Pegangan (PoS).

Lihat juga [Apakah Polygon](/docs/home/polygon-basics/what-is-polygon).

## Apakah Bukti Pegangang (PoS)? {#what-is-proof-of-stake-pos}

Bukti Pegangan ialah sistem di mana rangkaian blok rantai bertujuan untuk mencapai konsensus yang diedarkan. Sesiapa sahaja yang mempunyai jumlah token yang mencukupi boleh mengunci mata wang kriptografi mereka dan insentif ekonomi terletak pada nilai kongsi rangkaian tak terpusat. Individu yang memegang mata wang kripto mereka mengesahkan urus niaga dengan mengundi pada perkara yang sama manakala konsensus dicapai apabila urus niaga atau satu set urus niaga dalam blok atau satu set blok dalam pusat pemeriksaan menerima undian yang mencukupi. Ambang menggunakan berat dari segi kepentingan yang disertakan dengan setiap undi. Sebagai contoh, dalam Polygon, konsensus dicapai untuk melakukan pusat pemeriksaan blok Polygon ke rangkaian Ethereum, apabila sekurang-kurangnya ⅔ +1 daripada jumlah undi kuasa mempertaruhkan untuk ini.

Lihat juga[Apa Itu Bukti Pegangan](/docs/home/polygon-basics/what-is-proof-of-stake).

## Apakah peranan yang dimainkan oleh Bukti Pegangan dalam seni bina Polygon? {#what-role-does-proof-of-stake-play-in-the-polygon-architecture}

Lapisan Bukti Pegangan dalam seni bina Polygon berfungsi untuk 2 tujuan berikut:

* Bertindak sebagai lapisan insentif untuk mengekalkan keaktifan rantaian Plasma, terutamanya mengurangkan isu pedih tentang ketidaktersediaan data.
* Laksanakan jaminan sekuriti Bukti Pegangan untuk peralihan keadaan yang tidak dilindungi oleh Plasma.

## Bagaimanakah PoS Polygon berbeza daripada sistem lain yang sama? {#how-is-polygon-pos-different-from-other-similar-systems}

Ia berbeza dalam erti kata ia berfungsi untuk dua tujuan — menyediakan jaminan ketersediaan data untuk rantaian Plasma yang meliputi peralihan keadaan melalui Predikat Plasma, serta pengesahan Bukti Pegangan untuk kontrak pintar generik dalam EVM.

Seni bina Polygon juga memisahkan proses pengeluaran blok dan pengesahan kepada 2 lapisan yang berbeza. Pengesah sebagai pengeluar blok membuat blok seperti yang dicadangkan oleh namanya pada rantai Polygon untuk pengesahan separa yang lebih cepat (< 2 saat) manakala pengesahan akhir dicapai sebaik sahaja pusat pemeriksaan dilakukan pada rantaian utama dengan selang waktu tertentu, tempoh yang mungkin berbeza-beza bergantung pada pelbagai faktor seperti kesesakan Ethereum atau bilangan transaksi Polygon. Dalam keadaan yang ideal, ia mestilah sekitar 15 minit hingga 1 jam.

Titik Semak pada asasnya ialah punca Merkle bagi semua blok yang dihasilkan di antara selang waktu. Pengesah memainkan berbilang peranan, mencipta blok pada lapisan pengeluar blok, mengambil bahagian dalam konsensus dengan menandatangani semua titik semak dan melakukan titik semak apabila bertindak sebagai pencadang. Kebarangkalian pengesah menjadi pengeluar atau pencadang blok adalah berdasarkan nisbah pegangan mereka dalam kumpulan keseluruhan.

## Menggalakkan pencadang memasukkan semua tandatangan {#encouraging-the-proposer-to-include-all-signatures}

Untuk memanfaatkan bonus pencadang sepenuhnya, pencadang perlu memasukkan semua tandatangan dalam pusat pemeriksaan. Kerana protokol inginkan 2/3+1 berat daripada jumlah pegangan, pusat pemeriksaan akan diterima walaupun dengan 80% undian. Walau bagaimanapun, dalam kes ini, pencadang hanya mendapat 80% daripada bonus yang dikira.

## Bagaimanakah saya boleh meningkatkan tiket sokongan atau menyumbang kepada dokumentasi Polygon? {#how-can-i-raise-a-support-ticket-or-contribute-to-polygon-documentation}
Jika anda rasa sesuatu perlu dibetulkan pada dokumentasi kami atau anda mahu menambah maklumat baharu di sini, anda boleh [menimbulkan isu pada repositori Github](https://github.com/maticnetwork/matic.js/issues). Fail[Readme pada ](https://github.com/maticnetwork/matic-docs/blob/master/README.md)repositori juga memberi anda beberapa cadangan tentang cara menyumbang kepada dokumentasi kami.

Jika anda masih memerlukan bantuan, anda boleh menghubungi **pasukan sokongan kami pada bila-bila masa**.
