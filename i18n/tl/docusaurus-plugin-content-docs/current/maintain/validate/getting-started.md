---
id: validator-index
title: Index ng Validator
description: Isang koleksyon ng mga tagubilin kung paano paganahin at patakbuhin ang mga validator node sa Polygon Network.
keywords:
  - docs
  - polygon
  - validate
  - validator
  - maintain
  - architecture
slug: validator-index
image: https://matic.network/banners/matic-network-16x9.png
---

Mga validator ang pangunahing kalahok sa pagpapanatili ng Polygon network. Nagpapatakbo ang mga validator ng full node at sine-secure
ang network sa pamamagitan ng pag-stake ng MATIC para makagawa ng mga block, mag-validate at lumahok sa PoS consensus.

:::info

May limitadong espasyo para sa pagtanggap ng mga bagong validator. Makakasali lang ang mga bagong validator sa active na set kapag nag-unbond ang isang kasalukuyang active na validator.

Sisimulan ang isang bagong proseso ng pag-auction para sa pagpapalit ng validator.

:::

:::tip Manatiling may alam

Manatiling nakasubaybay sa mga pinakabagong update sa node at validator mula sa team ng Polygon
at sa komunidad sa pamamagitan ng pag-subscribe sa
[mga notification group sa Polygon](https://polygon.technology/notifications/).

:::

## Pangkalahatang-ideya {#overview}

Ang polygon ay binubuo ng tatlong sumusunod na mga layer:

* Ethereum layer - isang set ng mga kontrata sa Ethereum mainnet.
* Heimdall layer - isang set ng mga proof-of-stake na Heimdall node na tumatakbo nang parallel sa Ethereum mainnet, sinusubaybayan ang set ng mga kontrata sa pag-stake na naka-deploy sa Ethereum mainnet, at nagko-commit ng mga checkpoint ng Polygon Network sa Ethereum mainnet. Ang Heimdall ay nakabatay sa Tendermint.
* Bor layer - isang set ng mga block-producing Bor node na sina-shuffle ng mga Heimdall node. Ang Bor ay nakabatay sa Go Ethereum.

Para maging validator sa Polygon Network, dapat mong i-run ang:

* Sentry node - isang hiwalay na machine na nagpapatakbo ng Heimdall node at Bor node. Bukas ang sentry nose sa lahat ng node sa Polygon Network.
* Validator node - isang hiwalay na machine na nagpapatakbo ng Heimdall node at Bor node. Nakakatanggap ng data ang validator node mula sa sentry node at nagpapadala ng data sa sentry node.
* I-stake ang mga MATIC token sa mga kontrata sa pag-stake na naka-deploy sa Ethereum mainnet.

## Mga Bumubuo {#components}

### Heimdall {#heimdall}

Ginagawa ng Heimdall ang sumusunod:

* Sinusubaybayan ang mga kontrata sa pag-stake sa Ethereum mainnet.
* Vine-verify ang lahat ng transisyon ng state sa Bor chain.
* Kino-commit ang mga state checkpoint ng Bor chain sa Ethereum mainnet.

Ang Heimdall ay nakabatay sa Tendermint.

:::note

Tingnan din ang:

* Repository ng GitHub: [Heimdall](https://github.com/maticnetwork/heimdall)
* Repository ng GitHub: [Mga kontrata sa pag-stake](https://github.com/maticnetwork/contracts/tree/master/contracts/staking)
* Blog post: [Heimdall at Bor](https://blog.polygon.technology/heimdall-and-bor/)

:::

### Bor {#bor}

Ginagawa ng Bor ang sumusunod:

* Gumagawa ng mga block sa Polygon Network.

Ang Bor ay nakabatay sa Go Ethereum.

Ang Bor ay ang Block producer node at layer para sa Polygon Network. Vina-validate ng mga Heimdall node ang mga block na ginawa sa Bor.

:::note

Tingnan din ang:

* Repository ng GitHub: [Bor](https://github.com/maticnetwork/bor)
* Blog post: [Heimdall at Bor](https://blog.polygon.technology/heimdall-and-bor/)

:::

Gagabayan ka ng seksyong ito sa mga sumusunod na paksa:

* [Mga responsibilidad ng Validator](validator-responsibilities.md)
* Pagsali sa network bilang validator:
  * [Mag-start at mag-run ng mga node gamit ang Ansible](run-validator-ansible.md)
  * [Mag-start at mag-run ng mga node gamit ang binaries](run-validator-binaries.md)
  * [Mag-stake bilang isang validator](validator-staking-operations.md)
* Pagpapanatili ng mga validator node mo:
  * [Palitan ang address ng signer](change-signer-address.md)
  * [Baguhin ang komisyon](validator-commission-operations.md)

Tulong sa komunidad:

* [Discord](https://discord.com/invite/0xPolygon)
* [Forum](https://forum.polygon.technology/)
