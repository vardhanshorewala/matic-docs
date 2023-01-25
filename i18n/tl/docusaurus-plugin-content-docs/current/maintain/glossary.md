---
id: glossary
title: Glossary
description: "Mahahalagang term sa Polygon."
keywords:
  - docs
  - matic
  - polygon
  - glossary
slug: glossary
image: https://matic.network/banners/matic-network-16x9.png
---

## Block producer {#block-producer}

Ang block producer ay isang active [validator](#validator) na pinili para magsilibi bilang block producer sa loob ng isang [span](#span).

Ang isang block producer ay responsable sa paggawa ng mga block at pag-broadcast ng mga ginawang block sa network.

## Bor {#bor}

Ang Bor node ay isang node na gumagawa ng mga block sa Polygon Network.

Ang Bor ay batay sa [Go Ethereum](https://geth.ethereum.org/).

## Transaksyon sa checkpoint {#checkpoint-transaction}

Ang checkpoint na transaksyon ay isang transaksyon na naglalaman ng Merkle root of blocks ng [Bor](#bor) layer sa pagitan ng mga interval ng checkpoint.

Nakatuon ang transaksyon sa mga kontrata ng pag-stake sa Polygon sa Ethereum mainnet sa pamamagitan ng isang [Heimdall](#heimdall) node.

Tingnan din ang:

* [Heimdall architecture: Checkpoint](../pos/heimdall/checkpoint)
* [Mekanismo ng Checkpoint](validator/core-components/checkpoint-mechanism)

## Komisyon {#commission}

Ang komisyon ay porsyento ng mga gantimpala na kinuha ng [mga validator](#validator) mula sa [mga delegator](#delegator) na nag-stake sa mga validator.

Tingnan din ang [Validator Commission Operations](/docs/maintain/validate/validator-commission-operations).

## Delegator {#delegator}

Tungkulin ng delegator na i-stake ang mga MATIC token para i-secure ang Polygon Network gamit ang mga kasalukuyang [validator](#validator) nang hindi pinapatakbo ang mga mismong node.

Tingnan din ang [Sino ang Delegator](polygon-basics/who-is-delegator).

## Full node {#full-node}

Ang full node ay isang ganap na naka-sync na [sentry node](#sentry) na tumatakbo sa [Heimdall](#heimdall) at [Bor](#bor).

Tingnan din ang [Full Node Deployment](../develop/network-details/full-node-deployment).

## Heimdall {#heimdall}

Ang Heimdall node ay isang node na tumatakbo nang sabay sa Ethereum mainnet, na sinusubaybayan ang set ng mga kontrata na naka-deploy sa Ethereum mainnet, at ikinokonekta ang mga [checkpoint](#checkpoint-transaction) ng Polygon Network sa Ethereum mainnet.

Ang Heimdall ay batay sa [Tendermint](https://tendermint.com/).

## Address ng may-ari {#owner-address}

Ang address ng may-ari ay ang address na ginamit para mag-stake, mag-restake, palitan ang address ng lumagda, i-withdraw ang mga gantimpala, at i-manage ang mga parameter na nauugnay sa delegation sa Ethereum mainnet.

Habang nananatili sa node ang [signer key](#signer-address) at itinuturing na isang *hot* wallet, kailangang panatiling mahigpit na naka-secure ang key ng may-ari, madalang na ginagamit, at itinuturing na isang *cold* wallet.

Tingnan din ang [Key Management](validator/core-components/key-management).

## Proposer {#proposer}

Ang proposer ay ang [validator](#validator) na pinili ng algorithm para mag-propose ng bagong block.

Responsibilidad din ng proposer ang pagkolekta ng lahat ng lagda para sa isang partikular na [checkpoint](#checkpoint-transaction) at pagkonekta ng checkpoint sa Ethereum mainnet.

## Sentry {#sentry}

Ang sentry node ay isang node na nagpapatakbo ng [Heimdall](#heimdall) node at [Bor](#bor) node para mag-download ng data mula sa iba pang node sa network at para mag-propagate ng [validator](#validator) data sa network.

Bukas ang isang sentry node sa lahat ng iba pang sentry node na nasa network.

## Span {#span}

Isang lohikal na tinukoy na set ng mga block kung saan pinipili ang isang set ng mga validator mula sa laht ng available na [validator](#validator).

Ang napili sa bawat span ay napagpasyahan ng hindi bababa sa 2/3 ng mga validator batay sa staking power.

Tingnan din ang [Bor Consensus: Span](../pos/bor/consensus/#span).

## Pag-stake {#staking}

Ang pag-stake ay ang proseso ng pag-lock ng mga token sa isang deposito para makakuha ng karapatang mag-validate at makagawa ng mga block sa isang blockchain. Karaniwang ginagawa ang pag-stake sa native token para sa network—dahil ni-lock ng mga validator/staker ang MATIC token sa Polygon Network. Kasama sa iba pang halimbawa ang ETH sa ETH 2.0, ATOM sa Cosmos, atbp.

Tingnan din ang [Ano ang Proof of Stake](polygon-basics/what-is-proof-of-stake).

## Address ng lumagda {#signer-address}

Ang address ng lumagda ay ang address ng isang Ethereum account ng [Heimdall](#heimdall) validator node. Nilalagdaan at isinusumite ng address ng lumagda ang [mga transaksyon ng checkpoint](#checkpoint-transaction).

Habang nananatili sa node ang signer key at itinuturing na isang *hot* wallet, kailangang panatiling mahigpit na naka-secure ang [key ng may-ari](#owner-address), madalang na ginagamit, at itinuturing na isang *cold* wallet.

Tingnan din ang [Key Management](validator/core-components/key-management).

## Validator {#validator}

Tungkulin ng validator na i-stake ang mga MATIC token at pinapatakbo ang [Heimdall](#heimdall) node at [Bor](/docs/maintain/glossary#bor) node para ikonekta ang mga checkpoint ng network sa Ethereum mainnet at para makagawa ng mga block sa network.

Bukas lang ang validator node sa [sentry](#sentry) node nito at sarado sa iba pang nasa network.

Tingnan din ang [Sino Ang Isang Validator](polygon-basics/who-is-validator).
