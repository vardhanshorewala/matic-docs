---
title: Tellor
description: "Руководство по интеграции оракула Tellor в ваш контракт Polygon."
author: "Tellor"
lang: en
sidebar: true
tags: ["solidity", "smart contracts", "price feeds", "oracles", "Polygon", "Matic", "Tellor"]
skill: beginner
published: 2022-02-10
source: Tellor Docs
sourceUrl: https://docs.tellor.io/tellor/
---

Tellor — это оракул, предоставляющий устойчивые к цензуре данные, защищенные простыми криптоэкономическими стимулами. Данные могут предоставляться кем угодно и проверяться кем угодно. Гибкая структура Tellor может предоставить любые данные в любой интервал времени, чтобы обеспечить простоту экспериментирования / инноваций.

## (Мягкие) Предварительные требования {#soft-prerequisites}

Мы предполагаем, что перед работой над оракулом у вас имеются следующие навыки программирования.

Предположения:

- вы можете использовать терминал
- у вас установлен npm
- вы знаете, как использовать npm для управления зависимостями

Tellor — это активный оракул с открытым исходным кодом, готовый для реализации. Это руководство для начинающих покажет вам, как просто можно начать работу с Tellor и получить для вашего проекта полностю децентрализованный и устойчивый к цензуре оракул.

## Обзор {#overview}

Tellor — это система оракула, где стороны могут запрашивать значение точки данных вне цепочки (например, BTC/USD) и авторы отчетов соревнуются для добавления этого значения в банк данных в цепочке, доступный для всех смарт-контрактов Polygon. Вводы в этот банк данных защищены сетью авторов отчетов со стейками. Tellor использует криптоэкономические механизмы поощрения. За честную отправку данных авторы отчетов получают вознаграждение в токенах Tellor. Недобросовестные пользователи быстро наказываются и удаляются из сети посредством механима споров.

В этом руководстве мы рассмотрим следующее:

- Настройка начального набора инструментов, необходимого для начала работы.
- Выполнение простого примера.
- Укажите адреса тестовой сети для сетей, где вы можете тестировать Tellor.

## UsingTellor {#usingtellor}

Прежде всего, вам необходимо установить базовые инструменты для использования Tellor в качестве оракула. Используйте [этот пакет,](https://github.com/tellor-io/usingtellor) чтобы установить Tellor User Contracts:

`npm install usingtellor`

После установки это позволит вашим контрактам наследовать функции от контракта 'UsingTellor'.

Отлично! Теперь вы подготовили инструменты, и мы можем выполнить простое упражнение, в котором мы получим цену биткойна:

### Пример BTC/USD {#btc-usd-example}

Унаследуйте контракт UsingTellor, передав адрес Tellor в качестве аргумента конструктора:

Приведем пример:

```solidity
import "usingtellor/contracts/UsingTellor.sol";

contract BtcPriceContract is UsingTellor {

  //This Contract now has access to all functions in UsingTellor

  bytes btcPrice;
  bytes32 btcQueryId = 0x0000000000000000000000000000000000000000000000000000000000000002;

  constructor(address payable _tellorAddress) UsingTellor(_tellorAddress) public {}

  function setBtcPrice() public {
    bool _didGet;
    uint256 _timestamp;

    (_didGet, btcPrice, _timestamp) = getCurrentValue(btcQueryId);
  }
}
```

**Хотите попробовать другой источник данных? Посмотрите список поддерживаемых источников данных здесь:
 [Текущие источники данных](https://docs.tellor.io/tellor/integration/data-feed-ids)**

## Адреса: {#addresses}

Tellor Tributes: [`0xe3322702bedaaed36cddab233360b939775ae5f1`](https://polygonscan.com/token/0xe3322702bedaaed36cddab233360b939775ae5f1#code)

Оракул: [`0xfd45ae72e81adaaf01cc61c8bce016b7060dd537`](https://polygonscan.com/address/0xfd45ae72e81adaaf01cc61c8bce016b7060dd537#code)

#### Хотите сначала провести тестирование?: {#looking-to-do-some-testing-first}

Тестовая сеть Polygon Mumbai: [`0x3477EB82263dabb59AC0CAcE47a61292f28A2eA7 `](https://mumbai.polygonscan.com/address/0x3477EB82263dabb59AC0CAcE47a61292f28A2eA7/contracts#code)

#### Для более надежной реализации оракула Tellor посмотрите полный список доступных функций [здесь.](https://github.com/tellor-io/usingtellor/blob/master/README.md)
