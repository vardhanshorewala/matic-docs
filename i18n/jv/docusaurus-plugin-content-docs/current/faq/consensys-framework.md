---
id: consensys-framework
title: Kerangka Paningkatan Consensys
sidebar_label: Consensys Scaling Framework
description: Mbangun aplikasi blockchain panjenengan sabanjure ing Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

Kerangka kerja iki asale saka P[atang pitakonan Consensys kanggo mbiji saben solusi paningkatan](https://consensys.net/?p=19015&preview=true&_thumbnail_id=19017)

## Sapa sing ngoperasekake? {#who-operates-it}
Node panambang ing mainnet Ethereum mindhahake utawa "ngoperasikake" jaringan maju kanthi ngrampungake Proof of Work lan nggawe blok anyar. Solusi L2 mbutuhake peran "operator" sing meh padha ing jaringan iku, sing padha karo panambang mainnet Ethereum sing bisa majokake jaringan L2. Nanging, ana sawetara bedane: Contone, bebarengan karo proses lan otorisasi transaksi kaya panambang, operator L2 uga bisa nggampangake pangguna kanggo mlebu lan metu saka lapisan L2 kuwi dhewe.

### - Sapa utawa apa sing dibutuhake kanggo ngoperasekake jaringan Proof of Stake Polygon? {#who-or-what-is-required-to-operate-the-polygon-proof-of-stake-network}

Rante sing nglakokake Polygon PoS gumantung karo sakumpulan validator kanggo ngamanake jaringan kasebut. Peran validator yaiku mbukak node pepak; gawe blok, menehi validasi lan melu ing konsensus sarta nindakake checkpoint ing rante-utama Ethereum. Kanggo dadi validator, perlu pasang stake token MATIC lan kontrak manajemen staking sing manggon ing rante utama Ethereum.

Kanggo rincian liyane, pirsanana https://docs.polygon.technology/docs/validate/validator/introduction#overview

### - Kepiye carane dheweke dadi operator ing jaringan Polygon PoS? Aturan apa sing padha dituruti? {#how-do-they-become-operators-in-the-polygon-pos-network-what-rules-do-they-abide-by}

Kanggo dadi validator, dheweke perlu pasang stake token MATIC karo
kontrak manajemen staking sing manggon ing mainchain Ethereum.

Ganjaran disebarake kanggo kabeh staker sebanding karo sing stake sing dipasang ing saben checkpoint, kajaba pangusul entuk bonus tambahan. Saldo ganjaran pangguna dianyarake ing kontrak sing dimangsud nalika
njaluk ganjaran.

Stake nduweni risiko kepotong yen node validator nglakoni
tumindak mbebayani kaya tekenan dhobel, downtime validator kang uga mengaruhi
delegator sing ditautake ing checkpoint kasebut.

Kanggo rincian liyane pirsanana
https://docs.polygon.technology/docs/validate/validator/introduction#end-to-end-flow-for-a-matic-validator lan https://docs.polygon.technology/docs/validate/validator/responsibilities/#responsibilities-of-validator


### - Asumsi kapercayan kaya apa sing kudu ditindakake pangguna Polygon PoS ing babagan operator kasebut? {#what-trust-assumptions-must-the-polygon-pos-users-make-about-the-operator}

Rante sing nglakokake Polygon PoS gumantung karo sakumpulan validator kanggo ngamanake jaringan kasebut. Peran validator yaiku kanggo nglakokake node pepak; nggawe blok, menehi validasi, melu ing konsensus, lan nindakake checkpoint ing rante utama. Kanggo dadi validator, perlu pasang stake token MATIC lan kontrak manajemen staking sing manggon ing rante utama.
Anggere ⅔ stake validator sing katimbang iku jujur, rante bakal nduweni progres kanthi akurat.

### - Apa tanggung jawabe operator? Kakuwatan apa sing diduweni? {#what-are-the-operators-responsible-for-what-power-do-they-have}

Peran validator yaiku kanggo nglakokake node pepak; gawe blok, menehi validasi, melu ing konsensus, lan nindakake checkpoint ing rante utama.

Validator bisa mungkasi kamajuan rante, nyusun maneh blok, lan liya-liyane, kanthi asumsi yen ⅔ validator stake sing katimbang ora jujur. Dheweke ora duwe kuwasa ngganti kahanan, saldo aset pangguna, lsp.

### - Apa motivasine dadi operator Polygon PoS? {#what-are-the-motivations-to-become-an-operator-of-the-polygon-pos}

Validator masang stake token matic minangka jaminan kerja kanggo kaamanan jaringan lan minangka imbalan kanggo layanane, supaya entuk ganjaran.

Pirsanana https://docs.polygon.technology/docs/validate/economics#what-is-the-incentive kanggo rincian liyane.

## Kepriye Datane? {#how-s-the-data}
Miturut definisi, teknologi Lapisan 2 kudu nggawe checkpoint data tambahan ing Lapisan 1 (Ethereum mainnet). Kawigaten kita yaiku wektu interstisial antarane check-in Lapisan 1 periodik kasebut. Sacara khusus, kepiye data Lapisan 2 diasilake, disimpen, lan diurus nalika adoh saka pelabuhan aman Lapisan 1? Kita paling wigati babagan iki amarga iki kahanan nalika pangguna paling adoh saka kaamanan mainnet publik sing ora dipercaya.

### - Apa wae syarat lock-up kanggo Polygon PoS? {#what-are-the-lock-up-conditions-for-polygon-pos}

Ing akeh-akehe pola rancangan token, token kasebut dicithak ing Ethereum lan bisa dikirim menyang Polygon PoS. Kanggo mindhah token kasebut saka Ethereum menyang Polygon PoS, pangguna kudu ngunci dana ing kontrak ing Ethereum, lan token kasebut banjur dicithak ing Polygon PoS.

Mekanisme relay jembatan iki ditindakake dening validator Polygon PoS sing kudu disetujoni dening ⅔ ing prastawa token sing dikunci ing Ethereum kanggo nggawe cacahe token mau ing Polygon PoS.

Narik aset bali menyang ethereum iku proses 2 langkah ing ngendi token aset kudu dibakar dhisik ing rante sing nglakokake Polygon PoS lan banjur bukti transaksi sing dibakar iki kudu dikirim ing rante Ethereum.


Kanggo rincian liyane, pirsanana https://docs.polygon.technology/docs/develop/ethereum-polygon/pos/getting-started#steps-to-use-the-pos-bridge

### - Sepira suwene dana kasebut sumadhiya ing Polygon PoS? {#how-soon-are-those-funds-available-on-the-polygon-pos}

Kira-kira ~ 22-30 menit. Iki ditindakake liwat mekanisme pesen sing diarani.`state sync` Rincian liyane bisa ditemokake ing kene: https://docs.polygon.technology/docs/pos/state-sync/state-sync/

Apa Polygon PoS nyedhiyakake dhukungan kanggo pangguna sing mlebu tanpa kunci L1 (yaiku, yen pangguna langsung mlebu menyang Polygon, banjur pangguna pengin metu menyang mainnet Ethereum)?

Ya, mekanisme jembatan khusus digunakake kanggo nuntasake iki. Nalika pangguna pengin metu menyang Ethereum, tinimbang cara biasa kanggo mbukak kunci token saka kontrak khusus, iki dicithak.

Panjenengan bisa maca kuwi ing kene: https://docs.polygon.technology/docs/develop/ethereum-polygon/pos/mintable-assets

### - Kepiye pangguna bakal mbantah transaksi Polygon PoS sing ora bener? Mbuktekake transaksi Polygon PoS sing bener? {#how-would-a-user-dispute-an-invalid-polygon-pos-transaction-prove-a-valid-polygon-pos-transaction}

Saiki ora ana cara on-chain kanggo mbantah transaksi Polygon PoS sing ora bener. Nanging, validator rante Polygon PoS ngirim checkpoint periodik menyang Ethereum - panjenengan bisa mirsani rincian liyane ing kene: https://docs.polygon.technology/docs/pos/heimdall/modules/checkpoint/
Panjenengan bisa verifikasi transaksi ing rante Polygon PoS ing Ethereum kanthi mbangun bukti wit Merkle lan verifikasi marang checkpoint periodik sing kedadeyan ing Ethereum saka transaksi Polygon PoS lan nampa root wit Merkle.

Yen pangguna Polygon pengin metu, sepira suwene dana Lapisan 1 sing dikunci (ditambah utawa dikurangi karo keuntungan utawa kerugian L2) sumadhiya maneh ing L1?

Kira-kira ~ 1-3 jam gumantung saka frekuensi checkpoint (https://docs.polygon.technology/docs/pos/heimdall/modules/checkpoint/). Frekuensi kasebut utamane minangka fungsi saka beya sing bakal dibayarake dening validator kanggo ongkos gas ETH kanggo ngirimake checkpoint.

### - Apa panjenengan ngarepake ana Penyedhiya Likuiditas ing Lapisan 1 sing gelem nyedhiyakake dana L1 sing bisa ditebus langsung kanggo pangguna Polygon PoS sing wis ana? {#do-you-anticipate-there-being-liquidity-providers-on-layer-1-willing-to-provide-immediately-redeemable-l1-funds-to-existing-polygon-pos-users}

Wis ana sawetara pemain kayata https://connext.network/ (wis tayang) lan https://biconomy.io/ sing nyedhiyakake utawa bakal nyedhiyakake layanan iki. Ana sawetara pemain liya sing uga bakal tayang sacepete.

## Stack iku kepriye? {#how-s-the-stack}
Mbandhingake stack penting kanggo nyorot apa Lapisan 2 wis diganti utawa ora diganti saka Ethereum mainnet.

### - Sepira akehe stack Polygon PoS sing melu diduweni stack Ethereum mainnet? {#how-much-does-the-polygon-pos-stack-share-with-the-ethereum-mainnet-stack}

Yen panjenengan sawijining Developer Ethereum, panjenengan wis dadi developer Polygon PoS. Kabeh alat sing panjenangan akrabi didhukung ing Polygon PoS sacara langsung: Truffle, Remix, Web3js, lan liya-liyane.

Ora ana owah-owahan gedhe ing antarmuka EVM kanggo Polygon PoS relatif marang Ethereum.

### - Apa bedane Polygon PoS karo stack Ethereum mainnet lan apa risiko/ganjarane? {#where-does-the-polygon-pos-differ-from-ethereum-mainnet-stack-and-what-risks-rewards-does-that-introduce}

Ora ana owah-owahan gedhe.

## Nyiapake kanggo sing paling Ala {#preparing-for-the-worst}
Kepiye sistem Polygon PoS nyiapake kanggo:

### - Para pangguna rame-rame padha metu? {#a-mass-exit-of-users}

Anggere ⅔ saka validator jujur, dana ing rante aman. Yen asumsi iki ora bener, ing skenario kuwi rante bisa mandheg utawa nata maneh bisa kelakon. Konsensus sosial bakal dibutuhake kanggo miwiti maneh rante saka kahanan sadurunge - kalebu snapshot saka kahanan Polygon PoS sing dikirim liwat checkpoint sing bisa digunakake kanggo nindakake iki.

### - Peserta Polygon nyoba mainake konsensus Polygon. Contone, kanthi gawe kartel? {#polygon-participants-attempting-to-game-the-polygon-consensus-for-example-by-forming-a-cartel}

Konsensus sosial bakal dibutuhake kanggo miwiti maneh rante saka kahanan sadurunge kanthi mbusak validator kasebut lan miwiti maneh nganggo set validator anyar - kalebu snapshot saka kahanan Polygon PoS sing dikirim liwat checkpoint sing bisa digunakake kanggo nindakake iki.


### - Bug utawa eksploit sing ditemokake ing bagean kritis sisteme? {#a-bug-or-exploit-discovered-in-a-critical-part-of-its-system}

Tuumindak ngati-ati wis dilakoni kanggo migunakake maneh komponen sing wis diuji nalika nggawe sistem iku. Nanging, yen ana bug utawa eksploit ing bagean kritis sistem, mulihake rante menyang kahanan sing sadurunge liwat konsensus sosial iku solusi sing utama.
