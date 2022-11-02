---
id: mapping-assets
title: Сопоставление активов с использованием Plasma
description: "Сопоставление активов из Polygon в Ethereum."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Токены ERC20 и ERC721 в Ethereum можно вносить на депозит и выводить из Polygon chain, используя протокол plasma. Для этого необходимо выполнить сопоставление контракта токена в Ethereum (_rootToken_) с контрактом токена в Polygon chain(_childToken_).

Вы можете отправить заявку на сопоставление [здесь](/docs/develop/ethereum-polygon/submit-mapping-request). Обратите внимание, что эта форма отправки заявки на сопоставление предназначена для моста Plasma, а для моста PoS необходимо напрямую связаться с командой matic через discord.

## Сопоставление токена {#mapping-a-token}

Сопоставление токена включает развертывание контракта _childToken_ в Polygon chain и регистрацию токена в главной цепочке и Polygon chain.

Ограниченный _childToken_ развертывается и регистрируется в Polygon автоматически посредством вызова контракта в контракт ChildChain. Однако если _rootToken_ имеет дополнительные функции помимо базовых ERC20/ERC721, пользовательский контракт _childToken_ необходимо развернуть вручную. (Читайте раздел [Добавление дополнительных функций](/docs/develop/ethereum-polygon/plasma/mapping-assets#adding-functionality-to-child-token))

## Развертывание «ограниченного» дочернего токена {#deploying-a-restricted-child-token}

### Шаг 1: В Polygon {#step-1-on-polygon}

[`addToken` Вызов функции](https://github.com/maticnetwork/contracts/blob/fd4ed8343a8abb2dda5fe5a6a75a747cfd7a2807/contracts/child/ChildChain.sol#L55) в контракте ChildChain развертывает в Polygon дочерний токен с ограниченным функционалом (см.: [ChildERC20](https://github.com/maticnetwork/contracts/blob/master/contracts/child/ChildERC20.sol) и [ChildERC721](https://github.com/maticnetwork/contracts/blob/master/contracts/child/ChildERC721.sol)). Это необходимо для обеспечения безопасности Plasma для актива, а в противном случае модель ломается. Так что, если вам нужна безопасность Plasma с пользовательским токеном и дополнительные функции сверх предоставляемых типовым токеном, вам необходимо записать контракты безопасно с установленными ограничениями.

Определенные структуры данных поддерживаются для отслеживания актива в Polygon: при этом отслеживаются события [Deposit](https://github.com/maticnetwork/contracts/blob/fd4ed8343a8abb2dda5fe5a6a75a747cfd7a2807/contracts/child/BaseERC20.sol#L6), [Withdraw](https://github.com/maticnetwork/contracts/blob/fd4ed8343a8abb2dda5fe5a6a75a747cfd7a2807/contracts/child/BaseERC20.sol#L14), [LogTransfer](https://github.com/maticnetwork/contracts/blob/fd4ed8343a8abb2dda5fe5a6a75a747cfd7a2807/contracts/child/BaseERC20.sol#L22). Все это абсолютно необходимо для контрактов Plasma, которые считывают эти данные для обеспечения верификации данных в сайдчейне посредством защиты от мошенничества и предикатов Plasma.

Прислушавшись к отзывам разработчиков, мы добавили механизмы, позволяющие разработчикам программировать любые ограничения, которые они захотят сохранить для трансферов. В качестве примера можно посмотреть [этот документ](/docs/develop/advanced/custom-restrictions). Это позволяет кодировать произвольную логику до безопасной передачи Plasma, сохраняя логику трансфера и пользовательскую логику разделенными для обеспечения безопасности Plasma.

#### Примечание по ограничениям {#note-on-restrictions}

Безопасность Plasma относительно просто реализовать для контролируемых пользователем аккаунтов или EOA, поскольку владение активом можно легко определить. Однако контракты для Plasma сложно программировать, поскольку информацию о владении активами нельзя получать заранее, и она может отличаться в зависимости от сложности контракта.

Поэтому мы поддерживаем некоторые типы контрактов, такие как [предикаты Plasma](https://github.com/maticnetwork/contracts/tree/master/contracts/root/predicates). Мы начинаем с нескольких готовых предикатов, таких как трансфер активов, своп активов и т. д., и будем увеличивать количество готовых предикатов для отражения разнообразных сценариев использования.

### Шаг 2: В Ethereum {#step-2-on-ethereum}

Сопоставление контракта реестра обновляется для каждого сопоставляемого актива. Это выполняется с помощью[`mapToken` вызова функции](https://github.com/maticnetwork/contracts/blob/fd4ed8343a8abb2dda5fe5a6a75a747cfd7a2807/contracts/common/Registry.sol#L64) в Ethereum (или Ropsten). Эта функция принимает сопоставленный адрес, возвращаемый в результате вызова `addToken` к ChildChain и обновляет сопоставление в Ethereum.

## Перемещение актива {#moving-an-asset}

### Депозиты {#deposits}

1. Контракту Deposit Manager Contract разрешено потратить X от имени msg.sender
2. Deposit Manager выполняет трансфер количества от msg.sender себе

Это обеспечивает блокировку актива в основной цепочке и невозможность трансфера во время использования токена в Polygon

### Вывод {#withdrawals}

1. Сожгите токены в сайдчейне Polygon
2. Отправьте доказательство сжигания (получение tx сжигания) в корневой цепочке
   1. Этот шаг выполняется только после включения блока, состоящего из tx сжигания, в checkpoint в корневой цепочке.
   2. После отправки checkpoint успешное выполнение этого шага
      1. означает инициирование периода Challenge Exit (в основной сети этот период составляет 7 дней, а в тестовых сетях — 5 минут)
      2. Выполняет минтинг токена ExitNFT в аккаунт выходящего, что отражает выход, инициированный выходящим в дочерней цепочке
   3. processExits сжигает Exit NFT и выполняет трансфер токенов обратно из Deposit manager выходящему.

## Добавление функций в дочерний токен {#adding-functionality-to-child-token}

В некоторых случаях вам могут потребоваться дополнительные функции помимо предоставляемых ограниченным дочерним токеном. Чтобы добавить пользовательский токен как дочерний элемент в Polygon, вы можете унаследовать стандартный контракт plasma и добавить пользовательские функции в соответствии с использованием. Например,

```javascript

pragma solidity ^0.5.2;

import { ChildERC20 } from "./ChildERC20.sol";


contract YourCustomChildToken is ChildERC20 {

  // your custom functions

}
```

### request-submission {#request-submission}

Выполните [это](/docs/develop/ethereum-polygon/submit-mapping-request).
