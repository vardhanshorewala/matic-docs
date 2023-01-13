---
id: wallet-bridge-faq
title: Pitakonan Umum Jembatan <>Dhompet
description: Mbangun aplikasi blockchain panjenengan sabanjure ing Polygon.
keywords:
  - docs
  - matic
  - wallet
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## Ing endi aku bisa nggunakake Dhompet Web Matic? {#where-can-i-use-the-matic-web-wallet}
[https://wallet.polygon.technology/](https://wallet.polygon.technology/)

## Kepriye carane nemokake kontrak token? {#how-do-i-find-the-token-contract}

Wacanen artikel [Nambahake Token Kustom](../faq/adding-a-custom-token) iki

## Dhompet endi sing saiki didhukung? {#which-wallets-are-currently-supported}

- Metamask
- Coinbase Wallet
- Sambung Dhompet

Kita bakal enggal nambahake dompet liyane.

## Kaya apa bedane Plasma karo PoS? {#how-is-plasma-different-from-pos}

Plasma nduweni kaamanan tambahan. 
Priksanen: [https://docs.polygon.technology/docs/develop/ethereum-polygon/getting-started](https://docs.polygon.technology/docs/develop/ethereum-polygon/getting-started)

## Token apa sing mung sumadhiya ing Plasma? {#what-tokens-are-only-available-on-plasma}

Token Polygon

## Kepriye carane deposit menyang Dhompet Polygon lan uga narik? {#how-do-i-deposit-to-polygon-wallet-and-also-withdraw}

Blog lan video iki minangka pandhuan sing sampurna kanggo miwiti setor lan narik: 

Dokumentasi: [https://docs.polygon.technology/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/#depositing-funds-from-ethereum-to-matic](https://docs.polygon.technology/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/#depositing-funds-from-ethereum-to-matic)

Video: [https://www.youtube.com/playlist?list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9](https://www.youtube.com/playlist?list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9)

## Kepriye carane ngalih menyang mainnet Polygon ing Metamask? {#how-to-switch-to-polygon-mainnet-in-metamask}

Yen panjenengan wis nambahake jaringan lan RPC kustom kanggo mainnet Polygon ing dhompet Metamask panjenengan, kaya ngene carane panjenengan bisa ngalihake:

1. Bukak dhompet Metamask banjur klik dropdown jaringan kanggo nggedhekake kaya sing ditampilake ing gambar:

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-1.png")} width="30%" height="30%" />

1. Sawise jendhela digedhekake panjenengan bisa milih Mainnet Polygon kanggo ngalihake:

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-2.png")} width="357" height="600" />

Panjenengan saiki wis ngalih menyang Mainnet Polygon.

Panjenengan bisa mirsani tautan iki yen panjenengan nggoleki instruksi babagan carane nambahake jaringan menyang Metamask: [https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-metamask/](https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-metamask/)

## Kepriye carane milih mainnet Polygon ing Walletlink? {#how-to-choose-polygon-mainnet-in-walletlink}

Tutna pandhuan sing diwenehake ing [kene](https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-wallets#configure-polygon-on-walletlink)

## Aku wis setor WETH nanging aku ora weruh ing Metamask. Apa sing kudu dak lakoni? {#i-have-deposited-weth-but-i-don-t-see-it-on-metamask-what-do-i-do}

Panjenengan perlu nambahake alamat token kustom WETH menyang Metamask sacara manual.

Bukak Metamask banjur gulung mudhun kanggo ngeklik **Impor token**.

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-3.png")} width="357" height="600" />


Banjur, tambahana alamat kontrak, simbol, lan presisi desimal sing gegayutan. Alamat kontrak (PoS-WETH ing kasus iki) bisa ditemokake ing tautan iki: [https://docs.polygon.technology/docs/develop/network-details/mapped-tokens/](https://docs.polygon.technology/docs/develop/network-details/mapped-tokens/). Panjenengan kudu nambahake alamat token anak kanggo mirsani saldo ing Mainnet Polygon. Presisi desimal yaiku 18 kanggo WETH (kanggo umume presisi desimal token yaiku 18).

Sawise panjenengan ngisi kabeh kolom, panjenengan bisa ngeklik **Tambah Token Kustom** lan token panjenengan bakal ditambahake.

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-4.png")} width="357" height="600" />


## Apa aku bisa ngirim token saka Polygon menyang dhompet/bursa liyane ? {#can-i-send-my-tokens-from-polygon-to-any-other-wallet-exchange}

Panjenengan ora bisa langsung ngirim token saka Polygon UI menyang Bursa/dhompet. Panjenengan kudu narik dhisik saka Polygon menyang Ethereum banjur ngirim menyang alamat bursa (kajaba bursa/ dhompet panjenengan ndhukung jaringan kasebut).

## Aku salah ngirim dana menyang bursa/dhompet sacara langsung. Apa panjenengan bisa nulungi? {#i-made-a-mistake-of-sending-funds-to-an-exchange-wallet-directly-can-you-help}

Sayange, kita ora bisa nulungi ing kasus sing kaya mengkono. Aja ngirim dana langsung menyang bursa sing mung ndhukung Ethereum, panjenengan kudu narik dhisik saka Polygon menyang Ethereum banjur ngirim menyang alamat bursa.

## Transaksiku katundha suwe banget, apa sing bisa ditindakake? {#my-transaction-is-pending-for-too-long-what-can-i-do}

Transaksi ing blockchain bisa uga mudhun amarga rega gas murah nalika ngirim transaksi kasebut. Bisa uga mudhun nalika rega gas mundhak amarga kemacetan ing Ethereum. Kamungkinan liyane yaiku panjenengan bisa uga mbatalake transaksi saka dompet utawa ngganti transaksi kasebut. Ing kabeh kasus kasebut, web dhompet bakal nuduhake pesen transaksi sing lagi ditindakake lan iki bakal njalari panjenengan ngenteni luwih suwe.

Yen transaksi macet luwih saka sejam, tombol "Coba maneh" bakal ditampilake. Iki apik, tegese panjenengan bisa mundhut jaringan supaya nyoba maneh transaksi kanggo panjenengan. Apa sing bisa ditindakake sabanjure yaiku ngeklik tombol "Coba maneh" kanggo nyoba maneh transaksi mau. Yen transaksi setor panjenengan macet, proses setor bakal diwiwiti maneh lan yen transaksi tarik panjenengan macet, panjenengan bakal bisa terus narik saka langkah pungkasan sing wis dirampungake.

Yen panjenengan nemoni masalah nalika nerusake tombol "Coba maneh" lan panjenengan migunakake dhompet Metamask, panjenengan bisa uga perlu mriksa manawa ana akeh transaksi sing antri sing njalari macet ing bagean aktivitas metamask. Ing kasus iki, bisa uga migunani yen panjenengan nginstal maneh dhompet metamask banjur nerusake transaksi panjenengan. Utawa, panjenengan bisa nyoba miwiti transaksi saka browser kapisah.

Mirsani video ing ngisor iki bisa menehi kajelasan babagan carane nggunakake fitur "Coba maneh"

[https://youtu.be/0b4yjR_naEQ](https://youtu.be/0b4yjR_naEQ)

## Dhaptar Bursa apa bae sing Didhukung ing Polygon? {#what-are-the-list-of-supported-exchanges-on-polygon}

Ing ngisor iki dhaptar bursa terpusat sing saiki ndhukung Polygon lan uga token sing didhukung bursa iki.

AscendEX - USDC, EASY, MATIC

MXC - MATIC, QUICK, PlotX, Dfyn

Okcoin - ETH, USDT, LINK, MKR, USDC, DAI, USDK, COMP, YFI, SNX, YFII, and UNI. (Token mung bisa dipindhah saka Okcoin menyang rante Polygon. Nransfer token saka Polygon menyang Okcoin saiki ora didhukung)

Okex - BAL, BAT, CEL, COMP, CRV, DAI, ETH, GHST, GUSD, LINK, MKR, PAX, SNX, SUSHI, TUSD, UNI, USDC-ERC20, USDT-ERC20, USDK, wBTC, YFI, YFII, ZRX (Token mung bisa dipindhahake saka Okex menyang rante Polygon. Transfer token saka Polygon menyang Okex saiki ora didhukung)

Bitforex - MATIC

Ngirim Token menyang bursa liyane sing ora kasebut kanthi jelas ing dhaptar ing ndhuwur bisa njalari dana ilang. Yen panjenengan pengin narik dana menyang bursa apa bae sing ora ndhukung Polygon, panjenengan kudu narik token kasebut menyang Ethereum lan banjur ngirim menyang bursa nggunakake dhompet Ethereum. Video iki nuduhake carane narik dana saka Polygon menyang Ethereum - [https://www.youtube.com/watch?v=DgpHY95qrbQ&list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9&index=5](https://www.youtube.com/watch?v=DgpHY95qrbQ&list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9&index=5)

Utawa, panjenengan bisa nindakake pandhuan iki ng [kene](https://docs.matic.today/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/).

## Aku ora bisa login, apa sing kudu dak lakoni? {#i-am-not-able-to-login-what-do-i-do}

[https://docs.polygon.technology/docs/validate/delegator-faq/#my-metamask-is-stuck-at-confirming-after-login-what-do-i-do-or-nothing-happens-when-i-try-to-login](https://docs.polygon.technology/docs/validate/delegator-faq/#my-metamask-is-stuck-at-confirming-after-login-what-do-i-do-or-nothing-happens-when-i-try-to-login)

## Apa Polygon ndhukung dhompet piranti keras? {#does-polygon-support-hardware-wallets}
Ya, dhompet piranti keras didhukung.

## Apa sing bisa ngapa bae nganggo dhompet Polygon? {#what-can-i-do-with-my-polygon-wallet}

- Ngirim dana menyang akun apa bae ing Polygon.
- Deposit dana saka Ethereum menyang Polygon (nggunakake jembatan).
- Narik dana bali menyang Ethereum saka Polygon (uga nggunakake jembatan).

## Tokenku ora katon ing dhaptar. Sapa sing kudu dak hubungi? {#my-token-is-not-visible-in-the-list-who-should-i-contact}

Mangga kontak tim Polygon ing Discord utawa Telegram lan mundhuta supaya token panjenengan didhaptar. Sadurunge, pesthekake token panjenengan wis dipetakake. Yen durung dipetakake, kirim panyuwunan ing [https://mapper.polygon.technology/](https://mapper.polygon.technology/)

## Endi praktik paling apik sing bisa dak tindakake? {#what-are-some-best-practices-to-follow}

- Yen panjenengan pengin ngirim dana saka Polygon menyang Ethereum, gunakna fungsi penarikan. Aja nggunakake fungsi ngirim. Iki bakal njalari dana ilang.
- Aja setor menyang mainnet Polygon yen panjenengan mung pengin melu staking.
- Aja ngowahi watesan gas saka Metamask.

## Apa sing kudu ditindakake yen setoran dikonfirmasi nanging saldo ora dianyarake? {#what-do-i-do-if-the-deposit-is-confirmed-but-the-balance-is-not-getting-updated}

Perlu 22-30 menit supaya transaksi setoran rampung. Enteni sawetara wektu lan klik ing "segerake saldo".

## Apa sing kudu ditindakake yen checkpoint ora kedadeyan? {#what-should-i-do-if-the-checkpoint-is-not-happening}

Checkpoints kadhangkala mbutuhake wektu luwih saka 45 menit nganti 1 jam gumantung kemacetan jaringan ing Ethereum, disaranake ngenteni sawetara wektu sadurunge ngirim tiket.

## Apa bisa mbatalake transaksi penarikan? {#is-it-possible-to-cancel-a-withdraw-transaction}

Ora, panjenengan kudu ngrampungake langkah sabanjure. Yen rega gas saiki dhuwur banget, banjur entenana lan coba mengko yen regane mudhun.

## Apa sebabe token MATIC ora didhukung ing PoS? {#why-is-the-matic-token-is-not-supported-on-pos}

MATIC iku token asli Polygon lan duwe alamat kontrak - 0x0000000000000000000000000000000000001010 ing rante Polygon. Iki uga digunakake kanggo mbayar gas. Metaake token MATIC ing jembatan PoS bakal njalari MATIC duwe alamat kontrak tambahan ing rante Polygon. Iki bakal tabrakan karo alamat kontrak sing wis ana amarga alamat token anyar iki ora bisa digunakake kanggo mbayar gas lan kudu tetep minangka token ERC20 normal ing rante Polygon. Mula, kanggo ngendhani kebingungan iki, diputusake supaya nahan MATIC mung ing Plasma.

## Kepriye carane aku metaake token? {#how-do-i-map-tokens}

Kirim panyuwunan pametaan ing [https://mapper.polygon.technology/](https://mapper.polygon.technology/)

## Apa sing kudu ditindakake yen transaksi suwe banget utawa yen rega gas dhuwur banget? {#what-do-i-do-if-the-transaction-is-taking-too-long-or-if-the-gas-price-is-too-high}

Wektu transaksi lan rega gas beda-beda gumantung kemacetan jaringan. Yen rega gas dhuwur dibayar, transaksi bakal dikonfirmasi luwih cepet.

## Apa aku bisa ngowahi watesan gas utawa rega gas? {#can-i-change-the-gas-limit-or-the-gas-price}

Watesan gas dikira-kira lan disetel dening aplikasi miturut syarat tartamtu saka fungsi sing disebut ing kontrak. Iki ora oleh diowahi. Mung rega gas sing bisa diowahi kanggo nambah utawa nyuda beya transaksi.

## Apa sing kudu ditindakake yen transaksi dibatalake nanging dhompet web nuduhake transaksi wis rampung? {#what-should-i-do-if-the-transaction-was-cancelled-but-the-web-wallet-shows-transaction-is-completed}

Mangga kontak tim dhukungan kita.

## Ing ngendi aku ngirim tiket dhukungan? {#where-do-i-raise-a-support-ticket}
https://support.polygon.technology/support/home

## Rega gas luwih saka jumlah sing pengin dak tarik. {#the-gas-price-is-more-than-the-amount-i-seek-to-withdraw}

Transaksi tarikan nganggo jembatan Plasma diperang dadi 3 langkah, sak langkah kedadeyan ing Mainnet Polygon lan rong langkah sing bakal dirampungake ing Mainnet Ethereum. Ing jembatan PoS, transaksi tarikan dumadi liwat rong langkah: Pambakaran Token ing jaringan Polygon lan pangiriman bukti ing jaringan Ethereum. Ing mainnet Polygon, beyane minimal banget, lan bagean sing gedhe saka beya transaksi sing panjenengan pirsani yaiku rega gas ing Jaringan Ethereum sing diatur dening penambang Ethereum. Kaya sing bisa diarepake, beya iki ora bisa kita kontrol, lan kita ora duwe akeh pengaruh babagan rega. Sing pungkasan, yen token panjenengan dibakar, panjenengan bisa uga kudu nerusake narik tanpa kuwi amarga ora ana sing bisa ditindakake kanggo mbalikake proses kasebut.


## Apa aku bisa mbatalake transaksi tarikan? {#can-i-cancel-my-withdrawal-transaction}

Sayange, Polygon ora bisa mbatalake tarikan sawise proses diwiwiti lan token kasil dibakar. Hash sing dibakar digawe lan fase sabanjure transaksi teka sanalika kuwi. Yen transaksi sing dibakar isih katundha, panjenengan bisa nggampangake pambatalan liwat pandhuan ing ngisor iki

[Metamask](https://metamask.zendesk.com/hc/en-us/articles/360015489251-How-to-Speed-Up-or-Cancel-a-Pending-Transaction) <br />
[Walletlink](https://www.techdreams.org/crypto-currency/how-to-cancel-a-pending-ethereum-transaction-on-coinbase-wallet/10159-20210412)


## Transaksiku macet. {#my-transaction-is-stuck}

Kita wis nyathet sawetara error umum sing bisa dialami pangguna. Panjenengan bisa nemokake solusi ing ngisor gambar error. Yen panjenengan nemoni error sing beda, [kirim tiket dhukungan](https://support.polygon.technology/support/home) menyang tim kita kanggo pamecahan masalah.

  - ### Error Umum {#common-errors}
a. Tarikan macet ing fase Inisialisasi.

    <img src={useBaseUrl("img/wallet-bridge/plasma-progress-stuck.png")} width="357" height="800"/>

    Iki biasane kedadeyan nalika transaksi diganti lan aplikasi web dhompet ora bisa ndeteksi hash transaksi sing diganti. Mangga nindakake instruksi ing [https://withdraw.polygon.technology/](https://withdraw.polygon.technology/) lan rampungake penarikan sampeyan.

 b. Error RPC

    <img src={useBaseUrl("img/wallet-bridge/checkpoint-rpc-error.png")} width="357" height="600"/>

    RPC Error sing lagi panjenengan adhepi bisa uga amarga kakehan RPC.

    Coba ganti RPC panjenengan lan nerusake transaksi. Panjenengan bisa ngetutake tautan iki ing [kene](https://docs.polygon.technology/docs/develop/network-details/network#matic-mainnet) kanggo informasi luwih lengkap.

 c.

  <img src={useBaseUrl("img/wallet-bridge/checkpoint-stumbled-error.png")} width="357" height="600"/>

 Iki biasane Error mati-lan-urip sing bakal diatasi kanthi otomatis. Yen panjenenga isih ngalami error sing padha nalika miwiti langkah iku maneh, [kirimna tiket dhukungan](https://support.polygon.technology/) nganggo kabeh informasi sing gegayutan kanggo ngrampungake masalah iki.

## Aku salah ngirim dana menyang bursa/dhompet langsung saka Dhompet Polygon. Apa panjenengan bisa nulungi? {#i-made-the-mistake-of-sending-funds-to-an-exchange-wallet-directly-from-polygon-wallet-can-you-help}

Sayange, nyuwun pangapura yen kita ora bisa nulung panjenengan yen panjenengan wis ngirim token saka jaringan Polygon menyang bursa/dhompet sing ora didhukung.

Iki sing kudu ditindakake dening bursa ing kasus iki (sanajan ora yakin sepira luwese eksekutif pandhukung bisa nindakake iki). Yen eksekutif dhukungan bursa duwe akses menyang kunci privat akun kasebut, dheweke bisa transfer dana saka akun ing Polygon menyang alamat panjenengan (pangguna) ing Polygon.

Penting kanggo dicathet yen panjenengan kudune ora ngirim dana langsung menyang bursa sing mung ndhukung Ethereum. Prosedur sing bener yaiku panjenengan kudu narik dhisik saka Polygon menyang Ethereum banjur ngirim menyang alamat bursa panjenengan.

## Aku ngalami error saldo ora cukup. {#i-m-shown-an-insufficient-balance-error}

Tarikan lan setoran ing jaringan Polygon iku murah. Sing kudu dimangerteni yaiku error saldo sing ora cukup bisa diilangi kanthi ngentukake sawetara saldo ETH ing mainnet ethereum. Sing umume ngrampungake masalah saldo sing ora cukup.

Yen iki sawijining transaksi ing mainnet Polygon, kita bakal nyuwun panjenengan duwe saldo token matic sing cukup.

## Kepriye carane jembatani aset antar rante? {#how-do-i-bridge-assets-across-chains}

[https://wallet.polygon.technology/bridge/](https://wallet.polygon.technology/bridge/) (ETH <-> Polygon) <br/>
[https://xpollinate.io/](https://xpollinate.io/) (BSC <-> Polygon <-> xDai) <br/>
[https://exchange.chainswap.com/](https://exchange.chainswap.com/) (ETH <-> Polygon/BSC) <br/>
[https://anyswap.exchange/bridge](https://anyswap.exchange/bridge) (ETH <-> Polygon <-> BSC/xDai) <br/>
[https://app.0.exchange/#/home](https://app.0.exchange/#/home)(ETH <-> Polygon <-> Avalanche <-> BSC)

Kanggo nambahake, kita ora nganggo layanan eksternal, pesthekna yen panjenengan tansah nindakake riset dhewe

## Aku tansfer menyang alamat sing salah. Kepriye carane nompo maneh dana kasebut? {#i-made-a-transfer-to-the-wrong-address-how-do-i-retrieve-the-funds}

Sayange, ora ana sing bisa ditindakake. Mung sing duwe kunci privat menyang alamat tartamtu sing bisa mindhahake aset kasebut.


## Transaksiku ora katon ing panjelajah. Apa sing kudu ditindakake? {#my-transactions-are-not-visible-on-the-explorer-what-should-i-do}

Iki mbokmenawa masalah gawe indeks Polygonscan. Mangga kontak [Tim Dhukungan](https://support.polygon.technology/support/home) kanggo klarifikasi luwih lengkap.
Panjenengan uga bisa nyoba panjelajah blok iki

[https://polygon-explorer-mainnet.chainstacklabs.com](https://polygon-explorer-mainnet.chainstacklabs.com/) <br />
[https://explorer-mainnet.maticvigil.com](https://explorer-mainnet.maticvigil.com/) <br />
[https://explorer.matic.network](https://explorer.matic.network/) <br />
[https://backup-explorer.matic.network](https://backup-explorer.matic.network/)


## Aku miwiti deposit ing Ethereum nanging isih katon katundha. Apa sing kudu ditindakake? {#i-initiated-a-deposit-on-ethereum-but-it-still-shows-as-pending-what-should-i-do}

Gas sing panjenengan sedhiyakake bisa uga sithik banget. Panjenengan kudu ngenteni sawetara wektu lan gawe transaksi maneh yen ora ditambang. Yen perlu pitulungan tambahan, mangga kontak [tim dhukungan](https://support.polygon.technology/support/home) nganggo alamat dhompet, hash transaksi (yen ana) lan cuplikan layar sing gegayutan.


## Aku ngalami masalah tarikan token karo OpenSea utawa aplikasi liyane sing nggunakake jembatan polygon. {#i-have-a-token-withdrawal-issue-with-opensea-or-any-other-application-which-uses-polygon-bridge}

Yen panjenengan ngalami masalah bab transaksi tarikan panjenengan macet, Polygon nawakake jembatan tarikan nganggo https://polygon-withdraw.matic.network/ kanggo mbantu panjenengan ngatasi masalah yen sampeyan duwe hash sing dibakar. Kanthi alat iki, panjenengan bakal cepet dibantu lan masalah kasebut bakal dirampungi. Pitakonan liyane babagan transaksi panjenengan nganggo OpenSea lan dApps liyane bakal ditangani dening tim aplikasi.


## Ing endi bisa njaluk token MATIC sacara langsung? {#where-can-i-get-matic-tokens-directly}

Dadi token MATIC bisa dituku saka sembarang bursa sentralisasi ([Binance](https://www.binance.com/en), [Coinbase](https://www.coinbase.com/), lsp) utawa ([Uniswap](https://uniswap.org/), [QuickSwap](https://quickswap.exchange/#/swap)) desentralisasi. Panjenengan uga bisa riset lan nyoba sawetara on-ramp kayata [Transak](https://transak.com/), [Ramp](https://ramp.network/).
Tujuane tuku koin MATIC uga kudu nemtokake saka ngendi panjenengan bakal tuku lan jaringane. Dianjurake duwe MATIC ing Main-net Ethereum yen niat panjenengan iku staking utawa delegasi. Yen niat panjenengan transaksi ing mainnet Polygon, panjenengan kudu nahan lan transaksi nganggo MATIC ing mainnet Polygon.


## Aku ora entuk hash transaksi lan setoranku ora kasil? Ana apa? {#i-m-not-getting-a-transaction-hash-and-my-deposits-aren-t-going-through-what-is-happening}

Panjenengan bisa uga duwe transaksi sing katundha sadurunge, batalna utawa dicepetake dhisik. Transaksi ing Ethereum mung bisa kedadeyan mbaka siji.


## Iki nuduhake Polygon ora nuntut beya apa bae kanggo narik nanging kita kudu mbayar sajrone transaksi. {#it-shows-polygon-does-not-charge-any-amount-for-a-withdrawal-but-we-are-to-pay-during-the-transaction}

Transaksi tarikan nganggo jembatan Plasma diperang dadi 3 langkah, sak langkah kedadeyan ing Mainnet Polygon lan rong langkah sing bakal dirampungake ing Mainnet Ethereum. Ing jembatan PoS, transaksi tarikan dumadi liwat rong langkah: Pambakaran Token ing jaringan Polygon lan pangiriman bukti ing jaringan Ethereum. Ing saben kasus, pambakaran token sing kedadeyan ing Mainnet Polygon bakal dadi beya sing paling minimal. Langkah-langkah sing isih ana ing Ethereum Mainnet kudu dibayar ing ETH gumantung saka rega gas saiki sing bisa diverifikasi [ing kene](https://ethgasstation.info/).




## Kepriye carane ngubungi aplikasi utama sing disebarake ing Jaringan Polygon? {#how-do-i-contact-major-applications-deployed-on-the-polygon-network}

Curve h[ttps://discord.gg/JnUFrsDF ](https://discord.gg/JnUFrsDF)
<br />SushiSwap ht[tps://discord.gg/ApbE4Eau
](https://discord.gg/ApbE4Eau)C<br />REAM htt[ps://discord.gg/js8JpmFB
A](https://discord.gg/js8JpmFB)A<br />VE http[s://discord.gg/YYtp7N5d
Fu](https://discord.gg/YYtp7N5d)r<br />uCombo https[://discord.gg/wJJ7PXAd
Qui](https://discord.gg/wJJ7PXAd)c<br />kSwap http:/[/t.me/QuickSwapDEX ](http://t.me/QuickSwapDEX)<br />

Beefy Finance - [https://discord.gg/egkEEAkC](https://discord.gg/egkEEAkC)


## Dhaptar dhompet piranti keras sing didhukung ing Jaringan Polygon. {#list-of-hardware-wallets-supported-on-polygon-network}

Dadi Jaringan Polygon bakal ndhukung kabeh dhompet piranti keras sing kompatibel karo Metamask. Bukak [tautan](https://metamask.zendesk.com/hc/en-us/articles/360020394612-How-to-connect-a-Trezor-or-Ledger-Hardware-Wallet) saka Metamask iki kanggo informasi luwih lengkap.


## Aku mentas diapusi. Kepriye carane ngentukake maneh tokenku? {#i-have-been-scammed-how-will-i-retrieve-my-tokens}

Sayange, ora ana proses pamulihan kanggo koin sing ilang. Kita njaluk sadurunge panjenengan transaksi, panjenengan kudu mriksa lan mriksa maneh sadurunge miwiti lan ngrampungake. Gatekna manawa jaringan Polygon lan akun resmi kita ora melu postingan hadiah utawa nggandakake token lan ora bakal nyedhaki panjenengan nganggo jeneng organisasi. Lirwakna kabeh upaya amarga kamungkinan kuwi kabeh ngapusi. Kabeh komunikasi kita liwat
akun resmi.


## Dadi Ethereum duwe Goerli minangka Jaringan tes. Apa Jaringan Polygon duwe Jaringan Tes. {#so-ethereum-has-goerli-as-its-test-network-does-polygon-network-have-a-test-network}

Dadi kayadene Jaringan Ethereum duwe Goerli minangka jaringan tes, Polygon Mainnet duwe Mumbai. Kabeh transaksi ing jaringan tes iki bakal diindeks ing Mumbai Explorer.


## Kepiye carane bisa nyepetake transaksi ing Metamask. {#how-can-speed-up-my-transaction-on-metamask}

Kanggo nyepetake transaksi liwat Metamask, bukak [tautan](https://metamask.zendesk.com/hc/en-us/articles/360015489251-How-to-Speed-Up-or-Cancel-a-Pending-Transaction)


## Kabeh informasi apa bae sing kudu diwenehake nalika nggawe tiket? {#what-all-information-should-i-provide-when-i-create-a-ticket}

- Alamat dhompet
- Hash transaksi
- Tumindak sing tepat lan asile, deskriptif banget
- Cuplikan layar utawa rekaman layar saka tindakan

## Aku nyoba setor nanging transaksi mandheg ing langkah Setujoni. {#i-was-trying-to-make-a-deposit-but-the-transaction-stopped-at-the-approve-step}

Yen transaksi isih ing langkah **Setujoni**, kuwi durung rampung. Kanggo ngrampungake, panjenengan kudu mbayar beya gas banjur lagi bisa lanjut.

## Ongkos gas kanggo transaksi tarikanku dhuwur banget. {#the-gas-fee-for-my-withdrawal-transaction-is-too-high}

Ongkos gas ing jaringan Polygon tansah cendhek banget, nanging kita ora bisa ngomong kaya mengkono kanggo ongkos mainnet Ethereum..
Yen panjenengan wis miwiti transaksi, penting aja dibatalake. Nanging, panjenengan bisa ngenteni beya gas mudhun utawa nambahake ETH liyane menyang akun.

## Ana sawetara transaksi sing ora sah ing dompetku. Apa dhompetku disusupi? {#there-are-some-unauthorized-transactions-in-my-wallet-is-my-wallet-hacked}

Sayange, jaringan ora bisa mbalekake transaksi sing ora dikarepake.
Tansah penting supaya ngati-ati karo kunci privat lan **aja dibagekake karo wong liya**.
Yen panjenengan isih duwe sawetara dana, transfer langsung sisane menyang dhompet sing anyar.

## Dhompet Polygon nuduhake pesen error 'Waduh, gangguan server'. {#polygon-wallet-shows-an-oops-our-server-stumbled-error-message}

Pesen kasebut bisa uga ateges server kita lagi gangguan. Nanging, yen kabeh katon mlaku kanthi becik, disaranake panjenengan migunakake browser liyane.
Yen panjenengan nyoba narik, panjenengan uga bisa nyoba [Alat Tarikan Polygon](https://polygon-withdraw.matic.network/). Ing kana, panjenengan bisa nyambungake dhompet, nempelake hash transaksi, lan nerusake transaksi.

## Dhompet Polygon nuduhake pesen error 'Pangguna nolak teken transaksi'. {#polygon-wallet-shows-user-denied-transaction-signature-error-message}

Iki biasane kedadeyan amarga pangguna mbatalake utawa ora gelem neken transaksi liwat MetaMask. Yen dijaluk dening dhompet MetaMask, terusna neken transaksi kanthi ngeklik ing Sarujuk lan ora ing Batal.

## Aku ora nampa token sing ditransfer menyang bursa {#i-did-not-receive-the-tokens-i-transferred-to-an-exchange}
Panjenengan transfer koin menyang Binance (Coinbase, Kucoin, utawa bursa liyane) nanging ora nampa ing bursa. Yen ngono, penting kanggo dimangerteni manawa kita saiki ora nyedhiyakake sambungan langsung karo bursa. Umume transaksi bakal ngliwati mainnet Ethereum sadurunge tekan bursa.
Mangga kontak tim dhukungan bursa.

## Dhompet MetaMask-ku ora nyambung karo dhompet Polygon {#my-metamask-wallet-is-not-connecting-with-polygon-wallet}

Ana akeh alesan apa sebabe bisa kedadeyan ngene. Kita saranake panjenengan **nyoba ing liya wektu**, **migunakake browser liyane**utawa, yen tetep ora bisa, **mangga kontak tim dhukungan kita**.

## Kepriye carane aku entuk token MATIC kanggo mbayar ongkos gas? {#how-can-i-get-matic-tokens-to-pay-for-gas-fees}

Kita nyedhiyakake layanan [Ijol Gas](https://wallet.polygon.technology/gas-swap/) sing bisa nulungi panjenengan bab kuwi. Panjenengan milih jumlah MATIC sing panjenengan butuhake kanggo ngrampungake transaksi lan panjenengan bisa ijol token liyane kayata Ether utawa USDT. Perlu dicathet yen iki **transaksi tanpa gas**.

## Ijol Token alon banget. {#token-swap-is-too-slow}

Yen panjenengan nyoba ijol token lan butuh wektu sing suwe banget, panjenengan bisa nyoba transaksi sing kaya kuwi ing browser liyane. Yen tetep ora bisa lan panjenengan nemoni error, kirimna cuplikan layar menyang tim Dhukungan.
