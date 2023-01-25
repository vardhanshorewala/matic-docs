---
id: validator-staking-operations
title: Mag-stake sa Polygon
description: "Alamin kung paano mag-stake bilang validator sa Polygon Network."
keywords:
  - docs
  - matic
  - polygon
  - stake
  - claim
  - unstake
slug: validator-staking-operations
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## Mga Prerequisite {#prerequisites}

### Pag-set up ng full node {#full-node-set-up}

Ganap na naka-set up at naka-sync ang validator node mo.

Tingnan ang:

* [Magpatakbo ng Validator Node gamit ang Ansible](run-validator-ansible)
* [Magpatakbo ng Validator Node mula sa Binaries](run-validator-binaries)

### Pag-setup ng account {#account-setup}

Sa validator node mo, tiyakin na naka-set up ang account.

Para tingnan, i-run ang sumusunod na command **sa validator node**:

```sh
    heimdalld show-account
```

Dapat lumabas ang output mo sa sumusunod na format:

```json
{
    "address": "0x6c468CF8c9879006E22EC4029696E005C2319C9D",
    "pub_key": "0x04b12d8b2f6e3d45a7ace12c4b2158f79b95e4c28ebe5ad54c439be9431d7fc9dc1164210bf6a5c3b8523528b931e772c86a307e8cff4b725e6b4a77d21417bf19"
}
```

Ipapakita nito ang address at pampublikong key mo para sa iyong validator node. **Tandaan na dapat tumugma ang address na ito sa signer address mo sa Ethereum.**

### Ipakita ang pribadong key {#show-private-key}

Opsyonal ang hakbang na ito.

Sa iyong validator node, tiyakin na tama ang pribadong key.

Para tingnan, i-run ang sumusunod na command **sa validator node**:

```sh
heimdalld show-privatekey
```

Dapat lumabas ang sumusunod na output:

```json
{
    "priv_key": "0x********************************************************"
}
```

## Mag-stake sa Polygon {#stake-on-polygon}

Puwede kang mag-stake sa Polygon gamit ang [dashboard ng validator](https://wallet.polygon.technology/staking/validators/).

### Mag-stake gamit ang dashboard sa pag-stake {#stake-using-the-staking-dashboard}

1. I-access ang [dashboard ng validator](https://wallet.polygon.technology/staking/validators/).
1. Mag-log in gamit ang wallet mo. MetaMask ang inirerekomendang wallet.

   Dapat mong siguraduhin na mag-log in ka gamit ang parehong address kung saan naroon ang mga MATIC token mo.

1. I-click ang **Maging Validator**

   Hihilingin sa iyo na i-set up ang iyong node. Kung hindi mo pa na-set up ang iyong node hanggang ngayon, kakailanganin mong gawin ito, dahil kung magpapatuloy ka, makakatanggap ka ng error kapag nagtangka kang mag-stake.

1. Sa susunod na screen, idagdag ang iyong mga detalye ng validator, ang rate ng komisyon, at ang halaga ng pag-stake.
1. I-click ang **Mag-stake Ngayon**.

Kapag nakumpleto na ang transaksyon, matagumpay ka nang makakapag-stake para maging validator. Hihilingin sa iyo nang tatlong beses na kumpirmahin ang transaksyon.

* Aprubahan ang Transaksyon—aaprubahan nito ang iyong transaksyon ng pag-stake.
* Mag-stake—Kukumpirmahin nito ang iyong transaksyon ng pag-stake.
* I-save—Ise-save nito ang iyong mga detalye ng validator.

:::note

Para magkabisa ang mga pagbabago sa [dashboard sa pag-stake](https://wallet.polygon.technology/staking/my-account), nangangailangan ito ng minimum na 12 kumpirmasyon ng block.

:::

### Tingnan ang balance {#check-the-balance}

Para tingnan ang balance ng address mo:

```sh
heimdallcli query auth account SIGNER_ADDRESS --chain-id CHAIN_ID
```

kung saan

* SIGNER_ADDRESS - ang iyong [signer address](../glossary#validator).
* CHAIN_ID - ang chain ID ng Polygon mainnet kasama ang client prefix: `heimdall-137`.

Dapat lumabas ang sumusunod na output:

```json
address: 0x6c468cf8c9879006e22ec4029696e005c2319c9d
coins:
- denom: matic
amount:
    i: "1000000000000000000000"
accountnumber: 0
sequence: 0
```

### Mag-claim ng mga gantimpala bilang validator {#claim-rewards-as-a-validator}

Kapag naka-set up ka na at nag-stake bilang validator, makakakuha ka ng mga gantimpala para sa pagsasagawa ng mga tungkulin ng validator. Kapag masunurin mong isinagawa ang mga tungkulin ng validator, magagantimpalaan ka.

Para mag-claim ng mga gantimpala, puwede kang pumunta sa iyong [dashboard ng validator](https://wallet.polygon.technology/staking/my-account).

Makakakita ka ng dalawang button sa profile mo:

* I-withdraw ang Gantimpala
* I-restake ang Gantimpala

#### I-withdraw ang Gantimpala {#withdraw-reward}

Bilang validator, nakakakuha ka ng mga gantimpala hangga't isinasagawa mo ang iyong mga tungkulin ng validator nang tama.

Kapag na-click ang **I-withdraw ang Gantimpala**, ilalagay ang iyong mga gantimpala sa wallet mo.

Maa-update ang dashboard pagkatapos ng 12 kumpirmasyon ng block.

#### I-restake ang Gantimpala {#restake-reward}

Ang pag-restake ng mga gantimpala mo ay madaling paraan para  dagdagan ang iyong stake bilang validator.

Kapag na-click ang **I-restake ang Gantimpala**, magre-restake sa iyong gantimpala at magpapataas sa iyong stake.

Maa-update ang dashboard pagkatapos ng 12 kumpirmasyon ng block.
