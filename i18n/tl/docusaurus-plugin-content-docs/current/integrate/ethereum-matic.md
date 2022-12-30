---
id: ethereum-polygon
title: Ethereum ↔ Polygon
description: Buuin ang susunod mong blockchain app sa Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Plasma Secured na Solusyon para ilipat ang mga asset mo mula sa Ethereum papunta sa Polygon at kabaliktaran.
* Gamitin ang [matic.js](https://github.com/maticnetwork/matic.js) para makipag-interaksyon sa mga kontrata ng Plasma sa Polygon.

<!-- * [getting-started](https://maticnetwork.github.io/matic.js/): Set-up the environment for maticjs.
1. [(Ethereum → Matic)](/docs/develop/maticjs/deposit): Deposit assets from root chain to Matic.
2. [(Matic ↔ Matic)](/docs/develop/maticjs/transfer): Transfer assets between accounts on Matic.
3. [(Matic → Ethereum)](/docs/develop/maticjs/withdraw): Withdraw assets from Matic to root chain. -->

## Daloy {#flow}
Heto ang Daloy sa pag-deploy ng mga kontrata mo sa Polygon at Suporta para sa Ethereum↔Polygon.

1. Nagde-deploy ang user ng ERC-20 token sa Ethereum - XToken

2. Ngayon, ibahagi ang address ng kontrata mo sa [Polygon](https://t.me/joinchat/HkoSvlDKW0qKs_kK4Ow0hQ). Heto ang isang halimbawang kahilingan...

> Kumusta sa lahat, Kami ang AwesomeDApp na naka-deploy sa Polygon. Naghahanap ng solusyon para ilipat ang mga asset ko mula sa Ethereum papunta sa Polygon at kabaliktaran. <br/><br/>
> Isang maikling paglalarawan sa aking AwesomeDApp...<br/><br/>
> Token_Address sa Ropsten-> "0x.."<br/>
> Token_Name-> "XToken"<br/>
> Token_Symbol-> "X"<br/>
> Token_Decimals-> "18"<br/><br/>
> Hinihiling sa iyo na I-mapa ang mga token na ito sa Testnet na Bersyon ng Polygon.<br/>

Magde-deploy kami ng Child Contract para sa iyo sa Polygon na maaaring maging flexible batay sa mga kinakailangan at naimapa sa iyong mga token sa Ethereum ↔ Polygon.( Ang pag-deploy sa Polygon ay nangangailangan ng native token nito na Polygon, na maaaring ideposito mula sa Ethereum papunta sa Polygon o maaaring bilhin sa Secondary Market Place.)

3. Maaaring i-mint ng user ang mga Xtoken at Ilipat sa Ethereum. Halimbawa, sabihin nating 100XToken ang na-mint at saka inilipat sa isa pang account.

4. Para i-avail ang mga token na ito sa Polygon Chain, I-call ang function na deposit na magko-call para sa dalawang transaksyon, ang una ay approve at pagkatapos ay depositERC20.

5. Ngayon, 100XTokens ang magagamit sa Polygon Chain sa parehong address.

6. Maaari kang maglipat ng 50 XToken mula sa YourAddress papunta sa NewAddress. Muli, para sa mga transaksyon sa Polygon katulad sa Ethereum, ginagamit ng Polygon ang sarili nitong Native token.

7. Kung gustong mabawi ng mga user ang mga Xtoken na ito sa Ethereum Chain, i-call ang StartWithdraw na magwi-withdraw mula sa childTokenContract at ibu-burn ang mga token na ito sa Polygon Chain. Para maiwasan ang anumang hindi magandang pakikilahok, mangyayari ang isang set ng pag-validate. Kapag tapos na ito, magiging available ang mga token sa Ethereum Chain.

8. I-call ang processExits() para matanggap ang mga token na iyon pabalik sa iyong EOA o address ng account mo.

9. Dapat mong makita ang 50 XToken sa Ethereum mainnet sa Address ng Account mo.
