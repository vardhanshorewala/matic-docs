---
id: wallet-bridge-faq
title: Soalan <>lazim Penghubung Dompet
description: Bangunkan aplikasi blok rantai anda yang seterusnya di Polygon.
keywords:
  - docs
  - matic
  - wallet
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## Di manakah saya boleh menggunakan Dompet Web Matic? {#where-can-i-use-the-matic-web-wallet}
[https://wallet.polygon.technology/](https://wallet.polygon.technology/)

## Bagaimanakah cara saya mencari kontrak token? {#how-do-i-find-the-token-contract}

Sila semak [Menambah artikel Token](../faq/adding-a-custom-token) Tersuai

## Dompet manakah yang disokong pada masa ini? {#which-wallets-are-currently-supported}

- Metamask
- Dompet Coinbase
- Hubung Dompet

Kami akan menambah lebih banyak dompet tidak lama lagi.

## Bagaimanakah Plasma berbeza dengan PoS? {#how-is-plasma-different-from-pos}

Plasma dilengkapi dengan sekuruti tambahan. Semak: [https://docs.polygon.technology/docs/develop/ethereum-polygon/getting-started](https://docs.polygon.technology/docs/develop/ethereum-polygon/getting-started)

## Apakah token yang hanya tersedia di Plasma? {#what-tokens-are-only-available-on-plasma}

Token Polygon

## Bagaimanakah cara saya mendepositkan ke Dompet Polygon dan juga mengeluarkan? {#how-do-i-deposit-to-polygon-wallet-and-also-withdraw}

Blog dan video ini adalah panduan yang sempurna untuk bermula dengan deposit dan mengeluarkan:

Dokumentasi: [https://docs.polygon.technology/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/#depositing-funds-from-ethereum-to-matic](https://docs.polygon.technology/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/#depositing-funds-from-ethereum-to-matic)

Video: [https://www.youtube.com/playlist?list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9](https://www.youtube.com/playlist?list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9)

## Bagaimanakah untuk bertukar kepada mainnet Polygon di Metamask? {#how-to-switch-to-polygon-mainnet-in-metamask}

Dengan mengandaikan bahawa anda telah menambahkan rangkaian dan RPC tersuai untuk mainnet Polygon dalam dompet Metamask anda di sini ialah cara anda boleh menukar:

1. Buka dompet Metamask anda dan klik pada juntai bawah rangkaian untuk mengembangkan seperti ditunjukkan dalam rajah:

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-1.png")} width="30%" height="30%" />

1. Setelah tetingkap berkembang anda boleh memilih Mainnet Polygon untuk bertukar:

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-2.png")} width="357" height="600" />

Anda kini telah bertukar kepada Mainnet Polygon.

Anda boleh merujuk pautan ini jika anda sedang mencari arahan tentang cara menambah rangkaian pada Metamask: [https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-metamask/](https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-metamask/)

## Bagaimanakah untuk memilih mainnet Polygon dalam Walletlink? {#how-to-choose-polygon-mainnet-in-walletlink}

Sila ikut panduan yang diberikan [di sini](https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-wallets#configure-polygon-on-walletlink)

## Saya telah depositkan WETH tetapi saya tidak melihatnya di Metamask. Apakah yang saya buat? {#i-have-deposited-weth-but-i-don-t-see-it-on-metamask-what-do-i-do}

Anda perlu menambah secara manual alamat token tersuai WETH ke Metamask.

Buka Metamask dan skrol ke bawah untuk mengklik pada **Token Import**.

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-3.png")} width="357" height="600" />


Kemudian, tambahkan alamat kontrak, simbol dan ketepatan perpuluhan yang berkaitan. Alamat kontrak (PoS-WETH dalam kes ini) boleh didapati pada pautan ini link: [https://docs.polygon.technology/docs/develop/network-details/mapped-tokens/](https://docs.polygon.technology/docs/develop/network-details/mapped-tokens/). Anda perlu menambah alamat token kanak-kanak untuk melihat baki di Mainnet Polygon. Perpuluhan ketepatan ialah 18 untuk WETH (secara amnya, untuk kebanyakan token perpuluhan ketepatan ialah 18).

Sebaik sahaja anda mengisi semua medan, anda boleh klik pada T**ambah Token Tersuai **dan token anda akan ditambah.

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-4.png")} width="357" height="600" />


## Bolehkah saya hantar token saya dari Polygon ke mana-mana dompet/pertukaran lain? {#can-i-send-my-tokens-from-polygon-to-any-other-wallet-exchange}

Anda tidak boleh hantar terus token daripada Polygon UI ke Pertukaran/dompet. Anda perlu terlebih dahulu menarik diri daripada Polygon ke Ethereum dan kemudian menghantarnya ke alamat pertukaran anda (melainkan pertukaran/dompet anda secara jelas menyokong rangkaian).

## Saya tersilap menghantar dana ke pertukaran/dompet secara langsung. Bolehkah anda bantu? {#i-made-a-mistake-of-sending-funds-to-an-exchange-wallet-directly-can-you-help}

Malangnya, kami tidak dapat bantu dalam kes sedemikian. Sila jangan hantar dana terus ke pertukaran yang menyokong Ethereum sahaja, anda perlu terlebih dahulu menarik diri daripada Polygon ke Ethereum dan kemudian menghantarnya ke alamat pertukaran anda.

## Transaksi saya belum selesai terlalu lama, apakah yang boleh saya lakukan? {#my-transaction-is-pending-for-too-long-what-can-i-do}

Transaksi pada blok rantai mungkin akan digugurkan kerana harga gas yang rendah ditetapkan semasa menyerahkan transaksi. Mereka juga mungkin akan digugurkan apabila terdapat lonjakan mendadak dalam harga gas disebabkan oleh kesesakan pada Ethereum. Kemungkinan lain ialah anda mungkin telah membatalkan transaksi daripada dompet anda atau menggantikan transaksi tersebut. Dalam semua kes ini, web dompet akan menunjukkan kepada anda mesej dalam proses transaksi dan ini akan menyebabkan anda menunggu lebih lama.

Jika transaksi anda tersekat selama lebih daripada sejam, butang "Cuba Lagi" akan ditunjukkan. Ini bagus, ini bermakna anda boleh menggesa rangkaian untuk mencuba semula transaksi untuk anda. Apa yang anda boleh lakukan seterusnya ialah klik pada butang "Cuba Lagi" untuk mencuba semula transaksi yang sama. Jika transaksi deposit anda tersekat, proses deposit anda akan dimulakan semula dan jika transaksi pengeluaran anda tersekat, anda akan dapat meneruskan pengeluaran anda dari tempat anda berjaya menyelesaikan langkah terakhir.

Sekiranya anda menghadapi masalah untuk meneruskan butang "Cuba Lagi" dan anda menggunakan dompet Metamask, anda mungkin perlu semak sama ada terdapat banyak transaksi beratur yang menyumbat bahagian aktiviti metamask anda. Dalam kes ini, mungkin berguna untuk memasang semula dompet metamask dan kemudian meneruskan transaksi anda. Sebagai alternatif, anda boleh cuba memulakan transaksi daripada penyemak imbas yang berasingan.

Menonton video di bawah boleh memberikan lebih jelas tentang cara menggunakan ciri "Cuba Lagi"

[https://youtu.be/0b4yjR_naEQ](https://youtu.be/0b4yjR_naEQ)

## Apakah senarai Pertukaran yang Disokong pada Polygon? {#what-are-the-list-of-supported-exchanges-on-polygon}

Di bawah ialah senarai pertukaran berpusat yang menyokong Polygon pada masa ini dan juga token yang disokong oleh pertukaran ini.

AscendEX - USDC, EASY, MATIC

MXC - MATIC, QUICK, PlotX, Dfyn

Okcoin - ETH, USDT, LINK, MKR, USDC, DAI, USDK, COMP, YFI, SNX, YFII, dan UNI. (Token hanya boleh dialihkan dari Okcoin ke rantaian Polygon. Memindahkan token daripada Polygon ke Okcoin tidak disokong pada masa ini)

Okex - BAL, BAT, CEL, COMP, CRV, DAI, ETH, GHST, GUSD, LINK, MKR, PAX, SNX, SUSHI, TUSD, UNI, USDC-ERC20, USDT-ERC20, USDK, wBTC, YFI, YFII, ZRX (Token hanya boleh dialihkan dari Okex ke rantaian Polygon. Memindahkan token dari Polygon ke Okex tidak disokong pada masa ini)

Bitforex - MATIC

Menghantar Token ke mana-mana pertukaran lain yang tidak dinyatakan secara jelas dalam senarai di atas boleh menyebabkan kehilangan dana. Jika anda ingin mengeluarkan dana ke mana-mana pertukaran yang tidak menyokong Polygon, anda perlu terlebih dahulu mengeluarkan token ke Ethereum dan kemudian menghantarnya ke pertukaran menggunakan dompet Ethereum anda. Video ini menunjukkan cara untuk mengeluarkan dana daripada Polygon ke Ethereum - [ https://www.youtube.com/watch?v=DgpHY95qrbQ&list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9&index=5](https://www.youtube.com/watch?v=DgpHY95qrbQ&list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9&index=5)

Sebagai alternatif, anda boleh mengikuti [pand](https://docs.matic.today/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/)uan ini di sini.

## Saya tidak boleh log masuk, apakah yang perlu saya lakukan? {#i-am-not-able-to-login-what-do-i-do}

[https://docs.polygon.technology/docs/validate/delegator-faq/#my-metamask-is-stuck-at-confirming-after-login-what-do-i-do-or-nothing-happens-when-i-try-to-login](https://docs.polygon.technology/docs/validate/delegator-faq/#my-metamask-is-stuck-at-confirming-after-login-what-do-i-do-or-nothing-happens-when-i-try-to-login)

## Adakah Polygon menyokong dompet perkakasan? {#does-polygon-support-hardware-wallets}
Ya, dompet perkakasan disokong.

## Apakah yang boleh saya lakukan dengan dompet Polygon saya? {#what-can-i-do-with-my-polygon-wallet}

- Hantar dana ke mana-mana akaun di Polygon.
- Depositkan dana daripada Ethereum ke Polygon (menggunakan jambatan).
- Keluarkan dana kembali ke Ethereum dari Polygon (juga menggunakan jambatan).

## Token saya tidak kelihatan dalam senarai. Siapakah yang patut saya hubungi? {#my-token-is-not-visible-in-the-list-who-should-i-contact}

Hubungi pasukan Polygon di Discord atau Telegram dan senaraikan token anda. Sebelum itu, pastikan token anda dipetakan. Jika ia tidak dipetakan, sila bangkitkan permintaan di [https://mapper.polygon.technology/](https://mapper.polygon.technology/)

## Apakah beberapa amalan terbaik untuk diikuti? {#what-are-some-best-practices-to-follow}

- Apabila anda ingin menghantar dana dari Polygon ke Ethereum, gunakan fungsi pengeluaran. Jangan gunakan fungsi penghantaran. Ini akan menyebabkan kehilangan dana.
- Jangan deposit ke mainnet Polygon jika anda ingin mengambil bahagian dalam pegangan sahaja.
- Jangan ubah had gas dari Metamask.

## Apakah yang perlu saya lakukan jika deposit disahkan tetapi baki tidak dikemas kini? {#what-do-i-do-if-the-deposit-is-confirmed-but-the-balance-is-not-getting-updated}

Ia mengambil masa 22-30 minit untuk transaksi deposit untuk selesai. Sila tunggu beberapa ketika dan klik pada "segarkan semula baki".

## Apakah yang perlu saya lakukan jika titik semak tidak berlaku? {#what-should-i-do-if-the-checkpoint-is-not-happening}

Titik semak kadangkala mengambil masa lebih daripada 45 minit hingga 1 jam berdasarkan kesesakan rangkaian di Ethereum, kami cadangkan untuk menunggu seketika sebelum menaikkan tiket.

## Adakah boleh membatalkan transaksi pengeluaran? {#is-it-possible-to-cancel-a-withdraw-transaction}

Tidak, anda perlu melengkapkan langkah seterusnya. Jika harga gas semasa terlalu tinggi, sila tunggu dan cuba kemudian apabila harga turun.

## Mengapakah token MATIC tidak disokong pada PoS? {#why-is-the-matic-token-is-not-supported-on-pos}

MATIC ialah token asli Polygon dan ia mempunyai alamat kontrak - 0x0000000000000000000000000000000000001010 pada rantaian Polygon. Ia juga digunakan untuk membayar petrol. Pemetaan token MATIC pada penghubung PoS akan membawa kepada MATIC yang mempunyai alamat kontrak tambahan pada rantaian Polygon. Ini akan berlanggar dengan alamat kontrak sedia ada kerana alamat token baharu ini tidak boleh digunakan untuk membayar gas dan perlu kekal sebagai token ERC20 biasa pada rantaian Polygon. Oleh itu, untuk mengelakkan kekeliruan ini, ia telah diputuskan untuk mengekalkan MATIC hanya pada Plasma.

## Bagaimanakah saya memetakan token? {#how-do-i-map-tokens}

Sila bangkitkan permintaan pemetaan di [https://mapper.polygon.technology/](https://mapper.polygon.technology/)

## Apakah yang perlu saya lakukan sekiranya transaksi mengambil masa terlalu lama atau jika harga gas terlalu tinggi? {#what-do-i-do-if-the-transaction-is-taking-too-long-or-if-the-gas-price-is-too-high}

Masa transaksi dan harga gas berbeza-beza mengikut kesesakan rangkaian. Jika harga gas yang tinggi dibayar, maka transaksi akan disahkan lebih cepat.

## Bolehkah saya menukar had gas atau harga gas? {#can-i-change-the-gas-limit-or-the-gas-price}

Had gas dianggarkan dan ditetapkan oleh aplikasi mengikut keperluan tertentu bagi fungsi yang dipanggil dalam kontrak. Ini tidak boleh diedit. Hanya harga gas boleh diubah untuk menaikkan atau menurunkan yuran transaksi.

## Apakah yang perlu saya lakukan jika transaksi telah dibatalkan tetapi dompet web menunjukkan transaksi telah selesai? {#what-should-i-do-if-the-transaction-was-cancelled-but-the-web-wallet-shows-transaction-is-completed}

Sila hubungi pasukan sokongan kami.

## Di manakah saya boleh menaikkan tiket sokongan? {#where-do-i-raise-a-support-ticket}
https://support.polygon.technology/support/home

## Harga gas adalah lebih daripada jumlah yang saya ingin keluarkan. {#the-gas-price-is-more-than-the-amount-i-seek-to-withdraw}

Transaksi pengeluaran dengan penghubung Plasma dibahagikan kepada 3 langkah, satu yang berlaku pada Mainnet Polygon dan dua langkah yang perlu diselesaikan pada Ethereum Mainnet. Di penghubung PoS, transaksi pengeluaran berlaku melalui dua langkah: Pembakaran token pada rangkaian Polygon dan penyerahan bukti pada rangkaian Ethereum. Pada mainnet Polygon, caj adalah sangat minimum dan bahagian besar kos transaksi yang anda lihat ialah harga gas pada Rangkaian Ethereum yang ditadbir oleh pelombong Ethereum. Seperti yang boleh dijangkakan, caj ini di luar kawalan kami dan kami tidak mempunyai banyak pengaruh terhadap titik harga. Satu perkara terakhir, jika token anda hangus, anda mungkin perlu meneruskan pengeluaran anda tanpa mengira kerana tiada apa yang boleh kami lakukan untuk membalikkan proses tersebut.


## Bolehkah saya membatalkan transaksi pengeluaran saya? {#can-i-cancel-my-withdrawal-transaction}

Malangnya, Polygon tidak boleh membatalkan pengeluaran setelah proses dimulakan dan token berjaya dibakar. Cincang hangus dibuat dan fasa transaksi seterusnya akan datang dengan serta-merta. Jika transaksi yang hangus masih belum selesai, anda mungkin boleh memudahkan pembatalan melalui panduan berikut

[Metamask](https://metamask.zendesk.com/hc/en-us/articles/360015489251-How-to-Speed-Up-or-Cancel-a-Pending-Transaction)<br /> [Walletlink](https://www.techdreams.org/crypto-currency/how-to-cancel-a-pending-ethereum-transaction-on-coinbase-wallet/10159-20210412)


## Transaksi saya tersekat. {#my-transaction-is-stuck}

Kami telah senaraikan beberapa ralat biasa yang mungkin dihadapi oleh pengguna. Anda boleh mencari penyelesaian di bawah imej ralat tersebut. Jika anda ditunjukkan ralat yang berbeza, sila [angkat tiket sokongan ](https://support.polygon.technology/support/home)untuk pasukan kami selesaikan masalah.

  - ### Ralat Biasa {#common-errors}
a. Pengeluaran tersekat pada fasa yang Dimulakan.

    <img src={useBaseUrl("img/wallet-bridge/plasma-progress-stuck.png")} width="357" height="800"/>Ini biasanya berlaku apabila transaksi digantikan dan aplikasi web dompet tidak dapat mengesan cincang transaksi yang diganti. Sila ikut arahan pada [https://withdraw.polygon.technology/](https://withdraw.polygon.technology/) dan lengkapkan pengeluaran anda.
b. Ralat RPC

    <img src={useBaseUrl("img/wallet-bridge/checkpoint-rpc-error.png")} width="357" height="600"/>Ralat RPC semasa yang anda hadapi mungkin disebabkan oleh beban RPC yang berlebihan. Sila cuba tukar RPC anda dan teruskan transaksi. Anda boleh mengikuti pautan ini [di sini](https://docs.polygon.technology/docs/develop/network-details/network#matic-mainnet) untuk mendapatkan maklumat lanjut.
c.

  <img src={useBaseUrl("img/wallet-bridge/checkpoint-stumbled-error.png")} width="357" height="600"/>

Ini biasanya ralat luar dan hidup yang dapat diselesaikan secara automatik. Jika anda masih menerima ralat yang sama semasa memulakan semula langkah, naikk[an tiket sokongan deng](https://support.polygon.technology/)an semua maklumat yang berkaitan untuk menyelesaikan masalah ini dengan lebih lanjut.

## Saya membuat kesilapan dengan menghantar dana ke pertukaran/dompet terus daripada Dompet Polygon. Bolehkah anda bantu? {#i-made-the-mistake-of-sending-funds-to-an-exchange-wallet-directly-from-polygon-wallet-can-you-help}

Malangnya, kami kesal untuk memaklumkan kepada anda bahawa kami mungkin tidak dapat membantu jika anda telah menghantar token daripada rangkaian Polygon ke pertukaran/dompet yang tidak disokong.

Inilah yang perlu dilakukan oleh pertukaran dalam kes ini (walaupun tidak pasti berapa banyak fleksibiliti eksekutif sokongan perlu melaksanakan ini). Dengan mengandaikan eksekutif sokongan pertukaran mempunyai akses kepada kunci peribadi akaun, mereka boleh memindahkan dana daripada akaun mereka di Polygon ke alamat (pengguna) anda di Polygon.

Adalah penting untuk ambil perhatian bahawa anda tidak sepatutnya menghantar dana terus ke pertukaran yang hanya menyokong Ethereum. Prosedur yang betul ialah anda perlu menarik diri terlebih dahulu daripada Polygon ke Ethereum dan kemudian menghantarnya ke alamat pertukaran anda.

## Saya telah menunjukkan ralat baki yang tidak mencukupi. {#i-m-shown-an-insufficient-balance-error}

Pengeluaran dan deposit di rangkaian Polygon adalah murah. Apa yang perlu difahami ialah ralat baki yang tidak mencukupi boleh dibersihkan dengan mendapatkan beberapa baki ETH pada mainnet ethereum. Itu secara amnya menyelesaikan masalah baki tidak mencukupi.

Jika ini adalah transaksi pada mainnet Polygon, kami memerlukan anda yang mempunyai jumlah token matik yang mencukupi.

## Bagaimanakah saya boleh menghubungkan aset merentasi rantaian? {#how-do-i-bridge-assets-across-chains}

[https://wallet.polygon.technology/bridge/](https://wallet.polygon.technology/bridge/) (ETH <-> Polygon)<br/> [https://xpollinate.io/](https://xpollinate.io/) (BSC <-> Polygon <-> xDai)<br/> [https://exchange.chainswap.com/](https://exchange.chainswap.com/) (ETH <-> Polygon/BSC) <br/>[https://anyswap.exchange/bridge](https://anyswap.exchange/bridge) (ETH <-> Polygon <-> BSC/xDai) <br/>[https://app.0.exchange/#/home](https://app.0.exchange/#/home)(ETH <-> Polygon <-> Avalanche <-> BSC)

Untuk menambah, kami tidak mengendors sebarang perkhidmatan luaran, sila pastikan anda sentiasa melakukan penyelidikan anda sendiri

## Saya membuat pemindahan ke alamat yang salah. Bagaimanakah cara saya mendapatkan semula dana? {#i-made-a-transfer-to-the-wrong-address-how-do-i-retrieve-the-funds}

Malangnya, tiada apa yang boleh dibuat. Hanya pemilik kunci persendirian ke alamat tertentu itu boleh memindahkan aset tersebut.


## Transaksi saya tidak dapat dilihat pada penjelajah. Apakah yang patut saya buat? {#my-transactions-are-not-visible-on-the-explorer-what-should-i-do}

Ini mungkin isu pengindeksan dengan Polygonscan. Sila hubungi [Pasukan Sokongan ](https://support.polygon.technology/support/home)untuk penjelasan lebih lanjut. Anda juga boleh mencuba penjelajah blok ini

[https://polygon-explorer-mainnet.chainstacklabs.com](https://polygon-explorer-mainnet.chainstacklabs.com/) <br />
[https://explorer-mainnet.maticvigil.com](https://explorer-mainnet.maticvigil.com/) <br />
[https://explorer.matic.network](https://explorer.matic.network/) <br />
[https://backup-explorer.matic.network](https://backup-explorer.matic.network/)


## Saya telah memulakan deposit pada Ethereum tetapi ia masih menunjukkan belum selesai. Apakah yang patut saya buat? {#i-initiated-a-deposit-on-ethereum-but-it-still-shows-as-pending-what-should-i-do}

Gas anda yang dibekalkan mungkin terlalu rendah. Anda harus menunggu sebentar dan buat semula transaksi jika ia tidak dilombong. Sekiranya terdapat bantuan tambahan, sila hubungi [pasukan sokongan](https://support.polygon.technology/support/home) dengan alamat dompet anda, cincang transaksi (jika ada) dan tangkapan skrin berkaitan.


## Saya mempunyai isu pengeluaran token dengan OpenSea atau mana-mana aplikasi lain yang menggunakan penghubung polygon. {#i-have-a-token-withdrawal-issue-with-opensea-or-any-other-application-which-uses-polygon-bridge}

Jika anda menghadapi masalah dengan transaksi pengeluaran anda yang tersekat, Polygon menawarkan penghubung penarikan dengan https://polygon-withdraw.matic.network/ untuk membantu anda melepaskan diri jika anda mempunyai cincangan hangus anda. Dengan alat ini, anda sudah bersedia dengan cepat dan isu tersebut akan diselesaikan. Soalan lain mengenai transaksi anda dengan OpenSea dan dApps lain perlu dikendalikan oleh pasukan aplikasi.


## Di manakah saya boleh dapatkan token MATIC secara terus? {#where-can-i-get-matic-tokens-directly}

Jadi token MATIC boleh dibeli daripada mana-mana [pertukaran](https://www.binance.com/en) [terpusat ](https://www.coinbase.com/)(Binance, Coinbase, et.al) [atau ](https://uniswap.org/)[Tidak Berpusat ](https://quickswap.exchange/#/swap)(Uniswap, QuickSwap). Anda juga boleh menyelidik dan mencuba beberapa tanjakan seperti [Transak](https://transak.com/), [Ramp.](https://ramp.network/) Tujuan pembelian syiling MATIC anda juga harus menentukan dari mana anda akan membeli syiling tersebut dan rangkaiannya. Adalah dinasihatkan untuk mempunyai MATIC di Ethereum Main-net jika niat anda sama ada pegangan atau perwakilan. jika niat anda ialah transaksi pada mainnet Polygon, anda harus memegang dan bertransaksi dengan MATIC pada mainnet Polygon.


## Saya tidak mendapat cincang transaksi dan deposit saya tidak berjaya? Apakah yang sedang berlaku? {#i-m-not-getting-a-transaction-hash-and-my-deposits-aren-t-going-through-what-is-happening}

Anda mungkin mempunyai transaksi yang belum selesai, sila batalkan atau percepatkannya terlebih dahulu. Transaksi dalam Ethereum hanya boleh berlaku satu demi satu.


## Ia menunjukkan Polygon tidak mengenakan sebarang amaun untuk pengeluaran tetapi kami perlu membayar semasa transaksi. {#it-shows-polygon-does-not-charge-any-amount-for-a-withdrawal-but-we-are-to-pay-during-the-transaction}

Transaksi pengeluaran dengan penghubung Plasma dibahagikan kepada 3 langkah, satu yang berlaku pada Mainnet Polygon dan dua langkah yang perlu diselesaikan pada Ethereum Mainnet. Di penghubung PoS, transaksi pengeluaran berlaku melalui dua langkah: Pembakaran token pada rangkaian Polygon dan penyerahan bukti pada rangkaian Ethereum. Dalam setiap kes, pembakaran token yang berlaku pada Mainnet Polygon akan menjadi kos yang sangat minimum. Langkah selebihnya yang berlaku pada Mainnet Ethereum perlu dibayar dalam ETH bergantung pada harga gas semasa yang boleh disahkan [di sini](https://ethgasstation.info/).


## Bagaimanakah saya boleh menghubungi aplikasi utama yang digunakan pada Rangkaian Polygon? {#how-do-i-contact-major-applications-deployed-on-the-polygon-network}

Curve  [https://discord.gg/JnUFrsDF](https://discord.gg/JnUFrsDF) <br />
SushiSwap  [https://discord.gg/ApbE4Eau](https://discord.gg/ApbE4Eau) <br />
CREAM  [https://discord.gg/js8JpmFB](https://discord.gg/js8JpmFB) <br />
AAVE  [https://discord.gg/YYtp7N5d](https://discord.gg/YYtp7N5d) <br />
FuruCombo  [https://discord.gg/wJJ7PXAd](https://discord.gg/wJJ7PXAd) <br />
QuickSwap  [http://t.me/QuickSwapDEX](http://t.me/QuickSwapDEX) <br />

Beefy Finance - [https://discord.gg/egkEEAkC](https://discord.gg/egkEEAkC)


## Senarai dompet perkakasan yang disokong pada Rangkaian Polygon. {#list-of-hardware-wallets-supported-on-polygon-network}

Jadi Rangkaian Polygon akan menyokong semua dompet perkakasan yang serasi dengan Metamask. Sila ikut [pautan ](https://metamask.zendesk.com/hc/en-us/articles/360020394612-How-to-connect-a-Trezor-or-Ledger-Hardware-Wallet)ini dari Metamask untuk mendapatkan maklumat lanjut.


## Saya telah ditipu. Bagaimanakah saya boleh mendapatkan semula token saya? {#i-have-been-scammed-how-will-i-retrieve-my-tokens}

Malangnya, tiada proses pemulihan untuk syiling hilang. Kami meminta sebelum anda membuat transaksi, anda terus menyemak dan menyemak semula sebelum memulakan dan melengkapkan. Harap maklum bahawa rangkaian Polygon dan pemegang rasmi kami tidak terlibat dalam sebarang siaran pemberian atau penggandaan token dan kami tidak akan sekali-kali mendekati anda bagi pihak organisasi. Sila abaikan semua percubaan kerana ia kemungkinan besar penipuan. Semua komunikasi kami adalah rasmi pemegang.


## Oleh itu, Ethereum mempunyai Goerli sebagai Rangkaian ujiannya. Adakah Rangkaian Polygon mempunyai Rangkaian Ujian. {#so-ethereum-has-goerli-as-its-test-network-does-polygon-network-have-a-test-network}

Oleh itu, cara Rangkaian Ethereum mempunyai Goerli sebagai rangkaian ujiannya, Mainnet Polygon mempunyai Mumbai. Semua transaksi pada rangkaian ujian ini akan diindeks pada Peneroka Mumbai.


## Cara yang boleh mempercepatkan transaksi saya di Metamask. {#how-can-speed-up-my-transaction-on-metamask}

Untuk mempercepatkan transaksi melalui Metamask, sila pergi ke [pautan](https://metamask.zendesk.com/hc/en-us/articles/360015489251-How-to-Speed-Up-or-Cancel-a-Pending-Transaction) ini


## Apakah semua maklumat yang perlu saya berikan semasa saya mencipta tiket? {#what-all-information-should-i-provide-when-i-create-a-ticket}

- Alamat dompet
- Cincang transaction
- Tindakan tepat dimaksudkan dan hasilnya, sangat deskriptif
- Tangkapan skrin atau rakaman skrin tindakan tersebut

## Saya cuba membuat deposit tetapi transaksi berhenti pada langkah Kelulusan. {#i-was-trying-to-make-a-deposit-but-the-transaction-stopped-at-the-approve-step}

Jika transaksi masih berada pada langkah **Kelulusan**, ia masih belum selesai. Untuk memenuhinya, anda perlu membayar yuran gas dan kemudian ia hendaklah lulus.

## Yuran gas untuk transaksi pengeluaran saya terlalu tinggi. {#the-gas-fee-for-my-withdrawal-transaction-is-too-high}

Yuran gas pada rangkaian Polygon sentiasa sangat rendah, tetapi kami tidak boleh mengatakan perkara yang sama untuk yuran mainnet Ethereum. Jika anda telah memulakan transaksi, adalah penting untuk tidak membatalkannya. Sebaliknya, anda boleh menunggu sehingga bayaran gas diturunkan atau menambah lebih banyak ETH pada akaun anda.

## Terdapat beberapa transaksi yang tidak dibenarkan dalam dompet saya. Adakah dompet saya digodam? {#there-are-some-unauthorized-transactions-in-my-wallet-is-my-wallet-hacked}

Malangnya, rangkaian tidak boleh mengembalikan transaksi yang tidak diingini. Ianya sentiasa penting untuk berhati-hati dengan kunci peribadi anda dan **jangan sekali-kali berkongsi dengan sesiapa pun**. Jika anda masih mempunyai baki dana, pindahkannya dengan segera ke dompet baharu.

## Dompet polygon menunjukkan mesej ralat 'Oops Pelayan kami Tersingkir'. {#polygon-wallet-shows-an-oops-our-server-stumbled-error-message}

Mesej itu mungkin bermakna pelayan kami tidak berfungsi. Walau bagaimanapun, jika semuanya berfungsi dengan baik, kami mencadangkan anda menggunakan penyemak imbas lain. Jika anda cuba membuat pengeluaran, anda juga boleh mencuba a[lat Pengeluaran Polygon](https://polygon-withdraw.matic.network/). Di sana, anda boleh hubungkan dompet anda, menampal cincang transaksi anda dan meneruskan transaksi.

## Dompet polygon menunjukkan mesej ralat 'Tandatangan transaksi ditolak pengguna'. {#polygon-wallet-shows-user-denied-transaction-signature-error-message}

Ini biasanya berlaku kerana pengguna membatalkan atau enggan menandatangani transaksi melalui MetaMask. Apabila digesa oleh dompet MetaMask, teruskan dengan menandatangani transaksi dengan klik pada Lulus dan bukan pada Batal.

## Saya tidak menerima token yang saya pindahkan ke pertukaran {#i-did-not-receive-the-tokens-i-transferred-to-an-exchange}
Anda memindahkan syiling ke Binance (Coinbase, Kucoin atau mana-mana pertukaran lain) tetapi tidak menerimanya di bahagian pertukaran. Jika itu adalah kes anda, ianya penting untuk mengetahui bahawa pada masa ini kami tidak menyediakan sambungan terus dengan pertukaran. Kebanyakan transaksi sebenarnya akan melalui Ethereum mainnet sebelum mencapai pertukaran. Sila hubungi pasukan sokongan pertukaran.

## Dompet MetaMask saya tidak bersambung dengan dompet Polygon {#my-metamask-wallet-is-not-connecting-with-polygon-wallet}

Terdapat banyak sebab mengapa perkara ini boleh berlaku. Kami mencadangkan agar anda **mencuba lain kali**, **gunakan penyemak imbas lain** atau, jika mana-mana daripada ini tidak membantu,** hubungi pasukan sokongan kami**.

## Bagaimanakah saya boleh mendapatkan token MATIC untuk membayar yuran gas? {#how-can-i-get-matic-tokens-to-pay-for-gas-fees}

Kami menyedia[kan perk](https://wallet.polygon.technology/gas-swap/)hidmatan Pertukaran Gas yang akan membantu anda dengan itu. Anda memilih jumlah MATIC yang anda perlukan untuk melengkapkan transaksi anda dan anda boleh menukarnya dengan token lain seperti Ether atau USDT. Perlu diingat bahawa ini adalah **transaksi tanpa gas**.

## Swap Token terlalu perlahan. {#token-swap-is-too-slow}

Jika anda cuba menukar token dan ia mengambil masa terlalu lama, anda boleh mencuba transaksi yang sama pada penyemak imbas yang berbeza. Jika perkara itu tidak berjaya dan anda menghadapi ralat, sila hantar tangkapan skrin kepada pasukan Sokongan kami.
