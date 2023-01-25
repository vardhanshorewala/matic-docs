---
id: move-stake
title: Paglipat ng Stake
description: Buuin ang susunod mong blockchain app sa Polygon.
keywords:
  - docs
  - polygon
  - matic
  - stake
  - move stake
slug: move-stake
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## Paglilipat ng Stake mula sa mga Foundation node papunta sa External Node {#moving-stake-from-foundation-nodes-to-external-nodes}


<video loop autoplay width="100%" height="100%" controls="true" >
  <source type="video/mp4" src="/img/staking/MoveStakeDemo.mp4"></source>
  <source type="video/quicktime" src="/img/staking/MoveStakeDemo.mov"></source>
  <p>Hindi sinusuportahan ng browser mo ang video element.</p>
</video>

Binibigyan na ngayon ng opsyon ang mga delegator na ilipat ang kanilang stake mula sa mga Foundation node papunta sa anumang External node na kanilang pinili sa pamamagitan ng paggamit ng Move Stake functionality sa Staking UI

Isang transaksyon lang ang paglilipat ng Stake mula sa foundation node papunta sa external node. Kaya walang delay o unbonding period habang nasa event na ito.

Pakitandaan na pinapayagan lang ang Paglilipat ng Stake mula sa Foundation node papunta sa External node. Kung gusto mong ilipat ang stake mo mula sa isang External node papunta sa isa pang External node, kailangan mo munang I-unbond at pagkatapos ay I-delegate ito sa bagong external na node.

Isa ring pansamantalang function ang Paglipat ng Stake na binuo ng Polygon team para matiyak ang maayos na paglilipat ng mga pondo mula sa mga Foundation node papunta sa External. At mananatili lang itong active hanggang sa i-off ang mga foundation node.

### Paano Maglipat ng Stake {#how-to-move-stake}

Para Ilipat ang stake, kailangan mo munang mag-login sa Staking UI: https://wallet.polygon.technology/staking gamit ang Delegator Address mo.

**Address ng Delegator** = Ang address na nagamit mo na para sa Pag-stake sa mga Foundation Node.

Kapag naka-log in na, makikita mo ang listahan ng mga Validator.

<img src={useBaseUrl("img/staking/validator-list.png")} />

Ngayon, pumunta ka sa mo Delegator Profile sa pamamagitan ng pag-click sa button na "Ipakita ang mga Detalye ng Delegator" o sa opsyon na "**Mga Detalye ng Delegator Ko**"  sa bandang kaliwang bahagi

<img src={useBaseUrl("img/staking/show-delegator-details.png")} />

Makikita mo rito ang bagong button na tinatawag na "**Paglipat ng Stake**"

<img src={useBaseUrl("img/staking/move-stake-button.png")} />

Sa pag-click sa button na iyon, ina-navigate ka sa isang page na may listahan ng mga validator kung kanino ka puwedeng Mag-deligate. Puwede kang mag-delegate sa kahit sinong Validator na nasa listahang ito.

<img src={useBaseUrl("img/staking/move-stake-validator.png")} />

Ngayon, pagkatapos piliin ang validator kung kanino mo gustong mag-validate, i-click ang button na "**I-delegate Dito**".

Sa pag-click sa button na iyon, magbubukas ang isang pop up.

<img src={useBaseUrl("img/staking/stake-funds.png")} />

Makikita mo rito ang field ng Halaga na awtomatikong mapupunan ng buong halaga para sa Pag-delegate. Puwede ka ring gumamit ng bahagyang halaga para i-deligate sa isang validator.

**Halimbawa**, kung nag-delegate ka ng 100 Matic token sa Foundation Node 1 at gusto mo na ngayong ilipat ang stake mo mula sa foundation node papunta sa isang external node, puwede kang mag-delegate ng bahagyang halaga sa external node na pinili mo, gaya ng 50 Matic token. Mananatili sa Foundation node 1 ang matitira sa 50 Matic token. Pagkatapos ay puwede mong piliing i-delegate ang natitira sa 50 token sa isa pang external node o sa parehong external node.

Kapag nailagay mo na ang halaga, puwede mo nang i-click ang button na Stake Funds. Hihingi ito ng kumpirmasyon sa Metamask mo para lagdaan ang address.

Kapag nalagdaan mo na ang transaksyon, matagumpay na maililipat ang stake mo mula sa Foundation node papunta sa External node. Pero kakailanganin mong maghintay ng 12 pagkumpirma ng block para lumabas ito sa Staking UI. Kung hindi lumabas ang mga inilapat mong pondo pagkatapos ng 12 pagkumpirma ng block, subukang i-refresh ang page nang isang beses para makita ang mga na-update na stake.

Kung mayroon kang anumang tanong o isyu, magsumite ng ticket [dito](https://support.polygon.technology/support/home).
