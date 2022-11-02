---
id: erc20
title: Руководство по депозиту и выводу ERC20
sidebar_label: ERC20
description:  "Депозит и вывод токенов ERC20 в сети Polygon."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Ознакомьтесь с актуальной [документацией Matic.js по Plasma ERC20](https://maticnetwork.github.io/matic.js/docs/plasma/erc20/), чтобы начать работу и посмотреть актуальные методы.

### Поток высокого уровня {#high-level-flow}

#### **Депозит ERC20 (процесс из 2 шагов)**

1. Предварительно необходимо одобрить токены в корневом контракте Polygon в родительской цепочке (Ethereum/Goerli).
2. После одобрения функция **депозита** вызывается тогда, когда токены вносятся на депозит на контракт Polygon и становятся доступными для использования в сети Polygon.

#### **Трансфер ERC20**

После получения средств в Polygon вы сможете использовать эти средства для мгновенной отправки другим.

#### **Вывод ERC20 (процесс из 3 шагов)**

1. Вывод средств инициируется Polygon. Устанавливается интервал checkpoint в 30 минут (для тестовых сетей подождать ~10), когда все блоки на уровне блоков Polygon сверяются с последним checkpoint.
2. После отправки checkpoint в контракт основной цепочки ERC20 создается токен NFT Exit (ERC721) эквивалентной ценности.
3. Выведенные средства можно затребовать обратно на аккаунт ERC20 из контракта основной цепочки с использованием процедуры процесс-выход.

## Настройка деталей {#setup-details}

---

### Настройка Polygon Edge {#configuring-polygon-edge}

Установите Matic SDK (**_3.0.0)_**

```bash
npm i @maticnetwork/maticjs-plasma
```

### util.js {#util-js}

Инициирование клиента Maticjs

```js
// const use = require('@maticnetwork/maticjs').use
const { Web3ClientPlugin } = require('@maticnetwork/maticjs-web3')
const { PlasmaClient } = require('@maticnetwork/maticjs-plasma')
const { use } = require('@maticnetwork/maticjs')
const HDWalletProvider = require('@truffle/hdwallet-provider')
const config = require('./config')

// install web3 plugin
use(Web3ClientPlugin)

const privateKey = config.user1.privateKey
const from = config.user1.address

async function getPlasmaClient (network = 'testnet', version = 'mumbai') {
  try {
    const plasmaClient = new PlasmaClient()
    return plasmaClient.init({
      network: network,
      version: version,
      parent: {
        provider: new HDWalletProvider(privateKey, config.parent.rpc),
        defaultConfig: {
          from
        }
      },
      child: {
        provider: new HDWalletProvider(privateKey, config.child.rpc),
        defaultConfig: {
          from
        }
      }
    })
  } catch (error) {
    console.error('error unable to initiate plasmaClient', error)
  }
}
```

### process.env {#process-env}

Создайте в корневом каталоге новый файл с именем process.env

```bash
USER1_FROM =
USER1_PRIVATE_KEY =
USER2_ADDRESS =
ROOT_RPC =
MATIC_RPC =
```

---

## deposit.js {#deposit-js}

**Одобрение**: Это нормальное одобрение ERC20, позволяющее **_depositManagerContract_** вызывать функцию **_transferFrom_**. Клиент Polygon Plasma открывает метод **_erc20Token.approve_** для осуществления этого вызова.

**Депозит**: депозит может выполняться посредством вызова **_depositERC20ForUser_** в контракте depositManagerContract.

> Обратите внимание, что сопоставление и утверждение токена для передачи необходимо выполнить заранее.

Метод **_erc20Token.deposit_** для выполнения этого вызова.

```js
const { getPlasmaClient, plasma, from } = require('../utils')

const amount = '1000000000000000000' // amount in wei
const token = plasma.parent.erc20

async function execute () {
  const plasmaClient = await getPlasmaClient()
  const erc20Token = plasmaClient.erc20(token, true)
  const result = await erc20Token.deposit(amount, from)
  const receipt = await result.getReceipt()
  console.log(receipt)
}

execute().then(() => {
}).catch(err => {
  console.error('err', err)
}).finally(_ => {
  process.exit(0)
})
```

> ПРИМЕЧАНИЕ. Депозиты из Ethereum в Polygon выполняются с использованием механизма синхронизации состояния, и это занимает примерно ~5-7 минут. После ожидания в течение этого временного интервала рекомендуется проверить баланс с помощью библиотеки web3.js/matic.js или Metamask. Баланс будет показан в обозревателе, только в дочерней цепочке была выполнена только одна передача активов. По этой [ссылке](/docs/develop/ethereum-polygon/plasma/deposit-withdraw-event-plasma) вы узнаете, как отслеживать события депозита.

## transfer.js {#transfer-js}

```js

const { getPlasmaClient, from, plasma, to } = require('../utils')

const amount = '1000000000' // amount in wei
const token = plasma.child.erc20

async function execute () {
  try {
    const plasmaClient = await getPlasmaClient()
    const erc20Token = plasmaClient.erc20(token)
    const result = await erc20Token.transfer(amount, to, { gasPrice: 1000000000 })
    const txHash = await result.getTransactionHash()
    const receipt = await result.getReceipt()
  } catch (error) {
    console.log(error)
  }
}

execute().then(() => {
}).catch(err => {
  console.error('err', err)
}).finally(_ => {
  process.exit(0)
})
```

## Вывод {#withdraw}

### 1. Сжигание {#1-burn}

Пользователь может вызвать функцию **_withdraw_** контракта дочернего токена **_getERC20TokenContract_**. Эта функция должна сжечь токены. Клиент Polygon Plasma открывает метод **_withdrawStart_** для выполнения этого вызова.

```js
const { getPlasmaClient, from, plasma } = require('../utils')

const amount = '1000000000000000' // amount in wei
const token = plasma.child.erc20
async function execute () {
  const plasmaClient = await getPlasmaClient()
  const erc20Token = plasmaClient.erc20(token)
  const result = await erc20Token.withdrawStart(amount)
  console.log(await result.getReceipt())
}

execute().then(() => {
}).catch(err => {
  console.error('err', err)
}).finally(_ => {
  process.exit(0)

```

### 2. confirm-withdraw.js {#2-confirm-withdraw-js}


Пользователь может вызвать функцию **_startExitWithBurntTokens_** контракта**_erc20Predicate_**. Эта функция должна сжечь токены. Клиент Polygon Plasma открывает метод **_withdrawConfirm_** для выполнения этого вызова. Эту функцию можно вызвать только после включения контрольной точки в основную цепочку. Включение контрольной точки можно отследить с помощью этого [руководства](/docs/develop/ethereum-polygon/plasma/deposit-withdraw-event-plasma#checkpoint-events).


```js
//Wait for ~10 mins for Mumbai testnet or ~30mins for Ethereum Mainnet till the checkpoint is submitted for burned transaction, then run the confirm withdraw
const { getPlasmaClient, from, plasma } = require('../utils')

async function execute () {
  const plasmaClient = await getPlasmaClient()
  const erc20Token = plasmaClient.erc20(plasma.parent.erc20, true)
  const result = await erc20Token.withdrawConfirm(<burn tx hash>)
  const txHash = await result.getTransactionHash()
  const txReceipt = await result.getReceipt()
  console.log(txReceipt)
}

execute().then(_ => {
  process.exit(0)
})
```

### 3. Выход из процесса {#3-process-exit}

Пользователь должен вызвать функцию **_processExits_** контракта **_withdrawManager_** и отправить доказательство сжигания. После отправки корректного доказательства токены передаются пользователю. Клиент Polygon Plasma открывает метод **_withdrawExit_** для выполнения этого вызова.

```js
const { getPlasmaClient, from, plasma } = require('../utils')

async function execute () {
  const plasmaClient = await getPlasmaClient()
  const erc20Token = plasmaClient.erc20(plasma.parent.erc20, true)
  const result = await erc20Token.withdrawExit()
  const txHash = await result.getTransactionHash()
  const txReceipt = await result.getReceipt()
  console.log(txReceipt)
}

execute().then(_ => {
  process.exit(0)
})
```

_Примечание. Контрольная точка checkpoint, отражающая все транзакции Polygon в цепочке erc20 приблизительно за каждые 30 минут, отправляется в контракт erc20 в mainchain._
