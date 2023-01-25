---
id: liquid-delegation
title: Liquid na Pag-delegate
sidebar_label: Liquid Delegation
description: "Paano ginagamit ng Polygon ang liquid na pag-delegate para mapanatili ang network."
keywords:
  - docs
  - polygon
  - matic
  - delegation
  - liquid delegation
slug: liquid-delegation
image: https://matic.network/banners/matic-network-16x9.png
---

Sa isang tradisyonal na mekanismo ng Proof of Stake, sinusubaybayan ng blockchain ang isang set ng mga validator. Puwedeng sumali ang sinuman sa hanay o karapatang ito para mag-validate ng mga transaksyon sa pamamagitan ng pagpapadala ng isang espesyal na uri ng transaksyon kung saan ini-stake ang kanilang mga coin (sa kaso ng Ethereum ay ether) at nila-lock up sa isang deposit. Pagkatapos ay isinasagawa ang proseso ng paggawa at pagsang-ayon sa mga bagong block sa pamamagitan ng consensus algorithm ng lahat ng kasalukuyang validator.

Nila-lock up nila ang bahagi ng kanilang stake para sa isang tiyak na tagal ng panahon (tulad ng isang panseguridad na deposit) at bilang kapalit, nagkakaroon sila ng pagkakataon na proporsyonal sa stake na iyon para piliin ang susunod na block

Ang mga insentibo para sa mga kalahok ay mga gantimpala sa Pag-stake—at ang posibilidad ng pag-slash—na humihikayat sa mga may-ari ng token na i-secure ang PoS blockchain. Dahil sa pag-sake, nagkakaroon ng "personal na interes na magtagumpay ang gawain" na kinakailangan para magkaroon ng magandang gawi gaya ng pagpapatakbo ng mga node sa network at hindi hinihikayat ang hindi magagandang gawi gaya ng hindi pananatiling naka-online o dalawang beses na paglagda.

### Pag-delegate at kahalagahan nito {#delegation-and-need-for-it}

Puwedeng maging magastos ang pag-stake at lalong nagpapataas sa hadlang para makapasok, kung saan lalong pinapayaman ang mayayaman. Gusto naming makilahok ang lahat sa seguridad ng network at mapataas ang halaga ng token. Ang tanging alternatibo ay makilahok sa pool sa pag-stake tulad ng pool sa pag-mine kung saan kailangan mong pagkatiwalaan ang mga validator. Kaya naman sa tingin namin, ang pagpapanatili ng pag-delegate sa protocol ang pinakamahusay na paraan para sa mga bagong delegator, dahil protektado at bukas ang kapital, mga gantimpala, at pag-slash sa pamamagitan ng in-protocol na mekanismo.

Puwedeng lumahok ang mga delegator sa pag-validate nang hindi nagho-host ng full node. Pero sa pag-stake sa tulong ng mga validator, puwede silang makakuha ng gantimpala at palakasin ang network sa pamamagitan ng pagbabayad ng kaunting komisyon sa validator (depende sa Validator) na kanilang pipiliin.

### Limitasyon ng Tradisyonal na Delegator at Validator pov {#limitation-of-traditional-delegator-and-validator-pov}

Mataas ang gastos sa pag-lock up ng kapital paa sa mga validator at delegator dahil sa disenyo ng protocol ng Proof of Stake.

Makapaghatid pa rin kami ng higit pang liquidity view mechanism gaya ng validator NFT[link sa blog mo] kung saan makakabili ng validator NFT ang sinumang bagong party na gustong maging validator mula sa isang validator na gustong umalis sa system sa anumang dahilan.

Sa mga delegator, ipinapalagay na nasa mas maliliit na bahagi ang naka-lock na halaga kaya gusto nating maging liquid iyon para mas maging active ang paglahok (hal. kung iniisip ng ilang delegator na maganda ang mga oportunidad sa defi ngayon pero naka-lock ang kanyang kapital sa pool sa pag-stake na kahit sa pag-withdraw, kailangan niyang maghintay nang 21 araw).

> Hindi libre ang pag-lock up ng X ether sa isang deposit, kailangan nitong magsakripisyo ng optionality para sa may-ari ng ether. Sa ngayon, kung mayroon akong 1000 ether, puwede kong gawin ang anumang gusto ko sa mga ito; kung ila-lock up ko ito sa isang deposit, mananatili ito roon nang ilang buwan.

> upang mapigilan ang mga pag-atake tulad ng [nothing at stake](https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ#what-is-the-nothing-at-stake-problem-and-how-can-it-be-fixed) at parusahan ang mga validator sa kanilang hindi magandang pakikilahok.

### In protocol vs application layer {#in-protocol-vs-application-layer}

> Mayroon kami ng parehong opsyon at bakit mas mainam ang in-protocol

> Kinakailangan ng liquidation ng pag-stake sa antas ng protocol na magkaroon ng malaking stake (pangunahing sa mga validator) na hindi liquid

> kung hindi, puwede itong mapinsala dulot ng tragedy of commons (ipagpalagay nating  kapag puwedeng magmay-ari ng 5% ng pool ang kahit na sino bilang max, walang kukuha ng responsibilidad na patakbuhin ang node)

May problema sa pagtitiwala ang liquidation sa pag-stake sa antas ng application, kaya mas pinapahalagahan ang liquidation sa pag-stake sa antas ng protocol dahil mapagkakatiwalaan ito ng sinumang bagong kalahok (na nakakahikayat ng mas maraming kapital, kahit mula sa mas maliliit na kalahok/delegator)

### Ang Solusyon ng Polygon para sa Pag-delegate {#polygon-s-solution-for-delegation}

Habang pinag-aaralan ang pag-delegate, napagtanto namin na kailangang maging in-protocol ang pag-delegate para magkaroon ng higit na pagtitiwala mula sa mga delegator.

Humaharap kami sa katulad na isyu sa liquidity ng kapital ng mga validator at naisip na gawin itong isang NFT na puwedeng ilipat at pinag-aralan ang mga katulad na ideya tulad ng paano ito puwedeng gawing mas liquid at napansin ang kamangha-mahang disenyo ng sikka-chorus.one 🙏 [https://blog.chorus.one/delegation-vouchers/](https://blog.chorus.one/delegation-vouchers/).

Isang magandang ideya na pag-isipang gumawa ng share ng pool ng validator. At dahil ipinapatupad ang pag-stake sa Polygon sa ethereum smart contract, nagbubukas ito ng mas maraming opsyon para sa atin gaya ng gawin itong compatible sa ERC20 para magamit ito sa mga defi protocol.

Sa ngayon, may sarili VMatic ang bawat validator (ibig sabihin, para sa validator Ashish, magkakaroon ng AMatic token)

dahil may magkakaibang performance ang bawa validator (mga gantimpala/pag-slash at rate ng komisyon).

Puwedeng bumili ang mga delegator ng maraming share ng validator at i-hedge ang kanilang panganib tungo sa pag-slash o hindi magandang performance ng partikular na validator.

### Mga Kalamangan {#advantages}

- Dahil sinusunod ng aming disenyo ang mala-ERC20 na interface sa pagpapatupad ng pag-delegate, madaling makakabuo ng mga Defi application mula rito.
- Magagamit ang mga na-delegate na token sa mga protocol sa pagpapautang.
- Puwedeng i-hedge ng mga delegator ang kanilang panganib sa pamamagitan ng mga prediction market tulad ng Auger.

Saklaw sa hinaharap:

- Sa kasalukuyan, hindi fungible ang ERC20 sa iba pang ERC20/Share token ng mga validator, pero sa tingin namin sa hinaharap, maraming bagong Defi application ang mabubuo mula rito at makakapagtaguyod ng ilang market para dito o ilang mas magandang produkto.
- Gamit ang [chorus.one](http://chorus.one) na panimulang pananaliksik, pinag-aaralan din namin ang mga problema tulad ng pagbabawas ng mga validator ng sarili nilang mga token at iba pang problema ( maiiwasan ang mga problema sa pagbabawas sa pamamagitan ng pag-lock ng validator sa sarili nilang stake sa loob ng x (na) buwan at iba pa tulad ng insurance ng validator (on-chain) na magdadala ng higit pang pagtitiwala sa mga delegator).
- Mga karapatan sa pagboto ng delegator upang makalahok sa mga desisyon sa pamamahala
- Habang ginagawang liquid ang pag-delegate, gusto rin naming tiyakin ang seguridad ng network. Dahil dito, naka-lock ang puwedeng i-slash na kapital sa ilang anyo kung sakaling magkaroon ng mapanlinlang na aktibidad.

May na-publish na higit pang impormasyon tungkol sa [link ng teknikal na disenyo hanggang sa teknikal na detalye] sa stack.matic o sa hiwalay na blog.

Gamit ang disenyo sa itaas na available in-protocol, palaging makakapagpatupad ang mga validator ng sarili nilang mga katulad na mekanismo at stake sa pamamagitan ng isang contract na hindi magiging available sa UI sa pag-stake ng Polygon.

—

direktang naka-link sa mga pangunahing asset

### Mga Layunin sa Hinaharap {#future-goals}

Mga bagay tulad ng interchain/cross-chain at lahat ay sa pamamagitan ng cosmos hub at everett B-harvest na disenyo.

### **:scroll:Mga Sanggunian**

- [Vitalik's pos design](https://medium.com/@VitalikButerin/a-proof-of-stake-design-philosophy-506585978d51)
- [Panimula sa mga Derivative sa Pag-stake](https://medium.com/lemniscap/an-intro-to-staking-derivatives-i-a43054efd51c)
- [Mga Pool sa Pag-stake](https://slideslive.com/38920085/ethereum-20-trustless-staking-pools)
- [Inflation sa Proof of Stake](https://medium.com/figment-networks/mis-understanding-yield-and-inflation-in-proof-of-stake-networks-6fea7e7c0e41)
