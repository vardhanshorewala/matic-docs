---
id: truffle
title: Использование Truffle
description:  "Используйте Truffle для развертывания смарт-контракта."
keywords:
  - docs
  - matic
  - smart
  - contract
  - truffle
image: https://matic.network/banners/matic-network-16x9.png
---

## Обзор {#overview}
[Truffle](https://trufflesuite.com/) — это среда разработки блокчейна, которую вы можете использовать для создания и тестирования смарт-контрактов с помощью виртуальной машины Ethereum.

### Что вы узнаете {#what-you-will-learn}
Это руководство описывает создание смарт-контракта с помощью Truffle и его развертывание в сети Matic.

### Что вы сделаете {#what-you-will-do}
- Установите и настройте Truffle
- Разверните контракт в сети Matic Network
- Проверьте статус развертывания в Polygonscan.

## Настройка среды разработки {#setting-up-the-development-environment}

Прежде чем мы начнем, нужно проверить несколько технических требований. Пожалуйста, установите следующее:

- [Node.js v8+ LTS и npm](https://nodejs.org/en/) (идет в комплекте с Node)
- [Git](https://git-scm.com/)

После их установки нам потребуется только одна команда для установки Truffle:

    npm install -g truffle

Чтобы проверить правильность установки Truffle, введите **`truffle version`** в строку терминала. Если вы увидите ошибку, проверьте, добавлены ли модули npm к вашему пути.

:::note

Далее идет адаптированная версия статьи <ins>Краткое руководство по Truffle</ins>.

:::

## Создание проекта {#creating-a-project}
### Проект MetaCoin {#metacoin-project}

Мы используем один из шаблонов Truffle, которые можно найти на их странице [Truffle Boxes](https://trufflesuite.com/boxes/). [Бокс MetaCoin](https://trufflesuite.com/boxes/metacoin/) создает токен, который можно перемещать между аккаунтами.

1. Для начала создадим новый каталог для этого проекта Truffle:

```bash
mkdir MetaCoin
cd MetaCoin
```

2. Загрузите бокс MetaCoin:

```bash
truffle unbox metacoin
```

На последнем шаге вы создали проект Truffle, содержащий папки с контрактами, развертыванием, тестированием и файлами конфигурации.

Это данные смарт-контракта из файла `metacoin.sol`:

```solidity
// SPDX-License-Identifier: MIT
// Tells the Solidity compiler to compile only from v0.8.13 to v0.9.0
pragma solidity ^0.8.13;

import "./ConvertLib.sol";

// This is just a simple example of a coin-like contract.
// It is not ERC20 compatible and cannot be expected to talk to other
// coin/token contracts.

contract MetaCoin {
	mapping (address => uint) balances;

	event Transfer(address indexed _from, address indexed _to, uint256 _value);

	constructor() {
		balances[tx.origin] = 10000;
	}

	function sendCoin(address receiver, uint amount) public returns(bool sufficient) {
		if (balances[msg.sender] < amount) return false;
		balances[msg.sender] -= amount;
		balances[receiver] += amount;
		emit Transfer(msg.sender, receiver, amount);
		return true;
	}

	function getBalanceInEth(address addr) public view returns(uint){
		return ConvertLib.convert(getBalance(addr),2);
	}

	function getBalance(address addr) public view returns(uint) {
		return balances[addr];
	}
}
```

:::note

Обратите внимание, что ConvertLib импортируется сразу после выражения `pragma`. В этом проекте имеется два смарт-контракта, которые будут развернуты в конце: один из них — это Metacoin, содержащий всю логику отправки и баланса; другой — ConvertLib, библиотека, используемая для конвертации значений.

:::

### Тестирование контракта {#testing-the-contract}

Вы можете выполнять тесты Solidity и Javascript.

1. Запустите тест Solidity на терминале:

```bash
truffle test ./test/TestMetaCoin.sol
```

Вы увидите следующий вывод:

![img](/img/truffle/test1.png)

2. Запустите тест JavaScript:

```bash
truffle test ./test/metacoin.js
```

Вы увидите следующий вывод:

![img](/img/truffle/test2.png)

### Компиляция контракта {#compiling-the-contract}
Скомпилируйте смарт-контракт:

```bash
truffle compile
```

Вы увидите следующий вывод:

![img](/img/truffle/compile.png)

### Настройка смарт-контракта {#configuring-the-smart-contract}

Прежде чем фактически развертывать контракт, вам необходимо будет настроить файл `truffle-config.js`, вставив данные сети и компиляторов.

- Перейдите к truffle-config.js
- Обновите truffle-config учетными данными matic-network-crendentials.

```js
const HDWalletProvider = require('@truffle/hdwallet-provider');
const fs = require('fs');
const mnemonic = fs.readFileSync(".secret").toString().trim();

module.exports = {
  networks: {
    development: {
      host: "127.0.0.1",     // Localhost (default: none)
      port: 8545,            // Standard Ethereum port (default: none)
      network_id: "*",       // Any network (default: none)
    },
    matic: {
      provider: () => new HDWalletProvider(mnemonic, `https://rpc-mumbai.maticvigil.com`),
      network_id: 80001,
      confirmations: 2,
      timeoutBlocks: 200,
      skipDryRun: true
    },
  },

  // Set default mocha options here, use special reporters etc.
  mocha: {
    // timeout: 100000
  },

  // Configure your compilers
  compilers: {
    solc: {
        version: "0.8.13",
    }
  }
}
```

Обратите внимание на необходимость передачи мнемонических данных для maticProvider, это исходная фраза для аккаунта, откуда вы выполняете развертывание. Создайте новый файл `.secret` в каталоге root и введите мнемоническую фразу из 12 слов для начала работы. Чтобы получить кодовые слова для фразы из кошелька Metamask, вам нужно перейти в настройки Metamask, а затем выбрать в меню пункт «Безопасность и конфиденциальность», после чего вы увидите кнопку «Показать кодовые слова».

### Развертывание в сети Matic {#deploying-on-matic-network}

Добавьте Matic в свой кошелек с помощью https://faucet.polygon.technology/.

Запустите эту команду на корневом уровне каталога проекта:

![img](/img/truffle/deployed-contract.png)

:::note

Помните, что адрес, transaction_hash и другие предоставленные детали будут отличаться. Вышеуказанные данные призваны просто дать представление о структуре.

:::

**Поздравляем!  Вы успешно развернули смарт-контракт с помощью Truffle. Теперь вы можете взаимодействовать с ним и проверить его статус развертывания здесь: https://mumbai.polygonscan.com/.**
