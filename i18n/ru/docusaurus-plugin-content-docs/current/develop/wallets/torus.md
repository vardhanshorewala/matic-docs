---
id: torus
title: Torus
description: Torus — это не предусматривающая ответственного хранения система управления ключами для децентрализованных приложений.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Torus — это удобная для пользователей, безопасная и не использующая ответственное хранение система управления ключами для децентрализованных приложений. Наша цель — дать массовым пользователям шлюз для работы с децентрализованной экосистемой.

**Тип**: без ответственного хранения/HD <br/>
 **Хранилище приватных ключей**: Хранилище локального браузера пользователя / Шифруются и хранятся на серверах Torus <br/>
 **Взаимодействие с журналом Ethereum**: Infura <br/>
 **Кодирование приватных ключей**: мнемоническое/вход с аутентификацией через социальную сеть <br/>

В зависимости от потребностей ваших приложений, Torus можно интегрировать через кошелек Torus или посредством прямого взаимодействия с сетью Torus через DirectAuth. Более подробную информацию можно найти в документации по Torus: https://docs.tor.us/getting-started

## 1. Интеграция кошелька Torus {#1-torus-wallet-integration}

Быстрый запуск кошелька Torus: https://docs.tor.us/torus-wallet/quick-start

Если ваше приложение уже совместимо с Metamask/другими поставщиками web3, интеграция кошелька Torus даст вам поставщика для оболочки этого же интерфейса web3. Вы можете выполнить установку через пакет npm или IPFS. или jsdelivr или unpkg. Более подробную информацию можно найти в документации Torus по интеграции кошелька: https://docs.tor.us/getting-started#torus-wallet-integration

**Установить пакет npm**

```bash
npm i @toruslabs/torus-embed
```

**Пример**

```js title="torus-example.js"
import Torus from "@toruslabs/torus-embed";
import Web3 from "web3";

const torus = new Torus({
  buttonPosition: "top-left" // default: bottom-left
});
await torus.init({
  buildEnv: "production", // default: production
  enableLogging: true, // default: false
  network: {
    host: "mumbai", // default: mainnet
    chainId: 80001, // default: 1
    networkName: "Mumbai Test Network" // default: Main Ethereum Network
  },
  showTorusButton: false // default: true
});
await torus.login(); // await torus.ethereum.enable()
const web3 = new Web3(torus.provider);
```

## 2. Интеграция с DirectAuth {#2-directauth-integration}

Если вы хотите контролировать UX от входа до каждого взаимодействия, вам лучше подойдет интеграция DirectAuth. Вы можете провести интеграцию с помощью одного из наших SDK в зависимости от платформ, на базе которых вы осуществляете строительство. Более подробную информацию можно найти на странице по интеграции прямой аутентификации в Torus: https://docs.tor.us/direct-auth/quick-start
