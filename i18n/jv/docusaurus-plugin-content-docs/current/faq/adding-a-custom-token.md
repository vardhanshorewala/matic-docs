---
id: adding-a-custom-token
title: Nambahi Token Kustom
sidebar_label: Adding a Custom Token
description: Mbangun aplikasi blockchain sampeyan sabanjure ing Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

Fitur **Tambahana fitur Token Kustom** saengga panjenengan bisa nambahi token kanthi eksplisit lan migunakake token iku nganggo Rerangken Dhompet Polygon. Panjenengan mung perlu nggoleki token kasebut adhedhasar alamat kontrak, root, utawa anak:

* Dene **Root** yaiku kontrak token ing Ethereum
* Dene **Child** yaiku kontrak ing Polygon

### Tip pro: Kepiye carane nemokake kontrak token? {#pro-tip-how-do-i-find-the-token-contract}

Panjenengan bisa nggoleki token adhedhasar jenenge ing salah sijine [Coingecko](http://coingecko.com) utawa [Coinmarketcap](https://coinmarketcap.com/) ing kono panjenengan bakal bisa pirsa alamat ing rante Ethereum (kanggo token ERC 20) lan rante sabanjure sing didhukung kayata Polygon. Alamat token ing rante liyane bisa uga ora dianyarake nanging panjenengan mesthi bisa migunakake alamat root kanggo tujuan apa wae.

Dadi nalika milih token, panjenengan bakal bisa nggoleki adhedhasar:
* simbol token
* jeneng token
* kontrak

Kaya mengkene cara kerjane:

<img src={useBaseUrl("img/wallet-bridge/001.png")} height="420px"/>

1. Nambahake token apa wae kanthi gampang menyang dhaptar kanthi nambahake alamat kontrak minangka token kustom (kita ndhukung

alamat kontrak ing Polygon utawa Ethereum):

<img src={useBaseUrl("img/wallet-bridge/002.png")} height="600px"/>

2. Sawise informasi token dientukake, panjenengan bakal pirsa layar konfirmasi sing isine kabeh informasi token. Panjenengan banjur bisa nambahake kuwi minangka token kustom sing bakal disimpen sacara lokal ing sistem panjenengan. Disaranake panjenengan verifikasi maneh kontrak token kaping pindho amarga ana akeh token scam utawa kloning:

<img src={useBaseUrl("img/wallet-bridge/003.png")} height="600px"/>

<img src={useBaseUrl("img/wallet-bridge/004.png")} height="600px"/>

3. Token sing panjenengan tambahake saiki ditampilake nalika milih token:

<img src={useBaseUrl("img/wallet-bridge/005.png")} height="600px"/>

4. Panjenengan bisa nambahake token langsung saka tab token ing layar **Atur**:

<img src={useBaseUrl("img/wallet-bridge/006.png")} height="600px"/>
