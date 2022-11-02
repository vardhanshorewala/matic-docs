---
id: swap-assets
title: Своп активов
description: "Руководства по свопам токенов, поддерживаемых Plasma."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

## Атомарные свопы токенов ERC20 и ERC721 с помощью свопов активов Plasma {#swap-erc20-and-erc721-tokens-atomically-using-plasma-asset-swaps}

Этот документ поможет понять свопы активов Plasma, которые можно осуществлять с помощью платформы Polygon. Это позволяет создавать такие приложения, как децентрализованные биржи, маркетплейсы NFT и тому подобное, используя нашу конструкцию Plasma, в основе которой лежат механизмы безопасности Ethereum.

## Введение в EIP712 и подписанные трансферы {#introduction-to-eip712-and-signed-transfer}
Данный раздел призван дать представление о свопе сопоставленных активов на цепочке Polygon plasma.

> Примечание: для токенов, разворачиваемых непосредственно на Polygon, этот процесс не требуется. Процесс применим только в отношении токенов, которые *соотносятся* с Polygon.

Процесс передачи активируется путем использования нового RPC-вызова `eth_SignTypedData`, впервые введенного в [EIP712](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-712.md). Это делается во избежание усложнения допуска на цепочках plasma, а также в целях упрощения доказательств мошенничества в plasma.

Данная конструкция включает введение нового метода в каждом сопутствующем контракте на актив — [ERC721](https://github.com/maticnetwork/contracts/blob/aee2433b2cb76b8bf2ad53736a9e6340cd3d9f15/contracts/child/ChildERC721.sol#L76) и [ERC20](https://github.com/maticnetwork/contracts/blob/aee2433b2cb76b8bf2ad53736a9e6340cd3d9f15/contracts/child/ChildERC20.sol#L104) на цепочке Polygon plasma под названием `transferWithSig`. А также смарт-контракт `Marketplace.sol`, который выполняет своп.


## Метод transferWithSig {#transferwithsig-method}

Ниже приводится определение этого метода:
```javascript
function transferWithSig(bytes calldata sig, uint256 amount, bytes32 data, uint256 expiration, address to) external returns (address from) {
    require(amount > 0);
    require(expiration == 0 || block.number <= expiration, "Signature is expired");

    bytes32 dataHash = getTokenTransferOrderHash(
      msg.sender,
      amount,
      data,
      expiration
    );
    require(disabledHashes[dataHash] == false, "Sig deactivated");
    disabledHashes[dataHash] = true;

    from = ecrecovery(dataHash, sig);
    _transferFrom(from, to, amount);
}
```

### Параметры {#params}
`bytes calldata sig` — подпись пользователя на ордере на расходование установленного количества токенов в обмен на другой набор токенов (создание *ордера*)

`uint256 amount` — количество токенов, подписываемых пользователем

`bytes32 data` — это хэш `keccak256` соответствующего ордера (идентификатор ордера, токен, количество)

`uint256 expiration` — номер блока, на котором должно закончиться действие ордера

`address to` — адрес составителя ордера

При вызове из внешнего контракта вышеуказанный метод подтверждает переданную подпись, конструкция которой соответствует [EIP712](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-712.md), извлекает адрес пользователя и передает указанное количество токенов с аккаунта пользователя на указанный аккаунт.

## Протокол свопа активов {#asset-swap-protocol}

В настоящее время эту конкретную функциональную возможность (передача активов с аккаунта пользователя с помощью подписи) можно использовать несколькими способами. Одним из них является маркетплейс по типу децентрализованной биржи, который выполняет атомарные свопы между токенами.

### Терминология {#terminology}
**Ордер** включает в себя идентификатор ордера, адрес токена, количество (или идентификатор токена). Пользователь подписывает **ордер** и генерирует подпись. Эта подпись затем используется для трансфера подписанного количества активов от имени пользователя.

Ниже приводится подробная спецификация смарт-контракта [Marketplace](https://github.com/maticnetwork/contracts/blob/master/contracts/child/misc/Marketplace.sol), развернутого на Polygon chain, который выполняет атомарные свопы активов.

### Marketplace.sol {#marketplace-sol}

```javascript
pragma solidity ^0.5.2;

interface MarketplaceToken {
  function transferWithSig(bytes calldata sig, uint256 tokenIdOrAmount, bytes32 data, uint256 expiration, address to) external returns (address);
}

contract Marketplace {
  struct Order {
    address token;
    bytes sig;
    uint256 tokenIdOrAmount;
  }

  function decode(bytes memory data) internal pure returns(Order memory order) {
    (order.token, order.sig, order.tokenIdOrAmount) = abi.decode(data, (address, bytes, uint256));
  }

  function executeOrder(
    bytes memory data1,
    bytes memory data2,
    bytes32 orderId,
    uint256 expiration,
    address taker
  ) public {
    Order memory order1 = decode(data1);
    Order memory order2 = decode(data2);

    // Transferring order1.token tokens from tradeParticipant1 to address2
    address tradeParticipant1 = MarketplaceToken(order1.token).transferWithSig(
      order1.sig,
      order1.tokenIdOrAmount,
      keccak256(abi.encodePacked(orderId, order2.token, order2.tokenIdOrAmount)),
      expiration,
      taker
    );

    // Transferring token2 from tradeParticipant2 to tradeParticipant1
    address tradeParticipant2 = MarketplaceToken(order2.token).transferWithSig(
      order2.sig,
      order2.tokenIdOrAmount,
      keccak256(abi.encodePacked(orderId, order1.token, order1.tokenIdOrAmount)),
      expiration,
      tradeParticipant1
    );
    require(taker == tradeParticipant2, "Orders are not complimentary");
  }
}
```
Приведенный выше контракт выполняет своп без предварительного согласования или транзакции допуска.

Функция executeOrder принимает два потока байтов, которые представляют два ордера, подлежащие урегулированию, наряду с исполнителем ордера (участником, который выполняет ордер). Расчет ордеров происходит с исполнением метода transferWithSig на двух токенах из обоих ордеров:

```javascript
address tradeParticipant1 = MarketplaceToken(order1.token).transferWithSig(
      order1.sig,
      order1.tokenIdOrAmount,
      keccak256(abi.encodePacked(orderId, order2.token, order2.tokenIdOrAmount)),
      expiration,
      taker
    );

// Transferring token2 from tradeParticipant2 to tradeParticipant1
address tradeParticipant2 = MarketplaceToken(order2.token).transferWithSig(
      order2.sig,
      order2.tokenIdOrAmount,
      keccak256(abi.encodePacked(orderId, order1.token, order1.tokenIdOrAmount)),
      expiration,
      tradeParticipant1
    );
require(taker == tradeParticipant2, "Orders are not complimentary");
```

## Руководство (своп ERC20/721) {#tutorial-erc20-721-swap}

Вот краткое руководство, с помощью которого вы можете попробовать выполнить свопы активов, поддерживаемых plasma, на Polygon.
 В вашем распоряжении имеется стандартная база исходного кода, которую можно клонировать [здесь](https://github.com/nglglhtr/asset-swap-tutorial).
 Этот репозиторий состоит из всех соответствующих контрактов, таких как ChildERC20, ChildERC721, Marketplace и их зависимостей, наряду со скриптами, которые помогут вам освоить приведенное далее руководство.

### Предварительные условия {#prerequisites}
1. Лучше всего использовать нод v10.17.0 (npm v6.11.3)
2. Truffle
```
npm install -g truffle
```
3. Web3
```
npm install -g web3
```

Клонируйте репозиторий и установите зависимости

```bash
$ git clone https://github.com/nglglhtr/asset-swap-tutorial.git
$ cd asset-swap-tutorial
$ npm i
```

> ПРИМЕЧАНИЕ: все токены, сопоставленные с Polygon (именно сопоставление обеспечивает возможность перемещения активов в основную цепочку (или корневую цепочку) и из нее), развертываются на сайдчейне Polygon в виде токенов [ChildERC20](https://github.com/maticnetwork/contracts/blob/master/contracts/child/ChildERC20.sol) и [ChildERC721](https://github.com/maticnetwork/contracts/blob/master/contracts/child/ChildERC721.sol).

Версия ChildERC20 и ChildERC721, используемая в этом руководстве, включает одну дополнительную функцию:

```javascript
// ChildERC20
function mint (uint256 amount) public {
    _mint (msg.sender, amount);
}
```
```javascript
// ChildERC721
function mint (uint256 tokenId) public {
    _mint (msg.sender, tokenId);
}
```
Они призваны помочь нам заминтить требуемые токены перед выполнением свопа.

### Шаг 1 — Настройка {#step-1-setup}
#### 1 — Компиляция контрактов и развертывание {#1-compile-contracts-and-deploy}
После клонирования репозитория скомпилируйте и перенесите контракты на предпочтительную сеть.

```bash
$ truffle compile
$ truffle migrate
```
Измените каталог на скрипты

`cd` в каталог `scripts/erc20-721/`.

#### 2 — Заполните сведения о контрактах и аккаунтах {#2-fill-in-contracts-and-accounts-details}
Откройте файл `config.js` в каталоге `/scripts/erc20-721/` и введите значения упомянутых переменных.

`provider` — провайдер сети, на которой развернуты ваши контракты

`erc20` — адрес контракта ERC20

`erc721` — адрес контракта ERC721

`marketplace` — адрес контракта с маркетплейсом

`amount` — количество токенов ERC20, которые вы хотели бы обменять на `tokenid`

`tokenid` — идентификатор токена ERC721, который вы хотели бы обменять на `amount` токенов ERC20

`privateKey1` и `privateKey2` — приватные ключи аккаунтов, участвующих в свопе

Вы можете пока не трогать переменные `orderId` и `expiration`.

> Примечание: лучше всего использовать кошелек (вместо жесткого прописывания приватных ключей в вашем коде) при построении производственной версии.

### Шаг 2 — Минт {#step-2-mint}

#### 1 — Заминтите токены в оба аккаунта {#1-mint-tokens-into-both-accounts}
Запустите
```bash
$ node mint.js
```
чтобы заминтить токены в двух аккаунтах.


Следующая функция в скрипте минтит указанное количество токенов в первом аккаунте и NFT указанного tokenId во втором аккаунте.

```javascript
async function mint () {
    await CHE.methods.mint(config.amount).send({
        from: wallet[0].address,
        gas: 6721975
    }).on('transactionHash', function(transactionHash){ console.log("erc20 mint\t" +  transactionHash) })

    await NFT.methods.mint(config.tokenid).send({
        from: wallet[1].address,
        gas: 6721975
    }).on('transactionHash', function(transactionHash){ console.log("erc721 mint\t" +  transactionHash) })
}
```

При запуске скрипта должны отобразиться хэши транзакций двух минтов токенов.

Вы можете в любой момент просмотреть остатки на двух аккаунтах, выполнив команду:
```bash
$ node balance.js
```
При этом отобразятся остатки на обоих аккаунтах для обоих токенов.

### Шаг 3 — Своп {#step-3-swap}

Чтобы произвести своп между двумя аккаунтами, мы сначала создаем две подписи (это равносильно созданию двух ордеров).


В скрипте `swap.js` функция `encode` подготавливает потоки байтов данных, которые являются первыми двумя параметрами функции `executeOrder` в смарт-контракте `Marketplace.sol`.
```javascript
function encode(token, sig, tokenIdOrAmount) {
    return web3.eth.abi.encodeParameters(
      ['address', 'bytes', 'uint256'],
      [token, sig, '0x' + tokenIdOrAmount.toString(16)]
    )
}
```

Далее мы создаем два объекта подписи, являющиеся по сути двумя ордерами, которые мы хотели бы соотнести и выполнить с помощью нашего смарт-контракта Marketplace.

```javascript
const obj1 = sigUtils.getSig({
    privateKey: privateKey1,
    spender: marketplaceAddress,
    orderId: orderId,
    expiration: expiration,

    token1: token1,
    amount1: amount1,
    token2: token2,
    amount2: amount2
})

const obj2 = sigUtils.getSig({
    privateKey: privateKey2,
    spender: marketplaceAddress,
    orderId: orderId,
    expiration: expiration,

    token2: token1,
    amount2: amount1,
    token1: token2,
    amount1: amount2
})
```

И выполняются два ордера:

```javascript
Marketplace.methods.executeOrder(
    encode(token1, obj1.sig, amount1),
    encode(token2, obj2.sig, amount2),
    orderId,
    expiration,
    address2
).send({
    from: address3,
    gas: maxGas
}).then(console.log)
```

Выполните следующую команду, чтобы исполнить своп:
```bash
$ node swap.js
```
В случае успешного свопа отображается хэш транзакции. Далее вы можете проверить остатки:

```bash
$ node balance.js
```

### Развертывание и свопинг на Polygon {#deploying-and-swapping-on-polygon}

Если вы захотите развернуть и тестировать на Polygon, требуемые шаги будут отличаться только переносом ваших смарт-контрактов на Polygon и изменением адресов контрактов в файле конфигурации.

Из корневого каталога запустите:
```bash
$ truffle migrate --network maticTestnet
```
или, в случае бета-сети Matic, запустите:
```bash
$ truffle migrate --network maticBetaMainnet
```

Когда у вас появятся адреса контрактов, введите их в файле конфигурации в каталоге `/scripts/erc20-721/` вместе с провайдером, который будет следующим для этих двух сетей:

Тестовая сеть Polygon: `<Mumbai testnet RPC URL>. Sign up for a free dedicated RPC URL at https://rpc.maticvigil.com/ or other hosted node providers.`

Polygon бета-mainnet: `https://beta.matic.network`

Подготовив файл конфигурации, запустите в каталоге `/scripts/erc20-721/` следующую команду:

Чтобы заминтить токены
```bash
$ node mint.js
```
Чтобы проверить остатки
```bash
$ node balance.js
```
Чтобы выполнить своп
```bash
$ node swap.js
```
После успешного выполнения свопа вы можете проверить и подтвердить остатки еще раз
```bash
$ node balance.js
```
