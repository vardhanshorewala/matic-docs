---
id: overview
title:
sidebar_label: Overview
description:
keywords:
  - docs
  - matic
  - wallet
image: https://matic.network/banners/matic-network-16x9.png
---





:::warning

:::

##  {#guide-to-setup-metamask-for-polygon}

*
*
*
*



###  {#1-set-up-web3}




  ```javascript
  npm install --save web3
  ```


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





>






```js
  import getWeb3 from '/path/to/web3';
```

```js
  getWeb3()
    .then((result) => {
      this.web3 = result;// we instantiate our contract next
    });
```
###  {#2-set-up-account}


```js
  this.web3.eth.getAccounts()
  .then((accounts) => {
    this.account = accounts[0];
  })
```


###  {#3-instantiate-your-contracts}


```js
  const myContractInstance = new this.web3.eth.Contract(myContractAbi, myContractAddress)
```
###  {#4-call-functions}






```js
  this.myContractInstance.methods.myMethod(myParams)
  .call()
  .then (
    // do stuff with returned values
  )
```

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
