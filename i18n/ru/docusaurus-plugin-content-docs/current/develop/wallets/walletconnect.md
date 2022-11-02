---
id: walletconnect
title: Wallet Connect
description: Открытый протокол, устанавливающий связь между децентрализованным приложением и кошельком.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
Wallet Connect — это не кошелек, а открытый протокол, созданный для создания канала связи между децентрализованными приложениями и кошельками. Кошелек и приложение, поддерживающие этот протокол, могут использовать безопасное соединение с помощью общего для двух узлов ключа. Децентрализованное приложение инициирует соединение, отображая QR-код со стандартным WalletConnect URI. Когда приложение кошелька подтверждает запрос подключения, соединение устанавливается. Дополнительные запросы, связанные с переводом средств подтверждаются в самом приложении кошелька.

## 1. Настройте Web3 {#1-set-up-web3}

Чтобы настроить децентрализованное приложение для подключения к кошельку Polygon пользователя, мы можем использовать поставщик Wallet Connect для прямого подключения к Polygon. Установите в децентрализованное приложение следующее:

```bash
npm install --save @maticnetwork/walletconnect-provider
```

Установите matic.js для интеграции Matic:

```bash
$ npm install @maticnetwork/maticjs
```
Добавьте в свое приложение следующий код:

```js
import WalletConnectProvider from "@maticnetwork/walletconnect-provider"

import Web3 from "web3"
import Matic from "maticjs"
```

Затем мы настроим поставщика Polygon и Ropsten с помощью объекта Wallet Connect:

```javascript
const maticProvider = new WalletConnectProvider(
  {
    host: `https://rpc-mumbai.matic.today`,
    callbacks: {
      onConnect: console.log('connected'),
      onDisconnect: console.log('disconnected!')
    }
  }
)

const ropstenProvider = new WalletConnectProvider({
  host: `https://ropsten.infura.io/v3/70645f042c3a409599c60f96f6dd9fbc`,
  callbacks: {
    onConnect: console.log('connected'),
    onDisconnect: console.log('disconnected')
  }
})
```
Мы создали два вышеуказанных объекта поставщика для создания экземпляра объекта Web3 с помощью кода:


```js
const maticWeb3 = new Web3(maticProvider)
const ropstenWeb3 = new Web3(ropstenProvider)
```


## 2. Создание экземпляров контрактов {#2-instantiating-contracts}

После получения объекта web3 для создания экземпляров контрактов требуются те же шаги, что и для metamask.

> При этом предполагается, что ABI и адрес контракта уже есть :)

```js
const myContractInstance = new this.maticWeb3.eth.Contract(myContractAbi, myContractAddress)
```

## 3. Вызов функций {#3-calling-functions}

Как говорилось выше, в Ethereum есть два типа функций в зависимости от взаимодействия с блокчейном. Мы используем `call()` при чтении данных и `send()` при записи данных.

### Вызов `call()` функций {#functions}

Для чтения данных не требуется подпись, и поэтому процесс совпадает с описанным выше:

```js
this.myContractInstance.methods
  .myMethod(myParams)
  .call()
  .then (
  // do stuff with returned values
  )
```
### Вызов `send()` функций {#functions-1}

Поскольку для записи в блокчейн нужна подпись, пользователь получает на свой кошелек (поддерживающий Wallet Connect) предложение подписать транзакцию.

Этот процесс включает два шага:
1. Построение транзакции
2. Получение подписи на транзакции
3. Отправка подписанной транзакции


```js
const tx = {
  from: this.account,
  to: myContractAddress,
  gas: 800000,
  data: this.myContractInstance.methods.myMethod(myParams).encodeABI(),
}
```


Вышеуказанный код создает объект транзакции, который отправляется в кошелек пользователя для получения подписи:


```js
maticWeb3.eth.signTransaction(tx)
  .then((result) =>{
    maticWeb3.eth.sendSignedTransaction(result)
    .then((receipt) =>
    console.log (receipt)
  )
})
```

Функция `signTransaction()` предлагает пользователю поставить подпись, и `sendSignedTransaction()` отправляет подписанную транзакцию (возвращая подтверждение транзакции после успешной отправки).

> ПРИМЕЧАНИЕ. При этом приватный ключ находится в кошельке пользователя, и приложение не получает к нему никакого доступа. :)
