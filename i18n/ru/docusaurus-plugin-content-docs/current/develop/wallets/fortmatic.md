---
id: fortmatic
title: Fortmatic
description: Используйте Formatic SDK для интеграции своего децентрализованного приложения с Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Fortmatic SDK дает возможность легко интегрировать с блокчейном Ethereum как существующие децентрализованные приложения, интегрированные с web3, так и новые децентрализованные приложения. Fortmatic обеспечивает быструю и приятную работу для вас и для пользователей вашего приложения.

**Установить пакет npm**

```bash
$ npm i --save fortmatic@latest
```

**Пример**

```js title="example.js"
import Fortmatic from 'fortmatic';
import Web3 from 'web3';

const customNodeOptions = {
    rpcUrl: 'https://rpc-mumbai.matic.today', // your own node url
    chainId: 80001 // chainId of your own node
}

// Setting network to localhost blockchain
const fm = new Fortmatic('YOUR_TEST_API_KEY', customNodeOptions);
window.web3 = new Web3(fm.getProvider());
```
