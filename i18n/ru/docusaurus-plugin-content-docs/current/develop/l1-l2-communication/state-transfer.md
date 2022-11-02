---
id: state-transfer
title: Трансфер состояния
description: Трансфер состояния или данных из Ethereum в Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

## Обзор {#overview}

Валидаторы Polygon постоянно отслеживают контракт в цепочке Ethereum с именем **_StateSender_**. Каждый раз, когда зарегистрированный контракт Ethereum вызывает этот контракт, он эмитирует событие. Валидаторы Polygon используют это событие для ретрансляции данных в другой контракт в цепочке Polygon. Этот механизм **_StateSync_** используется для отправки данных из Ethereum в Polygon.

Валидаторы Polygon также периодически отправляют хэш всех транзакций из цепочки Polygon в цепочку Ethereum. Данный **_Checkpoint_** можно использовать для проверки любой транзакции в Polygon. Когда осуществление транзакции в Polygon chain будет подтверждено, в Ethereum можно выполнить соответствующие действия.

Эти 2 механизма можно использовать вместе для обеспечения передачи данных (состояния) между Ethereum и Polygon в обе стороны. Чтобы абстрагировать все эти взаимодействия, вы можете напрямую наследовать наши контракты **_FxBaseRootTunnel_** (в Ethereum) и **_FxBaseChildTunnel_** (в Polygon).

### Контракт корневого туннеля {#root-tunnel-contract}

Используйте контракт `FxBaseRootTunnel`, который можно найти [здесь](https://github.com/jdkanani/fx-portal/blob/main/contracts/tunnel/FxBaseRootTunnel.sol). Этот контракт дает доступ к следующим функциям:

- `function _processMessageFromChild(bytes memory data)`: Это виртуальная функция, которая должна быть реализована в контакте, которые наследует ее для обработки данных, отправленных из ChildTunnel.
- `_sendMessageToChild(bytes memory message)`: эта функция может быть вызвана внутри цепочки с любыми байтовыми данными в качестве сообщения. Эти данные будут отправлены как в дочерний туннель.
- `receiveMessage(bytes memory inputData)`: эту функцию необходимо вызывать для получения сообщения, эмитированного ChildTunnel. Доказательство транзакции должно предоставляться как calldata. Ниже приведен пример скрипта для генерирования доказательства с использованием matic.js.

### Контракт дочернчего туннеля {#child-tunnel-contract}

Используйте контракт `FxBaseChildTunnel`, который можно найти [здесь](https://github.com/jdkanani/fx-portal/blob/main/contracts/tunnel/FxBaseChildTunnel.sol). Этот контракт дает доступ к следующим функциям:

- `function _processMessageFromRoot(uint256 stateId, address sender, bytes memory data)`: это виртуальная функция, которая необходимо для реализации логики для обработки сообщения, отправленного из RootTunnel.
- `function _sendMessageToRoot(bytes memory message)`: эту функцию можно вызвать внутри цепочки для отправки любых байтовых сообщений в корневой туннель.

## Предварительное требование {#pre-requisite}

- Вам потребуется унаследовать контракт `FxBaseRootTunnel` в корневом контракте ethereum. Например, вы можете следовать этому [контракту](https://github.com/jdkanani/fx-portal/blob/main/contracts/examples/state-transfer/FxStateRootTunnel.sol) . Аналогичным образом вам следует унаследовать контракт `FxBaseChildTunnel` в дочернем контракте или Matic. Следуйте этому [контракту](https://github.com/jdkanani/fx-portal/blob/main/contracts/examples/state-transfer/FxStateChildTunnel.sol) в качестве примера.
- При развертывании вашего корневого контракта в **тестовой сети Goerli** следует передать адрес `_checkpointManager` как `0x2890bA17EfE978480615e330ecB65333b880928e` и `_fxRoot` как `0x3d1d3E34f7fB6D26245E6640E1c50710eFFf15bA` . Для **ethereum mainnet** `_checkpointManager` — это `0x86e4dc95c7fbdbf52e33d563bbdb00823894c287` и `_fxRoot` — это `0xfe5e5D361b2ad62c541bAb87C45a0B9B018389a2`.
- Чтобы развернуть дочерний контракт в **тестовой сети Mumbai**, следует передать `0xCf73231F28B7331BBe3124B907840A94851f9f11` как `_fxChild` в конструкторе. Для **Polygon mainnet,** `_fxChild` будет `0x8397259c983751DAf40400790063935a11afa28a` .
- вызывать `setFxChildTunnel` в развернутом корневом туннеле с адресом дочернего туннеля (например: [https://goerli.etherscan.io/tx/0x79cd30ace561a226258918b56ce098a08ce0c70707a80bba91197f127a48b5c2](https://goerli.etherscan.io/tx/0x79cd30ace561a226258918b56ce098a08ce0c70707a80bba91197f127a48b5c2) )
- вызывать `setFxRootTunnel` в развернутом дочернем туннеле с адресом корневого туннеля (например: [https://mumbai.polygonscan.com/tx/0xffd0cda35a8c3fd6d8c1c04cd79a27b7e5e00cfc2ffc4b864d2b45a8bb7e98b8/internal-transactions](https://mumbai.polygonscan.com/tx/0xffd0cda35a8c3fd6d8c1c04cd79a27b7e5e00cfc2ffc4b864d2b45a8bb7e98b8/internal-transactions) )

## Примеры контрактов моста передачи состояния {#example-contracts-of-state-transfer-bridge}

- **Контракты**: [репозиторий Fx-Portal](https://github.com/jdkanani/fx-portal/tree/main/contracts/tunnel)
- **Goerli:** [0xc4432e7dab6c1b43f4dc38ad2a594ca448aec9af](https://goerli.etherscan.io/address/0xc4432e7dab6c1b43f4dc38ad2a594ca448aec9af)
- **Mumbai:** [0xa0060Cc969d760c3FA85844676fB654Bba693C22](https://mumbai.polygonscan.com/address/0xa0060Cc969d760c3FA85844676fB654Bba693C22/transactions)

## Передача состояния из Ethereum в Polygon {#state-transfer-from-ethereum-to-polygon}

- Вы должны вызвать `_sendMessageToChild()` внутри цепочки в ваш корневой контракт и передать данные в качестве аргумента для отправки в Polygon. (например: [https://goerli.etherscan.io/tx/0x28705fcae757a0c88694bd167cb94a2696a0bc9a645eb4ae20cff960537644c1](https://goerli.etherscan.io/tx/0x28705fcae757a0c88694bd167cb94a2696a0bc9a645eb4ae20cff960537644c1) )
- Реализуйте в дочернем контракте виртуальную функцию `_processMessageFromRoot()` в `FxBaseChildTunnel` для получения данных из Ethereum. Данные будут получены автоматически от приемника состояния при синхронизации состояния.

## Передача состояния из Polygon в Ethereum {#state-transfer-from-polygon-to-ethereum}

- Вызывайте `_sendMessageToRoot()` внутри дочернего контракта с данными в качестве параметра для отправки в Ethereum. ( например: [https://mumbai.polygonscan.com/tx/0x3cc9f7e675bb4f6af87ee99947bf24c38cbffa0b933d8c981644a2f2b550e66a/logs](https://mumbai.polygonscan.com/tx/0x3cc9f7e675bb4f6af87ee99947bf24c38cbffa0b933d8c981644a2f2b550e66a/logs) )
- Запишите хэш транзакции, поскольку он будет использовать для генерирования доказательств после их добавления в checkpoint. Используйте следующий образец скрипта для генерирования доказательств из хэша транзакций.

```jsx
// npm i @maticnetwork/maticjs
// for goerli - mumbai testnet
const getPOSClient = (network = 'testnet', version = 'mumbai') => {
  const posClient = new POSClient()
  return posClient.init({
    log: true,
    network: network,
    version: version,
    child: {
     <matic-provider>
    },
    parent: {
     <goerli-provider>
      }
    }
  });
}
posClient.exitUtil.buildPayloadForExit(<burntxhash>,<event signature>)
```

- Реализуйте `_processMessageFromChild()` в корневом контракте.
- Используйте сгенерированное доказательство как ввод в `receiveMessage()` для извлечения данных, отправленных из дочернего туннеля в ваш контракт. ( например: [https://goerli.etherscan.io/tx/0x436dcd500659bea715a09d9257295ddc21290769daeea7f0b666166ef75e3515](https://goerli.etherscan.io/tx/0x436dcd500659bea715a09d9257295ddc21290769daeea7f0b666166ef75e3515) )
