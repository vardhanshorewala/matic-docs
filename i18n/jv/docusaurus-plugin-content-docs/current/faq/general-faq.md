---
id: general-faq
title: Pitakonan Umum
description: Pitakonan umum ing jaringan Polygon.
keywords:
  - docs
  - matic
  - polygon
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

## Apa iku Jaringan Polygon? {#what-is-polygon-network}

Jaringan Polygon yaiku solusi paningkatan Lapisan 2 sing nggayuh skala kanthi migunakake sidechain kanggo komputasi off-chain, sinambi njamin kaamanan aset lan desentralisasi liwat validator Proof-of-Stake (PoS).

Pirsanana uga [Apa iku Polygon](/docs/home/polygon-basics/what-is-polygon).

## Apa iku Proof of Stake (PoS)? {#what-is-proof-of-stake-pos}

Proof-of-Stake yaiku sistem ing ngendi jaringan blockchain duwe tujuan nggayuh konsensus sing didistribusekake. Sapa wae sing duwe cukup token bisa ngunci mata uang kriptone lan insentif ekonomi ana ing nilai jaringan desentralisasi sing digunakake bebarengan. Individu sing staking mata uang kriptone nindakake validasi transaksi kanthi sing padha dene konsensus kagayuh nalika transaksi utawa sakumpulan transaksi ing blok utawa sakumpulan blok ing checkpoint entuk cukup pamilih. Ambang wates migunakake bobot miturut stake sing dientukake ing saben pamilihan. Contone, ing Polygon, konsensus digayuh kanggo nindakake checkpoint blok Polygon menyang jaringan Ethereum, dene saorane ⅔+1 saka total kuwasa staking milih iki.

Pirsanana uga [Apa iku Proof of Stake](/docs/home/polygon-basics/what-is-proof-of-stake).

## Apa peran Proof-of-Stake ing arsitektur Polygon? {#what-role-does-proof-of-stake-play-in-the-polygon-architecture}

Lapisan Proof-of-Stake ing arsitektur Polygon nduweni 2 tujuan ing ngisor iki:

* Tumindak minangka lapisan insentifisasi kanggo njaga uripe rante Plasma, utamane mitigasi masalah sing njengkelake amarga ora sumadhiyane data.
* Nerapake jaminan kaamanan Proof-of-Stake kanggo transisi kahanan sing ora bisa diatasi dening Plasma.

## Kepiye bedane Polygon PoS karo sistem liyane sing meh padha? {#how-is-polygon-pos-different-from-other-similar-systems}

Bedane yaiku Polygon PoS nglayani dwi tujuan — nyedhiyakake jaminan sumadhiyane data kanggo rante Plasma sing nyakup transisi kahanan liwat Predikat Plasma, sarta validasi Proof-of-Stake kanggo kontrak pinter generik ing EVM.

Arsitektur Polygon uga misahake proses produksi blok lan validasi dadi 2 lapisan sing beda. Validator minangka produsen blok nggawe blok kaya jenenge ing rante Polygon kanggo konfirmasi saperangan sing luwih cepet (<2 detik), nalika konfirmasi pungkasan digayuh sawise checkpoint ditindakake ing rante utama kanthi interval tartamtu, sing bisa beda-beda gumantung saka pirang-pirang faktor kayata macete Ethereum utawa jumlah transaksi Polygon. Ing kahanan ideal, kudune udakara 15 menit nganti 1 jam.

Checkpoint iku sejatine root Merkle saka kabeh blok sing diprodhuksi ing antarane interval. Validator nindakake pirang-pirang peran, nggawe blok ing lapisan produsen blok, melu konsensus kanthi nekeni kabeh checkpoint, lan nindakake checkpoint nalika tumindak minangka pangusul. Probabilitas validator dadi produsen blok utawa pangusul adhedhasar rasio stake ing sakabehing kumpulan.

## Nyengkuyung pangusul kanggo ngatutake kabeh teken {#encouraging-the-proposer-to-include-all-signatures}

Supaya bisa entuk bonus pangusul kanthi lengkap, pangusul kudu ngatutake kabeh teken ing checkpoint. Amarga protokol mbutuhake 2/3+1 bobot saka stake total, checkpoint bakal ditampa sanajan mung entuk 80% pamilih. Nanging, ing kasus iki, pangusul mung entuk 80% saka bonus sing diwilang.

## Kepiye carane bisa entuk tiket dhukungan utawa nyumbang kanggo dokumentasi Polygon? {#how-can-i-raise-a-support-ticket-or-contribute-to-polygon-documentation}
Yen panjenengan rumangsa ana sing kudu didandani ing dokumentasi kita utawa panjenengan ngersakake nambahai informasi anyar ing kene, panjenengan bisa [mundhut priksa ing repositori Github](https://github.com/maticnetwork/matic.js/issues). File [Readme](https://github.com/maticnetwork/matic-docs/blob/master/README.md) ing repositori uga nyedhiyakake sawetara saran babagan carane maringi kontribusi kanggo dokumentasi kita.

Yen panjenengan isih ngersakake pitulungan, panjenengan bisa tansah nimbali **tim dhukungan kita**.
