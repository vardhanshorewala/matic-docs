---
id: who-is-validator
title: Sino ang Validator
sidebar_label: Who is a Validator
description: "Isang kalahok sa network na nagpapatakbo ng mga Heimdall at Bor node."
keywords:
  - docs
  - matic
  - polygon
  - validator
image: https://matic.network/banners/matic-network-16x9.png
---

Ang validator ay isang kalahok sa network na nagla-lock up ng mga MATIC token sa system at nagpapatakbo ng mga Heimdall validator at Bor block producer node upang makatulong na patakbuhin ang network. Ini-stake ng mga validator ang kanilang mga MATIC token bilang collateral para siguruhin ang seguridad ng network at nang may kapalit para sa kanilang serbisyo, at nakakakuha ng mga gantimpala.

Ipinapamahagi ang mga gantimpala sa lahat ng nag-stake nang proporsyonal sa kanilang stake sa bawat checkpoint maliban sa proposer na nakakakuha ng karagdagang bonus. Naa-update ang balanse ng gantimpala ng user sa tinutukoy na kontrata kapag kumukuha ng mga gantimpala.

May panganib na ma-slash ang mga stake kapag gumawa ng isang mapaminsalang kilos ang validator node gaya ng dalawang bese na paglagda na nakakaapekto rin sa mga naka-link na delegator sa checkpoint na iyon.

:::note

Puwedeng lumahok bilang [mga delegator](../glossary#delegator) iyong mga interesadong gawing ligtas ang network pero hindi nagpapatakbo ng full node.

:::

## Pangkalahatang-ideya {#overview}

Pinipili ang mga validator sa Polygon network sa pamamagitan ng isang on-chain na proseso ng auction na nangyayari sa mga regular na interval. Lumalahok ang mga napiling validator na ito bilang mga block producer at verifier. Kapag na-validate na ng mga kalahok ang isang [checkpoint](../glossary#checkpoint-transaction), gagawa ng mga update sa parent chain (ang Ethereum mainnet) na siyang magbibigay ng mga gantimpala para sa mga validator depende sa kanilang stake sa network.

Umaasa ang Polygon sa isang set ng [mga validator](../glossary#validator) para i-secure ang network. Tungkulin ng mga validator na magpatakbo ng full node, [gumawa ng mga block](../glossary#block-producer), mag-validate at lumahok sa consensus, at mag-commit ng [mga checkpoint](../glossary#checkpoint-transaction) sa Ethereum mainnet. Para maging validator, kailangang [i-stake](../glossary#staking) ng isang tao ang kanilang mga MATIC token gamit ang mga kontrata sa pamamahala ng pag-stake na matatagpuan sa Ethereum mainnet.

## Mga pangunahing bahagi {#core-compenents}

Binabasa ng [Heimdall](../glossary#heimdall) ang mga event na inilabas ng mga kontrata sa pag-stake para pumili ng mga validator para sa kasalukuyang set gamit ang kanilang na-update na stake ratio, na ginagamit din ng [Bor](../glossary#bor) habang gumagawa ng mga block.

Naka-record din ang [pag-delegate](../glossary#delegator) sa mga kontrata sa pag-stake at nagkakaroon ng bisa ang anumang update sa kapangyarihan ng validator o [address ng signer](../glossary#signer-address) ng node o mga kahilingan sa pag-unbond kapag na-commit na ang susunod na checkpoint.


## End-to-end na daloy para sa isang validator ng Polygon {#end-to-end-flow-for-a-polygon-validator}

Sine-set up ng mga validator ang kanilang mga node sa paglagda, sini-sync ang data, at ini-stake ang kanilang mga token sa mga kontrata sa pag-stake sa Ethereum mainnet para matanggap bilang validator sa kasalukuyang set. Kung bakante ang isang slot, kaagad na tatanggapin ang validator. Kung hindi, kailangang dumaan ang isang tao sa mekanismo ng pagpapalit para makakuha ng slot.

:::note

May limitadong espasyo para sa pagtanggap ng mga bagong validator. Makakasali lang ang mga bagong validator sa active na set kapag nag-unbond ang isang kasalukuyang active na validator. Ipapakilala ang isang bagong proseso ng auction para sa pagpapalit ng validator.

:::

Pinipili ang mga block producer mula sa set ng validator kung saan responsibilidad ng mga napiling validator na gumawa ng mga block para sa isang ibinigay na [span](../glossary#span).

Vina-validate ng mga node sa Heimdall ang mga block na ginagawa, lumalahok sa consensus, at nagko-commit ng mga checkpoint sa Ethereum mainnet sa mga tinukoy na interval.

Nakadepende ang probability na mapili ang mga validator bilang block producer o [proposer](../glossary#proposer) ng checkpoint sa stake ratio ng isang tao, kabilang ang mga pag-delegate sa kabuuang pool.

Nakakatanggap ang mga validator ng mga gantimpala sa bawat checkpoint ayon sa kanilang stake ratio, pagkatapos ibawas ang bonus ng proposer na ibabayad sa proposer ng checkpoint.

Puwedeng mag-opt out sa system ang isang tao anumang oras at puwedeng mag-withdraw ng mga token kapag natapos na ang panahon ng pag-unbond.

## Economics {#economics}

Tingnan ang [Mga Gantimpala](/docs/maintain/validator/rewards).

## Pag-set up ng validator node {#setting-up-a-validator-node}

Tingnan ang [Mag-validate](../validate/validator-index).

## Tingnan din ang {#see-also}

* [Mga Responsibilidad ng Validator](../validate/validator-responsibilities)
* [Mag-validate](../validate/validator-index)
* [Mga Madalas Itanong tungkol sa Validator](../validate/faq/validator-faq)
