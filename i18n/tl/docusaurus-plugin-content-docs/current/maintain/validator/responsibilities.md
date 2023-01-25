---
id: responsibilities
title: Mga Responsibilidad
description: "Mga responsibilidad ng pagiging validator sa Polygon Network."
keywords:
  - docs
  - matic
  - polygon
  - validate
  - validator
  - responsibilities
slug: responsibilities
image: https://matic.network/banners/matic-network-16x9.png
---

## Pangkalahatang-ideya {#overview}

Sinumang [validator](/docs/maintain/glossary#validator) sa Polygon Network ay may mga sumusunod na responsibilidad:

* Mga teknikal na operasyon ng node na ginagawa ng mga node.
* Mga Operasyon:
  * Panatilihin ang mataas na uptime.
  * Tingnan ang mga serbisyo at proseso na may kaugnayan sa node araw-araw.
  * I-run ang pagsubaybay sa node.
  * Panatilihin ang balance ng ETH sa signer address.
* Pag-delegate:
  * Maging bukas sa pag-delegate.
  * Ipaalam ang mga rate ng komisyon.
* Komunikasyon:
  * Ipaalam ang mga isyu.
  * Magbigay ng feedback at mga mungkahi.

## Mga Responsibilidad {#responsibilities}

### Mga teknikal na operasyon ng node {#technical-node-operations}

Awtomatikong ginagawa ng mga node ang mga sumusunod na teknikal na operasyon ng node:

* Pagpili ng block producer:
  * Pumili ng subset ng mga validator para sa block producer set para sa bawat [span](../glossary#span)
  * Para sa bawat span, piliing muli ang block producer set sa [Heimdall](../glossary#heimdall) at regular na i-transmit ang impormasyon ng pagpili sa [Bor](../glossary#bor).
* Pag-validate ng mga block sa Bor:
  * Para sa isang set ng mga Bor sidechain block, malayang binabasa ng bawat validator ang data ng block para sa mga block na ito at vina-validate ang data sa Heimdall.
* Pagsusumite ng checkpoint:
  * Pipili ng isang [tagapanukala](../glossary#proposer) mula sa mga validator sa bawat Heimdall block. Ginagawa ng tagapanukala ng [checkpoint](../glossary#checkpoint-transaction) ang checkpoint ng data ng Bor block, vina-validate, at bino-broadcast ang nilagdaang transaksyon para payagan ng iba pang validator.
  * Kung higit sa 2/3 ng mga aktibong validator ang nagkaroon ng consensus sa checkpoint, isusumite ang checkpoint sa Ethereum mainnet.
* I-sync ang mga pagbabago sa mga kontrata sa pag-stake sa Polygon sa Ethereum:
  * Kasunod ng hakbang sa pagsusumite ng checkpoint, dahil isa itong external network call, posibleng nakumpirma o hindi ang transaksyon sa checkpoint sa Ethereum, o maaaring nakabinbin dahil sa mga isyu ng congestion sa Ethereum.
  * Sa kasong ito, may `ack/no-ack` na proseso na sinusunod para matiyak na naglalaman din ng snapshot ng mga nakaraang Bor block ang susunod na checkpoint. Halimbawa, kung ang checkpoint 1 ay para sa Bor blocks 1-256, at nabigo ito sa ilang dahilan, ang susunod na checkpoint 2 ay magiging para sa Bor blocks 1-512. Tingnan din ang [Arkitektura ng Heimdall: Checkpoint](../../pos/heimdall/checkpoint).
* Pag-sync ng state mula sa Ethereum mainnet papunta sa Bor sidechain:
  * Puwedeng magpalipat-lipat ang state ng kontrata sa pagitan ng Ethereum at Polygon, partikular na sa pamamagitan ng [Bor](../glossary#bor):
  * Magko-call ng function ang isang DApp contract sa Ethereum sa isang espesyal na Polygon contract sa Ethereum.
  * Nire-relay ang kaukulang kaganapan sa Heimdall at pagkatapos ay sa Bor.
  * Isang transaksyon ng pag-sync ng state ang mako-call sa isang smart contract ng Polygon at makukuha ng DApp ang value sa Bor sa pamamagitan ng isang function call sa mismong Bor.
  * May ipinapatupad na kaparehong mekanismo para sa pagpapadala ng state mula sa Polygon papuntang Ethereum. Tingnan din ang [Mekanismo ng Pag-sync sa State](../../pos/state-sync/state-sync).

### Mga Operasyon {#operations}

#### Panatilihin ang mataas na uptime {#maintain-high-uptime}

Ang uptime ng node sa Polygon Network ay batay sa bilang ng [mga transaksyon sa checkpoint](../glossary#checkpoint-transaction) na nilagdaan ng validator node.

Tinatayang sa bawat 34 na minuto, nagsusumite ang isang tagapanukala ng isang transaksyon sa checkpoint sa Ethereum mainnet. Kailangang lagdaan ng bawat [validator](../glossary#validator) sa Polygon Network ang transaksyon sa checkpoint.

Kapag hindi nalagdaan ang isang transaksyon sa checkpoint, magreresulta ito sa pagbaba ng performance ng validator node mo.

Awtomatiko ang proseso ng paglagda ng mga transaksyon sa checkpoint. Para matiyak na nilalagdaan ng validator node mo ang lahat ng transaksyon sa checkpoint, dapat mong panatilihin at subaybayan ang kalusugan ng node mo.

#### Tingnan ang mga serbisyo at proseso ng node araw-araw {#check-node-services-and-processes-daily}

Dapat mong tingnan ang mga serbisyo at proseso na nauugnay sa [Heimdall](../glossary#heimdall) at [Bor](../glossary#bor) araw-araw.

#### I-run ang pagsubaybay sa node {#run-node-monitoring}

Dapat mong i-run ang alinman sa:

* Mga Grafana Dashboard na ibinigay ng Polygon. Tingnan ang GitHub repository: [Matic-Jagar setup](https://github.com/vitwit/matic-jagar).
* O ang sarili mong tools sa pagsubaybay para sa mga [validator](../glossary#validator) at [sentry](../glossary#sentry) node.

#### Panatilihin ang balance ng ETH {#keep-an-eth-balance}

Dapat kang magpanatili ng sapat na halaga ng ETH sa [signer address](../glossary#signer-address) ng validator mo sa Ethereum mainnet.

Kailangan mo ng ETH para:

* Lagdaan ang mga ipinanukalang [transaksyon sa checkpoint](../glossary#checkpoint-transaction) sa Ethereum mainnet.
* Magpanukala at magpadala ng mga transaksyon sa checkpoint sa Ethereum mainnet.

Ang hindi pagpapanatili ng sapat na halaga ng ETH sa signer address ay magreresulta sa:

* Mga pagkaantala sa pagsusumite ng checkpoint. Tandaan na puwedeng magpabago at tumaas ang mga presyo ng gas ng transaksyon sa Ethereum network.
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

:::tip Manatiling may alam

Manatiling nakasubaybay sa mga pinakabagong update sa node at validator mula sa team ng Polygon
at sa komunidad sa pamamagitan ng pag-subscribe sa
[mga notification group sa Polygon](https://polygon.technology/notifications/).

:::
