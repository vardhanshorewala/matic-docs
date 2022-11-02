---
id: portis
title: Portis
description: Веб-кошелек, созданный с учетом удобства организации начала работы пользователей.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
Portis — это веб-кошелек, созданный с целью упростить процесс начала работы для пользователей. Он поставляется в комплекте с javascript SDK, который интегрируется в децентрализованное приложение и создает для пользователя локальную среду без кошелька. Более того, он выполняет настройку кошелька, транзакций и комиссии за газ. Как и Metamask, он не предусматривает ответственное хранение — пользователи контролируют свои ключи, а Portis просто хранит их в безопасном режиме. Однако, в отличие от Metamask, он интегрируется в приложение, а не в браузер. Ключи пользователей связываются с их идентификаторами пользователей и паролями.

**Тип**: без ответственного хранения/HD <br/>
 **Хранение приватных ключей**: шифруются и хранятся на серверах portis <br/>
 **Связь с журналом Ethereum**: определяется разработчиком<br/>
 **Кодирование приватных ключей**: мнемоническое<br/>

### 1. Настройка Web3 {#1-setup-web3}

Установите в децентрализованное приложение следующее:
```js
npm install --save @portis/web3
```

За регистрируйте децентрализованное приложение в Portis для получения идентификатора:
> [Дашборд Portis](https://dashboard.portis.io/)

Импортируйте `portis` и объект `web3`:

```js
import Portis from '@portis/web3';
import Web3 from 'web3';
```
Конструктор Portis принимает первый аргумент как идентификатор децентрализованного приложения (полученный на предыдущем шаге), а второй аргумент — как идентификатор сети, к которой вы хотите подключиться. Это может быть строка или объект.
```js
const portis = new Portis('YOUR_DAPP_ID', 'maticTestnet');
const web3 = new Web3(portis.provider);
```
### 2. Настройте аккаунт {#2-set-up-account}

Если установка и создание экземпляра web3 были выполнены успешно, следующие действия должны успешно возвратить подключенный аккаунт:
```js
this.web3.eth.getAccounts()
.then((accounts) => {
  this.account = accounts[0];
})
```
### 3. Создание экземпляров контрактов {#3-instantiating-contracts}

Процесс создания экземпляров контрактов останется таким же, как описано выше:
```js
const myContractInstance = new this.web3.eth.Contract(myContractAbi, myContractAddress)
```
### 4. Вызов функций {#4-calling-functions}

Вызов функций останется таким же, как описано в разделе выше: #### Вызов `call()` функций
```js
this.myContractInstance.methods.myMethod(myParams)
.call()
.then (
  // do stuff with returned values
)
```
### Вызов `send()` функций {#functions}
```js
this.myContractInstance.methods.myMethod(myParams)
.send({
  from: this.account,gasPrice: 0
})
.then ((receipt) => {
  // returns a transaction receipt
})
```
