---
id: metamask
title: Metamask
description: Создайте свое следующее блокчейн-приложение на Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Metamask — это надстройка для браузера, управляющая пользовательским кошельком Ethereum посредством сохранения приватного ключа в хранилище данных браузера и кодовой фразы, зашифрованной вместе с паролем. Этот кошелек не требует ответственного хранения, т. е. пользователь имеет полный доступ и несет полную ответственность за свой приватный ключ. В случае утери пользователь не сможет контролировать средства или восстановить доступ к кошельку.

**Тип**: без ответственного хранения/HD <br/>
 **Хранение приватного ключа**: хранилище локального браузера пользователя <br/>
 **Взаимодействие с журналом Ethereum**: Infura <br/>
 **Кодирование приватных ключей**: мнемоническое <br/>

### 1. Настройте Web3 {#1-set-up-web3}

**Шаг 1**

Установите в децентрализованное приложение следующее:
  ```javascript
  npm install --save web3
  ```
Создайте новый файл, назовите его `web3.js` и вставьте в него следующий код:

  ```javascript
  import Web3 from 'web3';

  const getWeb3 = () => new Promise((resolve) => {
    window.addEventListener('load', () => {
      let currentWeb3;

      if (window.ethereum) {
        currentWeb3 = new Web3(window.ethereum);
        try {
          // Request account access if needed
          window.ethereum.enable();
          // Acccounts now exposed
          resolve(currentWeb3);
        } catch (error) {
          // User denied account access...
          alert('Please allow access for the app to work');
        }
      } else if (window.web3) {
        window.web3 = new Web3(web3.currentProvider);
        // Acccounts always exposed
        resolve(currentWeb3);
      } else {
        console.log('Non-Ethereum browser detected. You should consider trying MetaMask!');
      }
    });
  });


  export default getWeb3;
  ```

Вышеуказанный файл экспортирует функцию с названием `getWeb3()`, цель которой заключается в запросе доступа к аккаунту Metamask с помощью определения глобального объекта (`ethereum` или `web3`), вставляемого Metamask.

Согласно [документации Metamask API](https://docs.metamask.io/guide/ethereum-provider.html#upcoming-provider-changes):

> MetaMask вставляет глобальный API на сайты, посещаемые его пользователями через window.ethereum (также доступно в window.web3.currentProvider по причинам совместимости). Этот API позволяет сайтам запрашивать учетные данные пользователя, загружать данные из блокчейнов, к которым подключен пользователь, и предлагать пользователю подписывать сообщения и транзакции. Вы сможете использовать этот API для обнаружения пользователя браузера web3.

Проще говоря, это означает, что если в вашем браузеер установлено расширение и (или надстройка) Metamask, у вас определена глобальная переменная с именем `ethereum` (`web3` для старых версий), и при использовании этой переменной создается экземпляр нашего объекта web3.

**Шаг 2**

Импортируйте вышеуказанный файл в код клиента
```js
  import getWeb3 from '/path/to/web3';
```
и вызовите функцию:
```js
  getWeb3()
    .then((result) => {
      this.web3 = result;// we instantiate our contract next
    });
```
### 2. Настройте аккаунт {#2-set-up-account}

Теперь для отправки транзакций (особенно меняющих состояние блокчейна) нам потребуется аккаунт для подписи этих транзакций. Мы создадим экземпляр этого контракта из объекта web3, созданного выше:
```js
  this.web3.eth.getAccounts()
  .then((accounts) => {
    this.account = accounts[0];
  })
```
Функция `getAccounts()` возвращает массив из всех аккаунтов из metamask пользователя, где `accounts[0]` — текущий выбранный пользователем аккаунт.

### 3. Создайте экземпляры ваших контрактов {#3-instantiate-your-contracts}

Когда наш объект `web3` будет на месте, мы создадим экземпляры наших контрактов > Предполагается, что API и адрес контракта у вас уже есть :)
```js
  const myContractInstance = new this.web3.eth.Contract(myContractAbi, myContractAddress)
```
### 4. Вызов функций {#4-call-functions}

Теперь мы напрямую взаимодействуем с созданным экземпляром объекта контракта (который декларирован  `myContractInstance` на шаге 2) при вызове любой функции из контракта.

Краткий обзор — функции, изменяющие состояние контракта, называются функциями `send()`, а функции, не изменяющие состояние контракта — функциями `call()`

**Вызов функций `call()`**
```js
  this.myContractInstance.methods.myMethod(myParams)
  .call()
  .then (
    // do stuff with returned values
  )
```
**Вызов функций `send()`**
```js
  this.myContractInstance.methods.myMethod(myParams)
  .send({
    from: this.account,gasPrice: 0
  })
  .then (
    (receipt) => {
      // returns a transaction receipt}
    )
```
