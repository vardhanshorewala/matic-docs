---
id: validator-responsibilities
title: Mga Responsibilidad ng Validator
description: Pangkalahatang-ideya ng mga responsibilidad ng isang validator sa Polygon network Network.
keywords:
  - docs
  - matic
  - polygon
  - validator
slug: validator-responsibilities
image: https://matic.network/banners/matic-network-16x9.png
---

Ang blockchain validator ay isang taong may responsibilidad sa pag-validate ng mga transaksyon sa loob ng isang blockchain. Sa Polygon Network, puwedeng maging kwalipikado ang sinumang kalahok na maging validator ng Polygon sa pamamagitan ng pagpapatakbo ng full node para makakuha ng mga reward at makakolekta ng mga bayarin sa transaksyon. Para matiyak ang magandang pakikilahok ng mga validator, ila-lock nila ang hindi bababa sa 1 MATIC token bilang stake sa ecosystem.

:::note


Sa kasalukuyan, may limitasyon na 100 active validator sa isang panahon.
Para sa detalyadong paglalarawan kung ano ang validator, tingnan ang [Validator](../validator/architecture).

:::

## Mga Responsibilidad {#responsibilities}

Ang sinumang [validator](../glossary#validator) sa Polygon Network ay may mga sumusunod na responsibilidad:

* Mga teknikal na pagpapatakbo ng node na ginagawa ng mga node.
* Mga Operasyon:
  * Panatilihin ang mataas na uptime.
  * I-check araw-araw ang mga serbisyo at prosesong nauugnay sa node.
  * I-run ang pagsubaybay sa node.
  * Panatilihin ang balance ng ETH sa signer address.
* Pag-delegate:
  * Maging bukas sa pag-delegate.
  * Ipaalam ang mga rate ng komisyon.
* Komunikasyon:
  * Ipaalam ang mga isyu.
  * Magbigay ng feedback at mga mungkahi.
* I-stake ang mga token ng network at patakbuhin ang mga validator node para makasali sa system bilang validator.
* Makakuha ng mga gantimpala sa pag-stake para sa pag-validate ng mga state transition sa blockchain.
* Saklaw ng mga parusa/pag-slash para sa mga aktibidad tulad ng double signing, validator downtime, atbp.

### Mga teknikal na operasyon ng node {#technical-node-operations}

Ang mga sumusunod na teknikal na operasyon ng node ay awtomatikong ginagawa ng mga node:

* Pagpili ng block producer:
  * Pumili ng subset ng mga validator para sa block producer set para sa bawat [span](../glossary#span)
  * Para sa bawat span, piliing muli ang block producer set sa [Heimdall](../glossary#heimdall) at i-transmit ang impormasyon ng pagpili sa [Bor](../glossary#bor) nang pana-panahon.
* Pag-validate ng mga block sa Bor:
  * Sa isang set ng mga block ng Bor sidechain, hiwalay na binabasa ng bawat validator ang block data para sa mga block na ito at vina-valifate ang data sa Heimdall
* Pagsusumite ng checkpoint:
  * Isang [tagapanukala](../glossary#proposer) ang pinipili mula sa mga validator para sa bawat Heimdall block. Ginagawa ng tagapanukala ng [checkpoint](../glossary#checkpoint-transaction) ang checkpoint ng data ng Bor block, vina-validate, at bino-broadcast ang nilagdaang transaksyon para payagan ng iba pang validator.
  * Kapag nagkaroon ng consensus ang >2/3 ng mga aktibong validator, isusuote na ang checkpoint sa Ethereum mainnet.
* I-sync ang mga pagbabago sa mga kontrata sa pag-stake ng Polygon sa Ethereum:
  * Kasunod ng hakbang sa pagsusumite ng checkpoint, dahil isa itong external network call, ang transaksyon ng checkpoint sa Ethereum ay maaari o maaaring hindi makumpirma, o maaaring nakabinbin dahil sa mga isyu ng pagsisikip sa Ethereum.
  * Sa pagkakataong ito, mayroong `ack/no-ack`na proseso na sinusunod para matiyak na naglalaman din ng snapshot ng mga nakaraang Bor block ang susunod na checkpoint. Halimbawa, kung para sa Bor blocks 1-256 ang checkpoint 1, at nabigo ito dulot ng ilang dahilan, magiging para sa Bor blocks 1-512 ang susunod na checkpoint 2. Tingnan din ang [Arkitektura ng Heimdall: Checkpoint](../../pos/heimdall/checkpoint).
* Pag-sync ng state mula sa Ethereum mainnet papunta sa Bor sidechain:
  * Puwedeng magpalipat-lipat ang contract state sa pagitan ng Ethereum at Polygon, partikular na sa pamamagitan ng [Bor](../glossary#bor):
  * Tatawag ang DApp contract sa Ethereum ng isang function sa isang espesyal na Polygon contract sa Ethereum.
  * Nire-relay ang nauugnay na event sa Heimdall at pagkatapos ay sa Bor.
  * Tatawag ng state-sync na transaksyon sa Polygon smart contract at makukuha ng DApp ang value sa Bor sa pamamagitan ng isang function call sa mismong Bor.
  * May ipinapatipad na kaparehong mekanismo para sa pagpapadala ng state mula Polygon papuntang Ethereum. Tingnan din ang [Mekanismo ng Pag-sync ng State](../../pos/state-sync/state-sync).

### Mga Operasyon {#operations}

#### Magpanatili ng mataas na uptime {#maintain-high-uptime}

Nakabatay ang uptime ng isang node sa Polygon network sa bilang ng [mga transaksyon sa checkpoint](../glossary#checkpoint-transaction) na nalagdaan ng validator node.

Tinatayang sa bawat 34 na minuto, nagsusumite ang isang tagapanukala ng isang transaksyon sa checkpoint sa Ethereum mainnet. Kailangang nilagdaan ng bawat [validator](../glossary#validator) sa Polygon network ang transaksyon sa checkpoint.

Kapag hindi nalagdaan ang transaksyon sa checkpoint, magreresulta ito sa pagbaba ng performance ng validator node mo.

Naka-automate ang proseso ng paglagda ng mga transaksyon sa checkpoint. Para matiyak na nilalagdaan ng validator node mo ang lahat ng transaksyon sa checkpoint, dapat mong panatilihin at subaybayan ang kalusugan ng node mo.

#### I-check ang araw-araw na mga serbisyo at proseso ng node {#check-daily-node-services-and-processes}

Dapat mong i-check araw-araw ang mga serbisyo at proseso na nauugnay sa [Heimdall](../glossary#heimdall) at [Bor](../glossary#bor).

#### I-run ang pagsubaybay sa node {#run-node-monitoring}

Dapat mong i-run ang alinman sa:

* Mga Grafana Dashboard na ibinigay ng Polygon. Tingnan ang GitHub repository: [Matic-Jagar setup](https://github.com/vitwit/matic-jagar).
* O ang sarili mong tools sa pagsubaybay para sa mga [validator](../glossary#validator) at [sentry](../glossary#sentry) node.

#### Panatilihin ang balance ng ETH {#keep-an-eth-balance}

Dapat kang magpanatili ng sapat na halaga ng ETH sa iyong [signer address](../glossary#signer-address) ng validator mo sa Ethereum mainnet.

Kailangan mo ng ETH para:

* Lagdaan ang mga ipinanukalang [transaksyon sa checkpoint](../glossary#checkpoint-transaction) sa Ethereum mainnet.
* Magpanukala at magpadala ng mga transaksyon sa checkpoint sa Ethereum mainnet.

Ang hindi pagpapanatili ng sapat na halaga ng ETH sa address ng lumagda ay magreresulta sa:

* Mga pagkaantala sa pagsusumite ng checkpoint. Tandaan na maaaring magpabago-bago at tumaas ang mga presyo ng gas ng transaksyon sa Ethereum network.
* Mga pagkaantala sa finality ng mga transaksyon na kasama sa mga checkpoint.
* Mga pagkaantala sa mga susunod na transaksyon sa checkpoint.

### Pag-delegate {#delegation}

#### Maging bukas para sa pag-delegate {#be-open-for-delegation}

Kailangang maging bukas ang lahat ng validator para sa pag-delegate mula sa komunidad.

May kakayahan ang bawat validator na itakda ang sarili nilang rate ng komisyon. Walang upper limit ang rate ng komisyon.

#### Ipaalam ang mga rate ng komisyon {#communicate-commission-rates}

Tungkuling moral ng mga validator na ipaalam sa komunidad ang mga rate ng komisyon at mga pagbabago sa rate ng komisyon.

Ang mga pinipiling platform para ipaalam ang mga rate ng komisyon ay:

* [Discord](https://discord.com/invite/0xPolygon)
* [Forum](https://forum.polygon.technology/)

### Komunikasyon {#communication}

#### Ipaalam ang mga isyu {#communicate-issues}

Kapag ipinapaalam ang mga isyu nang maaga hangga't maaari, tinitiyak niyo na maitatama ng komunidad at ng team ng Polygon ang mga problema sa lalong madaling panahon.

Ang mga pinipiling platform para ipaalam ang mga rate ng komisyon ay:

* [Discord](https://discord.com/invite/0xPolygon)
* [Forum](https://forum.polygon.technology/)
* [GitHub](https://github.com/maticnetwork)

#### Magbigay ng feedback at mga mungkahi {#provide-feedback-and-suggestions}

Sa Polygon, pinapahalagahan namin ang feedback at mga mungkahi mo sa anumang aspekto ng ecosystem ng validator.

[Forum](https://forum.polygon.technology/) ang piniling platform para magbigay ng mga feedback at mungkahi.
