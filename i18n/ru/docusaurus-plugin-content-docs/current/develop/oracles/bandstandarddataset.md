---
id: bandstandarddataset
title: Стандартный набор данных Band
description: "Данные по ценам из децентрализованной инфраструктуры оракула."
keywords:
  - docs
  - matic
  - band
  - oracle
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## Введение {#introduction}

Работающие с Polygon разработчики теперь могут использовать децентрализованную инфраструктуру оракулов Band. С оракулом Band они получат доступ к различным ценовым данным криптовалюты для интеграции в свои приложения.

## Поддерживаемые токены {#supported-tokens}

В настоящее время список поддерживаемых символов можно найти по адресу [data.bandprotocol.com](http://data.bandprotcool.com). В будущем этот список будет и дальше расширяться в зависимости от потребностей разработчиков и отзывов сообщества.

### Ценовые пары {#price-pairs}

Следующие методы могут работать с любой комбинацией пар токенов база/предложение, если символы базы и ценового предложения поддерживаются набором данных.

## Запросы цен {#querying-prices}

В настоящее время разработчикам доступно два метода запроса цен у оракула Band: через смарт-контракт Band `StdReference` в Polygon и через библиотеку помощника [`bandchain.js`](https://www.npmjs.com/package/%40bandprotocol%2Fbandchain.js) JavaScript.

### Смарт-контракт Solidity {#solidity-smart-contract}

Для запроса цен у оракул Band смарт-контракт должен ссылаться на контракт Band StdReference, а в частности на методы `getReferenceData` и `getReferenceDatabulk`.

`getReferenceData` принимает в качестве ввода две текстовых строки — базовый символ и символ ценового предложения. После этого он запрашивает у контракта `StdReference` последние курсы для этих двух токенов и выводит структуру `ReferenceData`, которая показана ниже.

```solidity
struct ReferenceData {
    uint256 rate; // base/quote exchange rate, multiplied by 1e18.
    uint256 lastUpdatedBase; // UNIX epoch of the last time when base price gets updated.
    uint256 lastUpdatedQuote; // UNIX epoch of the last time when quote price gets updated.
}
```

Вместо этого `getReferenceDataBulk` принимает два списка — один для токенов `base`, а другой — `quotes`. После этого он аналогичным образом запрашивает цену для каждой пары база/предложение для каждого индекса и выводит массив структур `ReferenceData`.

Например, если мы вызовем `getReferenceDataBulk` с помощью `['BTC','BTC','ETH']` и `['USD','ETH','BNB']`, возвращаемый массив`ReferenceData` будет содержать информацию о парах:

- `BTC/USD`
- `BTC/ETH`
- `ETH/BNB`


#### Адреса контрактов {#contract-addresses}

| Блокчейн | Адрес контракта |
| -------------------- | :------------------------------------------: |
| Polygon (тестовая сеть) | `0x56e2898e0ceff0d1222827759b56b28ad812f92f` |


####  Пример использования {#example-usage}

Этот [контракт](https://gist.github.com/tansawit/a66d460d4e896aa94a0790df299251db) демонстрирует пример использования контракта Band `StdReference` и функции `getReferenceData`.


### BandChain.JS {#bandchain-js}

Библиотека помощника нода Band [`bandchain.js`](https://www.npmjs.com/package/@bandprotocol/bandchain.js) также поддерживает похожую функцию `getReferenceData`. Эта функция принимает один аргумент, а именно список пар токенов для запроса результата. Затем она возвращает список соответствующих курсовых значений.


####  Пример использования {#example-usage-1}

В приведенном ниже коде показан пример использования функции

```javascript=
const { Client } = require('@bandprotocol/bandchain.js');

// BandChain's REST Endpoint
const endpoint = 'https://rpc.bandchain.org';
const client = new Client(endpoint);

// This example demonstrates how to query price data from
// Band's standard dataset
async function exampleGetReferenceData() {
  const rate = await client.getReferenceData(['BTC/ETH','BAND/EUR']);
  return rate;
}

(async () => {
  console.log(await exampleGetReferenceData());
})();

```

Соответствующий результат будет похож на

```bash
$ node index.js
[
    {
        pair: 'BTC/ETH',
        rate: 30.998744363906173,
        updatedAt: { base: 1615866954, quote: 1615866954 },
        requestID: { base: 2206590, quote: 2206590 }
    },
    {
        pair: 'BAND/EUR',
        rate: 10.566138918332376,
        updatedAt: { base: 1615866845, quote: 1615866911 },
        requestID: { base: 2206539, quote: 2206572 }
    }
]
```

Для каждой пары будет возвращена следующая информация:

- `pair`: текстовая строка пары символов база/предложение
- `rate`: получающийся курс данной пары
- `updated`: временная метка последнего обновления символов базы и предложения в BandChain. Для `USD`это будет текущая временная метка
- `rawRate`: этот объект состоит из двух частей.
  - `value` — это `BigInt` значение фактического курса, умноженное на `10^decimals`
  - `decimals` в этом случае является экспонентом, на который умножается `rate` для получения `rawRate`
