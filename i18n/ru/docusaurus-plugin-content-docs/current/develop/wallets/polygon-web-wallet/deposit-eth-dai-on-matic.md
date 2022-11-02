---
id: deposit-eth-dai-on-polygon
title: Как внести депозит ETH/DAI в Polygon ?
description: Как получить средства в Matic OpenSea.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

В этом руководстве объясняется самый простой способ завести средства на [https://matic.opensea.io/](http://matic.opensea.io), чтобы вы могли начать покупать NFT без проблем. Средства необходимы для участия в торгах на [https://matic.opensea.io/](http://matic.opensea.io). Заказы на продажу могут размещаться при наличии баланса токенов NFT в категориях NFT, поддерживаемых на платформе. Для покупки NFT вам потребуется достаточный баланс DAI/WETH в сети Matic. Существует только два токена ERC20, которые в настоящее время поддерживаются на [https://matic.opensea.io/](http://matic.opensea.io).

Тем, кто только знакомится с L2, важно понимать, что Polygon — это сайдчейн Ethereum, созданный, чтобы повысить масштабируемость. Время подтверждения и комиссия за выполнение транзакций в Polygon намного меньше, чем в Ethereum. Поэтому, если ваши средства находятся в Ethereum, вам нужно будет перенести их на Polygon, используя мост PoS, предлагаемый Polygon.

Получить эти токены в Polygon chain можно разными способами.

<img src={useBaseUrl("img/nft-marketplace/get-funds.png")} />

1. **Внесите депозит ETH/DAI из Ethereum на Polygon, используя мост PoS на wallet.polygon.technology**

  Вы можете войти в [https://wallet.polygon.technology/](https://wallet.polygon.technology/), используя аккаунт, на котором имеется достаточный остаток ETH/DAI. Если вы вносите депозит в ETH, вы получите WETH в Polygon chain. В цепочке Matic он называется pos-WETH и имеет адрес контракта — `0x7ceB23fD6bC0adD59E62ac25578270cFf1b9f619`. Для pos-DAI адрес контракта выглядит так: `0x8f3Cf7ad23Cd3CaDbD9735AFf958023239c6A063`

<img src={useBaseUrl("img/nft-marketplace/wallet-dashboard.png")} />

Вот так выглядит дашборд кошелька при посещении [https://wallet.polygon.technology/](https://wallet.polygon.technology/)

При нажатии на кнопку депозита рядом с токеном, который вы хотите внести на депозит, откроется следующая страница.

**Депозит ETH**

<img src={useBaseUrl("img/nft-marketplace/deposit-eth.png")} />

**Депозит DAI**

<img src={useBaseUrl("img/nft-marketplace/deposit-dai.png")} />

Если у вас имеется достаточный остаток ETH/DAI в Ethereum, у вас должна быть возможность внести депозит. Это руководство содержит указания, которые помогут лучше понять принципы депозитов

[https://blog.matic.network/deposits-and-withdrawals-on-pos-bridge/](https://blog.matic.network/deposits-and-withdrawals-on-pos-bridge/)

**«ОБЯЗАТЕЛЬНО ИСПОЛЬЗУЙТЕ МОСТ PoS ПРИ ДЕПОЗИТЕ ETH/DAI».**

Этой процедуре очень важно следовать, потому что [matic.opensea.io](http://matic.opensea.io) поддерживает только pos-версию DAI/ETH. При депозите ETH/DAI с использованием моста Plasma на ваш аккаунт будут внесены на депозит токены plasma-WETH и plasma-DAI, и вы не сможете использовать их для трейдинга на matic.opensea.io. После завершения процесса депозита его финализация занимает около 7-8 минут. У вас должна иметься возможность отслеживать статус депозита в реальном времени из компонента заголовка активности, который вы сможете увидеть в правой части панели навигации. После завершения депозита вы увидите обновленный баланс в дашборде кошелька, а также в разделе «Мой аккаунт» на matic.opensea.io, как показано ниже.

<img src={useBaseUrl("img/nft-marketplace/balance.png")} />

2. **Получайте средства напрямую в Polygon от Transak.**

Это URL-адрес, который нужно открыть для покупки токенов на Transak
 [https://global.transak.com/](https://global.transak.com/)

Вы можете выбрать сеть как Polygon, а затем выбрать DAI/WETH из списка токенов и выполнить требуемые шаги в приложении transak.

3. **Получите средства с другого счета Polygon**

Если у вас имеется достаточный остаток этих токенов или другой адрес на Polygon, то вы можете выполнить трансфер этих токенов с этого адреса на тот адрес, с которым вы входите на matic.opensea.io
