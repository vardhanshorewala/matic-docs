---
id: change-signer-address
title: Baguhin ang Signer Address Mo
description: "Baguhin ang signer address ng validator mo."
keywords:
  - docs
  - matic
  - polygon
  - signer
slug: change-signer-address
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

Para sa impormasyon kung ano ang [signer address](../glossary#signer-address), tingnan ang
[Pamamahala ng Key](../validator/core-components/key-management).

## Mga Prerequisite {#prerequisites}

Tiyaking ganap na naka-sync at tumatakbo ang bagong validator node gamit ang bagong signer address.

## Baguhin ang signer address {#change-the-signer-address}

Tinutukoy sa gabay na ito ang kasalukuyan mong validator node bilang Node 1 at ang bago mong validator node bilang Node 2.

1. Mag-log in sa [dashboard sa pag-stake](https://wallet.polygon.technology/staking/) gamit ang Node 1 address.
1. Sa profile mo, i-click ang **I-edit ang Profile**.
1. Sa field na *Address ng signer*, ilagay ang Node 2 address.
1. Sa field na *Pampublikong key ng signer*, ilagay ang pampublikong key ng Node 2.

   Para makuha ang pampublikong key, paganahin ang sumusunod na command sa validator node:

   ```sh
   heimdalld show-account
   ```

Kapag na-click ang **I-save**, mase-save ang mga bagong detalye mo para sa iyong node. Ibig sabihin nito, Node 1 ang magiging address mo na kokontrol sa stake, kung saan ipapadala ang mga reward, atbp. At Node 2 na ang magsasagawa ng mga aktibidad tulad ng pag-sign ng mga block, pag-sign ng mga checkpoint, atbp.
