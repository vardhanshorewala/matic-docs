---
id: polygon-faucet
title: Polygon Faucet
sidebar_label: Polygon Faucet
description: "Запрос Matic в Polygon Faucet."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import useBaseUrl from '@docusaurus/useBaseUrl';

[Polygon Faucet](https://faucet.polygon.technology/) — это инструмент, позволяющий получать бесплатные токены MATIC в тестовой сети, чтобы помочь вам начать работать с сетью Polygon. Эти токены позволяют работать с функциями Polygon, не тратя реальные токены MATIC в основной сети.

:::note

Токены в тестовых сетях не имеют ценности, поскольку они используются только для тестирования.

:::

### Как использовать Polygon Faucet {#how-to-use-polygon-faucet}

1. Перейдите на [faucet.polygon.technology](https://faucet.polygon.technology/)

2. Выберите одну из тестовых сетей блокчейна. Где:
    - **Mumbai** - тестовая сеть Polygon
    - **Goerli** - тестовая сеть Ethereum
    - **DA Testnet** - внутреннее тестирование


 <img src={useBaseUrl("img/tools/faucet.png")} />


3. Выберите тип токена тестовой сети, который вы хотите получить, где:
   - **MATIC Token** - токен тестовой сети Polygon
   - **Test ERC20** - стандартный токен тестовой сети Ethereum
   - **Test ERC1155** - стандартный токен тестовой сети, используемый для NFT
   - **LINK** - токен тестовой сети ERC677, наследующий функции от ERC20

<img src={useBaseUrl("img/tools/select-tokens.png")} />

4. Введите адрес вашего кошелька, который вы можете скопировать из кошелька Metamask или Polygon

5. Нажмите кнопку «Отправить» для отправки вашего запроса

6. Нажмите кнопку «Подтвердить», чтобы согласовать введенные данные
<img src={useBaseUrl("img/tools/confirm-transaction.png")} />

7. Поздравляем, вы успешно отправили вашу заявку. Вы получите запрошенные токены тестовой сети в течение 1-2 минут.
<img src={useBaseUrl("img/tools/submitted.png")} />

:::note

Если у вас в аккаунте недостаточно токенов тестовой сети MATIC для оплаты комиссии за газ, возможна ошибка транзакции. Если вам требуется много тестовых токенов, свяжитесь с нами в <ins>**[Discord](https://discord.com/invite/polygon)**</ins>.

:::

:::tip

В дополнение к Polygon faucet, [Alchemy’s Mumbai Faucet](https://mumbaifaucet.com/) позволит вам тестировать приложения Polygon перед запуском, предоставляя тестовые токены MATIC. [Вот как его использовать](/docs/develop/tools/alchemy-faucet).

:::