---
id: hardhat
title: Использование Hardhat
description: Используйте Hardhat для развертывания смарт-контракта.
keywords:
  - docs
  - matic
  - smart
  - contracts
  - hardhat
image: https://matic.network/banners/matic-network-16x9.png
---

## Обзор {#overview}
Hardhat — это среда разработки Ethereum, предоставляющая удобный способ развертывания контрактов, запуска тестов и локальной отладки кода Solidity.

### Что вы узнаете {#what-you-will-learn}
Из этого руководства вы узнаете, как настроить Hardhat и использовать его для создания, тестирования и развертывания простого смарт-контракта.

### Что вы сделаете {#what-you-will-do}
- Настройте Hardhat
- Создайте простой смарт-контракт
- Скомпилируйте контракт
- Протестируйте контракт
- Разверните контракт

## Настройка среды разработки {#setting-up-the-development-environment}

Прежде чем мы начнем, нужно проверить несколько технических требований. Пожалуйста, установите следующее:

- [Node.js v10+ LTS и npm](https://nodejs.org/en/) (входит в комплект Node)
- [Git](https://git-scm.com/)

После их установки вам потребуется создать проект npm, для чего вам нужно будет перейти в пустую папку, запустить `npm init` и следовать инструкциям для установки Hardhat. После готовности проекта запустите:

```bash
npm install --save-dev hardhat
```

Для создания вашего проекта Hardhat запустите `npx hardhat` в папке проекта.
 Давайте создадим образец проекта и выполним эти шаги, чтобы опробовать пример задачи и скомпилировать, протестировать и развернуть образец контракта.

:::note

Используемый здесь образец проекта основан на <ins>кратком руководстве по Hardhat</ins> и на его инструкциях.

:::

## Создание проекта {#creating-a-project}
### Образец проекта {#sample-project}

Для создания образца проекта запустите `npx hardhat` в папке вашего проекта. Вы должны увидеть следующую строку:

![img](/img/hardhat/quickstart.png)

Выберите проект JavaScript и выполните следующие шаги, чтобы скомпилировать, протестировать и развернуть образец контракта.

### Проверка контракта {#checking-the-contract}

Папка `contracts` содержит образец контракта `Lock.sol` , включающий простой цифровой замок, с которым пользователи могут выводить денежные средства только после определенного периода времени.

```solidity
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.9;

// Import this file to use console.log
import "hardhat/console.sol";

contract Lock {
    uint public unlockTime;
    address payable public owner;

    event Withdrawal(uint amount, uint when);

    constructor(uint _unlockTime) payable {
        require(
            block.timestamp < _unlockTime,
            "Unlock time should be in the future"
        );

        unlockTime = _unlockTime;
        owner = payable(msg.sender);
    }

    function withdraw() public {
        // Uncomment this line to print a log in your terminal
        // console.log("Unlock time is %o and block timestamp is %o", unlockTime, block.timestamp);

        require(block.timestamp >= unlockTime, "You can't withdraw yet");
        require(msg.sender == owner, "You aren't the owner");

        emit Withdrawal(address(this).balance, block.timestamp);

        owner.transfer(address(this).balance);
    }
}
```

### Настройка контракта {#setting-up-the-contract}

- Перейдите в `hardhat.config.js`
- Обновите `hardhat-config`, используя учетные данные matic-network-credentials
- Создайте файл `.env` в корневом каталоге для хранения вашего приватного ключа
- Добавьте ключ Polygonscan API в файл `.env` для подтверждения контракта в Polygonscan. Вы можете сгенерировать ключ API [создании аккаунта](https://polygonscan.com/register)


```js
require('dotenv').config();
require("@nomiclabs/hardhat-ethers");
require("@nomiclabs/hardhat-etherscan");

module.exports = {
  defaultNetwork: "matic",
  networks: {
    hardhat: {
    },
    matic: {
      url: "https://rpc-mumbai.maticvigil.com",
      accounts: [process.env.PRIVATE_KEY]
    }
  },
  etherscan: {
    apiKey: process.env.POLYGONSCAN_API_KEY
  },
  solidity: {
    version: "0.8.9",
    settings: {
      optimizer: {
        enabled: true,
        runs: 200
      }
    }
  },
}
```

:::note

Обратите внимание, что вышеуказанный файл требует DOTENV для управления переменными среды, а также ethers и etherscan. Обязательно установите все эти пакеты.

Найдите дополнительные инструкции по использованию DOTENV на <ins>этой странице</ins>.

:::

### Компиляция контракта {#compiling-the-contract}

Чтобы скомпилировать контракт, необходимо предварительно установить Hardhat Toolbox:
```bash
npm install --save-dev @nomicfoundation/hardhat-toolbox
```

Затем просто запустите следующую команду для компиляции:

```bash
npx hardhat compile
```

### Тестирование контракта {#testing-the-contract}
Чтобы запускать тесты с помощью Hardhat, вам нужно просто ввести следующую команду:

```bash
npx hardhat test
```

Ожидаемый результат выглядит так:

![img](/img/hardhat/test.png)

### Развертывание в сети Matic {#deploying-on-matic-network}

Запустите эту команду на корневом уровне каталога проекта:
```bash
npx hardhat run scripts/deploy.js --network matic
```

Контракт будет развернут в тестовой сети Matic Mumbai, и вы сможете проверить статус развертывания здесь: https://mumbai.polygonscan.com/

**Поздравляем! Вы успешно развернули смарт-контракт Greeter. Теперь вы можете взаимодействовать со смарт-контрактом.**

:::tip Быстрая проверка контрактов в Polygonscan

Запустите следующие команды, чтобы быстро проверить ваш контракт в Polygonscan. Это дает кому угодно возможность легко видеть исходный код развернутого контракта. Информацию о контрактах, имеющих конструктор со сложным списком аргументов, можно найти [здесь](https://hardhat.org/plugins/nomiclabs-hardhat-etherscan.html).

```bash
npm install --save-dev @nomiclabs/hardhat-etherscan
npx hardhat verify --network matic 0x4b75233D4FacbAa94264930aC26f9983e50C11AF
```
:::