---
id: delegate
title: Paano Mag-delegate
description: Alamin kung paano maging isang delegator sa Polygon Network.
keywords:
  - docs
  - matic
  - polygon
  - delegate
image: https://matic.network/banners/matic-network-16x9.png
slug: delegate
---
import useBaseUrl from '@docusaurus/useBaseUrl';

Isa itong step-by-step na gabay para tulungan kang maging isang [delegator](/docs/maintain/glossary#delegator) sa Polygon Network.

Kailangan mo lang magkaroon ng mga MATIC token at ETH sa mainnet address ng Ethereum.

## I-access ang dashboard {#access-the-dashboard}

1. Sa wallet mo (hal. MetaMask), piliin ang Ethereum mainnet.
1. Mag-log in sa [dashboard ng Polygon Wallet](https://wallet-dev.polygon.technology/staking/).
1. Kapag nag-log in ka, makikita mo ang listahan ng mga validator na may stats.

:::note

Kung isa kang validator, gumamit ng ibang hindi nagva-validate na address para mag-log in bilang isang delegator.

:::

## Mag-delegate sa isang validator {#delegate-to-a-validator}

1. I-click ang **Maging isang Delegator** o mag-scroll down sa isang partikular na validator at i-click ang **I-delegate**.
1. Ilagay ang halaga ng MATIC na ide-delegate.
1. Aprubahan ang transaksyon ng pag-delegate at i-click ang **I-delegate**.

Pagkatapos makumpleto ang transaksyon ng pag-delegate, makikita mo ang mensahe na *Nakumpleto na ang Pag-delegate*.

## Tingnan ang mga pag-delegate mo {#view-your-delegations}

Para makita ang mga pag-delegate mo, i-click ang [Account Ko](https://wallet.polygon.technology/staking/my-account).

## I-withdraw ang mga gantimpala {#withdraw-rewards}

1. I-click ang [Account Ko](https://wallet.polygon.technology/staking/my-account).
1. Sa ilalim ng na-delegate mong validator, i-click ang **I-withdraw ang Gantimpala**.

Iwi-withdraw nito ang mga MATIC token na gantimpala sa Ethereum address mo.

## I-restake ang mga gantimpala {#restake-rewards}

1. I-click ang [Account Ko](https://wallet.polygon.technology/staking/my-account).
1. Sa ilalim ng na-delegate mong validator, i-click ang **I-restake ang Gantimpala**.

Ire-restake nito ang mga MATIC token na gantimpala sa validator at dadagdagan nito ang stake mo sa pag-delegate.

## I-unbond mula sa isang validator {#unbond-from-a-validator}

1. I-click ang [Account Ko](https://wallet.polygon.technology/staking/my-account).
1. Sa ilalim ng na-delegate mong validator, i-click ang **I-unbond**.

Iwi-withdraw nito ang mga gantimpala mo mula sa validator at ang kabuuang stake mo mula sa validator.

Agad na makikita sa Ethereum address mo ang mga na-withdraw mong gantimpala.

Mala-lock sa loob ng 80 [checkpoint](../glossary#checkpoint-transaction) ang mga na-withdraw mong pondo ng stake.

Ipinatupad na ang pag-lock ng pondo sa loob ng panahon ng pag-unbond para matiyak na walang mapaminsalang gawi sa network.

## Ilipat ang stake mula sa isang node papunta sa isa pang node {#move-stake-from-one-node-to-another-node}

Isang transaksyon ang paglilipat ng stake mula sa isang ode papunta sa isa pang node. Walang pagkaantala o panahon ng pag-unbond habang nangyayari ito.

1. Mag-log in sa [Account Ko](https://wallet-dev.polygon.technology/staking/my-account) sa dashboard ng pag-stake.
1. I-click ang **Ilipat ang Stake** sa ilalim ng na-delegate mong validator.
1. Pumili ng isang external na validator at i-click ang **I-stake dito**.
1. Ilagay ang halaga ng stake at i-click ang **Ilipat ang Stake**.

Ililipat nito ang stake. Mag-a-update ang dashboard pagkatapos ng 12 pagkumpirma ng block.

:::note

Pinapayagan ang paglilipat ng stake sa pagitan ng anumang node. Ang tanging exception nito—hindi pinapayagan ang paglilipat ng stake mula sa isang Foundation node papunta sa isa pang Foundation node.

:::
