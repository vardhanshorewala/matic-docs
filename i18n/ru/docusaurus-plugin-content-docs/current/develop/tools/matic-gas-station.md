---
id: polygon-gas-station
title: Газовая станция Polygon
sidebar_label: Polygon Gas Station
description:  "Рекомендация по цене на газ."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

_Polygon Gas Station_ (газовая станция Polygon) создана, чтобы помогать разработчикам децентрализованных приложений, предоставляя им рекомендации по ценам на газ, чтобы они могли использовать их перед отправкой транзакций в сеть _Polygon_.

## происхождение {#origin}

Мы в _Polygon_ получили от разработчиков децентрализованных приложений запрос на создание сервиса рекомендации цен на газ. Поэтому мы создали такой сервис, взяв в качестве источника вдохновения _Eth Gas Station_.

## доступность {#availability}

Решение _Polygon Gas Station_ развернуто в тестовой сети Polygon Mumbai и в сети Polygon Mainnet, где оно анализирует последние 500 транзакций и дает рекомендацию по цене на газ.

## использование {#usage}

<TabItem value="mumbai"><Tabs
defaultValue="mainnet"
values={[
{ label: 'Polygon-Mainnet', value: 'mainnet', },
{ label: 'Mumbai-Testnet', value: 'mumbai', },
]
}>


# Mumbai - тестовая сеть {#mumbai-testnet}

Чтобы получить рекомендации по ценам на газ от этого оракула, отправьте запрос GET на [https://gasstation-mumbai.matic.today/v2](https://gasstation-mumbai.matic.today/v2)

### cURL {#curl}

```bash
curl https://gasstation-mumbai.matic.today/v2
```

### JavaScript {#javascript}

```javascript
fetch('https://gasstation-mumbai.matic.today/v2')
  .then(response => response.json())
  .then(json => console.log(json))
```

### Python {#python}

```python
import requests
requests.get('https://gasstation-mumbai.matic.today/v2').json()
```

</TabItem>
<TabItem value="mainnet">

# Polygon-Mainnet {#polygon-mainnet}

Чтобы получить рекомендации по ценам на газ от этого оракула, отправьте запрос GET в Polygon Gas Station V2 для получения приблизительной комиссии за газ. Конечная станция Polygon Gas Station V2: [https://gasstation-mainnet.matic.network/v2](https://gasstation-mainnet.matic.network/v2)

### cURL {#curl-1}

```bash
curl https://gasstation-mainnet.matic.network/v2
```

### JavaScript {#javascript-1}

```javascript
fetch('https://gasstation-mainnet.matic.network/v2')
  .then(response => response.json())
  .then(json => console.log(json))
```

### Python {#python-1}

```python
import requests
requests.get('https://gasstation-mainnet.matic.network/v2').json()
```

</TabItem>
</Tabs>

## интерпретация {#interpretation}

- Пример ответа JSON будет выглядеть следующим образом:

```json
{
  "safeLow": {
    "maxPriorityFee":30.7611840636,
    "maxFee":30.7611840796
    },
  "standard": {
    "maxPriorityFee":32.146027800733336,
    "maxFee":32.14602781673334
    },
  "fast": {
    "maxPriorityFee":33.284344224133335,
    "maxFee":33.284344240133336
    },
  "estimatedBaseFee":1.6e-8,
  "blockTime":6,
  "blockNumber":24962816
}
```

- {'safelow', 'standard', 'fast', 'estimatedBaseFee'} — цены на газ в GWei, вы можете использовать их перед отправкой транзакции в Polygon в зависимости от потребностей
- _'blockNumber'_ сообщает о том, какой блок был добыт последним при подаче рекомендации
- _'blockTime'_ среднее время блока в сети в секундах
