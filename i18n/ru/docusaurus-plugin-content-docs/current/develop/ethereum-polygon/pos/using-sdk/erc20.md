---
id: erc20
title: Руководство по депозиту и выводу ERC20
sidebar_label: ERC20
description: "Депозит и вывод токенов ERC20 в сети Polygon."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Ознакомьтесь с актуальной [документацией Matic.js по ERC20](https://maticnetwork.github.io/matic.js/docs/pos/erc20/).

Это руководство использует тестовую сеть Polygon ( Mumbai ), которая сопоставлена с сетью Goerli, для демонстрации перевода активов между двумя блокчейнами. **Важно отметить, что** при следовании указаниям настоящего руководства следует использовать адрес прокси всегда, когда это возможно. Например, адрес **RootChainManagerProxy** следует использовать для взаимодействия вместо адреса **RootChainManager**. **Адреса контрактов PoS, ABI, адреса тестовых токенов** и другие детали развертывания контрактов моста PoS можно найти [здесь](/docs/develop/ethereum-polygon/pos/deployment).

**Сопоставление активов** необходимо для интеграции моста PoS в ваше приложение. Вы можете отправить запрос на сопоставление [здесь](/docs/develop/ethereum-polygon/submit-mapping-request). Однако для целей настоящего руководства мы уже развернули **тестовые токены** и выполнили их сопоставление на мосту PoS. Это может вам потребоваться, если вы захотите попробовать выполнить указания руководства самостоятельно. Вы можете запросить желаемый актив из [faucet](https://faucet.polygon.technology/). Если тестовые токены недоступны на faucet, свяжитесь с нами в [discord](https://discord.com/invite/0xPolygonn)

В будущем руководстве каждый шаг будет разъяснен подробно с предоставлением нескольких сниппетов кода. Однако вы всегда сможете сослаться на этот [репозиторий](https://github.com/maticnetwork/matic.js/tree/master/examples/pos), который будет содержать все **примеры исходного кода**, которые могут помочь вам выполнить интеграцию и понять принципы работы моста PoS.

## Поток высокого уровня {#high-level-flow}

Депозит ERC20 -

1. **_Утвердите контракт_** **_ERC20Predicate_** для получения возможности тратить вносимые на депозит токены.
2. Выполните вызов **_depositFor_** в **_RootChainManager_**.

Вывод ERC20 -

1. **_Сожгите_** токены в Polygon chain.
2. Вызовите функцию **_exit_** в **_RootChainManager_** для отправки подтверждения транзакции сжигания. Этот вызов можно сделать **_после отправки checkpoint_** для блока, содержащего транзакцию сжигания.

## Детали шага {#step-details}

---

### Утвердить {#approve}

Это нормальное утверждение ERC20, позволяющее **_ERC20Predicate_** вызвать функцию **_transferFrom_**. Клиент Polygon POS открывает метод **_approve_** для выполнения этого вызова.

```jsx
const execute = async () => {
  const client = await getPOSClient();
  const erc20RootToken = posClient.erc20(<root token address>,true);
  const approveResult = await erc20Token.approve(100);
  const txHash = await approveResult.getTransactionHash();
  const txReceipt = await approveResult.getReceipt();
}
```

### Депозит {#deposit}

Обратите внимание, что необходимо выполнить сопоставление и утверждение токена для передачи заранее. Клиент Polygon POS открывает метод **_deposit_** для осуществления этого вызова.

```jsx
const execute = async () => {
  const client = await getPOSClient();
  const erc20RootToken = posClient.erc20(<root token address>, true);

  //deposit 100 to user address
  const result = await erc20Token.deposit(100, <user address>);
  const txHash = await result.getTransactionHash();
  const txReceipt = await result.getReceipt();

}
```

> ПРИМЕЧАНИЕ. Депозиты из Ethereum в Polygon выполняются с использованием механизма синхронизации состояния, и это занимает примерно ~5-7 минут. После ожидания в течение этого временного интервала рекомендуется проверить баланс с помощью библиотеки web3.js/matic.js или Metamask. Баланс будет показан в обозревателе, только если в дочерней цепочке была выполнена только одна передача активов. По этой [ссылке](/docs/develop/ethereum-polygon/pos/deposit-withdraw-event-pos) вы узнаете, как отслеживать события депозита.

### Метод WithdrawStart для сжигания {#withdrawstart-method-to-burn}

Метод *withdrawStart* можно использовать, чтобы инициировать процесс вывода, при котором будет сжигаться определенное количество токенов в цепочке polygon chain.

```jsx
const execute = async () => {
  const client = await getPOSClient();
  const erc20Token = posClient.erc20(<child token address>);

  // start withdraw process for 100 amount
  const result = await erc20Token.withdrawStart(100);
  const txHash = await result.getTransactionHash();
  const txReceipt = await result.getReceipt();
}
```

Сохраните хэш транзакции для этого вызова и используйте его при генерировании доказательства сжигания.

### Выход {#exit}

После отправки **_checkpoint_** для блока, **_содержащего_** транзакцию сжигания, пользователь должен вызвать функцию **_exit_** контракта **_RootChainManager_** и отправить доказательство сжигания. После отправки корректного доказательства токены передаются пользователю. Клиент Polygon POS открывает метод **_withdrawExit_** для выполнения этого вызова. Эту функцию можно вызвать только после включения checkpoint в основную цепочку. Включение контрольной точки можно отследить с помощью этого [руководства](/docs/develop/ethereum-polygon/pos/deposit-withdraw-event-pos#checkpoint-events).

Метод *withdrawExit* можно использовать для выхода из процесса вывода с помощью txHash из метода *withdrawStart*.

Примечание: для выхода из процесса вывода необходимо установить контрольные точки для транзакции withdrawStart.


```jsx
const execute = async () => {
  const client = await getPOSClient();
  const erc20RootToken = posClient.erc20(<root token address>, true);
  const result = await erc20Token.withdrawExit(<burn tx hash>);
  const txHash = await result.getTransactionHash();
  const txReceipt = await result.getReceipt();
}
```
