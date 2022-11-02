---
id: getting-started
title: Мост Plasma
sidebar_label: Introduction
description: Взаимодействие с мостом Plasma и сетью Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Чтобы приступить к работе, ознакомьтесь с новейшей [документацией по Matic.js на Plasma](https://maticnetwork.github.io/matic.js/docs/plasma/).

Мост фактически представляет собой набор контрактов, помогающих перемещать активы из корневой цепочки в дочернюю цепочку. Существует два основных моста для перемещения активов между Ethereum и Polygon. Первый из них — мост Plasma, а второй — **мост PoS** или мост **доказательства стейка**. **Мост Plasma** предоставляет дополнительные гарантии безопасности, связанные с механизмом выхода Plasma.

Однако существуют определенные ограничения дочернего токена, а период вывода занимает 7 дней в связи с операциями выхода и вывода из Polygon в Ethereum через мост Plasma. [Мост PoS](/docs/develop/ethereum-polygon/pos/getting-started) — более гибкий вариант, позволяющий производить вывод быстрее.

Это руководство содержит пошаговый процесс, который поможет понять и использовать мост Plasma с помощью [Matic JS](https://github.com/maticnetwork/matic.js) — самого удобного способа взаимодействия с мостом Plasma в сети Polygon.

## Поток активов на мосту Plasma {#assets-flow-in-plasma-bridge}

В этом руководстве мы продемонстрируем поток трансфера активов в Polygon и покажем, как сделать то же самое с помощью Matic.js:

<img src={useBaseUrl("img/matic/Matic-Workflow-2.jpg")} />

1. Пользователь вносит криптовалютные активы на контракт Polygon в mainchain
2. После подтверждения депозита токенов в mainchain соответствующие токены отражаются в цепочке Polygon chain
   - Теперь пользователь может выполнить трансфер токенов любому получателю с ничтожной комиссией. Цепочка Polygon имеет более быстрые блоки (приблизительно 1 секунда). Благодаря этому трансфер выполняется практически мгновенно.
3. Когда пользователь будет готов, он сможет вывести остающиеся токены из mainchain. Вывод средств инициируется через сайдчейн Plasma. Задается интервал checkpoint в 5 минут, когда все блоки на уровне блоков Polygon проверяются по отношению к последнему checkpoint.
4. После отправки checkpoint в контракт mainchain Ethereum создается токен Exit NFT (ERC721) эквивалентной ценности.
5. Выведенные средства можно затребовать обратно на аккаунт Ethereum из контракта mainchain с использованием процедуры процесс-выход.
   - Также пользователь может получить быстрый выход через 0x или Dharma (уже скоро!)

### Предварительные условия: {#prerequisites}

```
npm i @maticnetwork/maticjs-plasma

import { PlasmaClient } from "@maticnetwork/maticjs-plasma"

const plasmaClient = new PlasmaClient();

await plasmaClient.init({
    network: <network name>,  // 'testnet' or 'mainnet'
    version: <network version>, // 'mumbai' or 'v1'
    parent: {
      provider: <parent provider>,
      defaultConfig: {
            from: <from address>
      }
    },
    child: {
      provider: <child provider>,
      defaultConfig: {
            from: <from address>
      }
    }
});

```

### Görli Faucet {#görli-faucet}

Для выполнения любых транзакций вам потребуется немного эфира на тестовых аккаунтах, которые вы будете использовать, следуя указаниям руководства. Если у вас нет ETH в Görli, вы можете использовать ссылки на faucet, приведенные здесь — https://goerli-faucet.slock.it/.

### Polygon Faucet {#polygon-faucet}

В этом руководстве мы будем использовать в качестве примера токен ERC20 `TEST` в сети Görli. Это ТЕСТОВЫЙ ТОКЕН. В своем децентрализованном приложении вы можете заменить его любым токеном ERC20. Чтобы получить тестовые `TEST` токены в сети Polygon, вы можете использовать [Polygon Faucet](https://faucet.polygon.technology/).

> Примечание. Чтобы использовать собственные токены для депозита и вывода, вам требуется выполнить «сопоставление» токена. Фактически это означает, что вы сообщаете контрактам в основной цепочке и сайдчейне о существовании вашего пользовательского токена. Прочитайте более подробную информацию о процессе сопоставления [здесь](/docs/develop/ethereum-polygon/plasma/mapping-assets) или отправьте заявку на сопоставление [здесь](/docs/develop/ethereum-polygon/submit-mapping-request).

### Базовая настройка для кошелька Metamask (опционально) {#basic-setup-for-the-metamask-wallet-optional}

1. [Создайте кошелек](/docs/develop/metamask/hello): Если вы незнакомы с кошельками, настройте аккаунт Metamask.
2. [Настройте тестовую сеть Polygon](/docs/develop/metamask/config-polygon-on-metamask): Чтобы визуализировать поток средств в Polygon, будет удобно настроить тестовую сеть Polygon на Metamask.
   > Обратите внимание, что здесь мы используем Metamask исключительно для целей визуализации. Использовать Metamask для работы с Polygon необязательно.
3. [Создайте несколько аккаунтов](/docs/develop/metamask/multiple-accounts): Прежде чем начинать выполнение руководства, создайте 3 тестовых аккаунта Ethereum.
4. [Настройте токен в Polygon](/docs/develop/metamask/custom-tokens): Чтобы легко посмотреть поток средств в Polygon с помощью Matic.js, вы можете настроить токены в Metamask.
 Токен `TEST`, который мы используем в качестве примера в этом руководстве, можно настроить в Metamask для удобной визуализации остатков на аккаунте. > Обратите внимание, что это **необязательно**. Вы можете легко запрашивать остаток токенов и другие переменные, используя [web3](https://web3js.readthedocs.io/en/1.0/)
