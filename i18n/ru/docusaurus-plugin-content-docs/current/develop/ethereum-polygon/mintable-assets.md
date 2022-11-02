---
id: mintable-assets
title: Активы Polygon с возможностью произвольного минтинга
description: "Создайте актив на Polygon"
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

## Что такое токены Polygon с возможностью произвольного минтинга? {#what-are-polygon-mintable-tokens}

Активы можно передавать в Ethereum и Polygon chain, а также из них и между ними, с помощью моста PoS. Эти активы включают ERC20, ERC721, ERC1155 и многие другие стандарты токенов. Большинство активов уже существуют в цепочке Ethereum. Однако в Polygon chain также можно создавать новые активы и перемещать их обратно в цепочку Ethereum по мере необходимости. Это может сэкономить много газа и времени, которые тратятся на минтинг токенов в Ethereum. Создание активов в Polygon chain является гораздо более простым и рекомендуемым подходом. Эти активы можно перемещать в цепочку Ethereum в случае необходимости. Активы такого типа называются активами Polygon с возможностью произвольного минтинга.

Что касается токенов Polygon с возможностью произвольного минтинга, то активы создаются на Polygon. Если актив, минтинг которого выполнен на Polygon, необходимо переместить в Ethereum, этот актив необходимо сначала сжечь, а затем необходимо отправить доказательство этой транзакции сжигания в цепочку Ethereum. Контракт RootChainManager вызывает специальный контракт predicate на внутреннем уровне. Этот контракт predicate напрямую вызывает функцию минтинга контракта актива на Ethereum, при этом токены минтуются на адрес пользователя. Этот специальный predicate называется MintableAssetPredicate.

## Какие требования должны быть удовлетворены? {#what-are-the-requirements-to-be-satisfied}

Существует ряд условий, которые должны строго соблюдаться, когда нам необходимо создать актив на Polygon, а затем переместить его обратно в Ethereum.

### Контракт, подлежащий развертыванию в Polygon chain {#contract-to-be-deployed-on-polygon-chain}
Вы можете либо развернуть

- Контракт токена с возможностью произвольного минтинга в Polygon chain, либо
- Отправить заявку на сопоставление, при этом контракт токена с возможностью произвольного минтинга может быть автоматически развернут для вас в Polygon chain посредством инструмента Mapper. Вам нужно просто отправить заявку на сопоставление на сайте [https://mapper.polygon.technology/](https://mapper.polygon.technology/) и оставить в этой форме поле дочернего контракта пустым. Кроме того, не забудьте выбрать вариант Mintable в форме.

Перейдите по этой [ссылке](/docs/develop/ethereum-polygon/submit-mapping-request), чтобы узнать, как создать новую заявку на сопоставление.

- Если вы хотите развернуть контракт самостоятельно, то дочерний контракт должен выглядеть следующим образом. Вы можете по своему усмотрению внести собственные изменения в этот контракт, только убедитесь в наличии функций `deposit`, `withdraw` и `mint`.

    - ChildMintableERC20 -  [https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildMintableERC20.sol](https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildMintableERC20.sol)
    - ChildMintableERC721 - [https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildMintableERC721.sol](https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildMintableERC721.sol)
    - ChildMintableERC1155 - [https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildMintableERC1155.sol](https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildMintableERC1155.sol)

- Что особенно важно, дочернему контракту менеджера на Polygon должна быть отведена роль депонента в контракте актива, развернутом на Polygon. Только этот адрес прокси дочернего менеджера должен обладать правами депонирования токенов на Polygon.
- Обязательно проверьте оба контракта на Polygonscan и Etherscan соответственно, прежде чем отправлять заявку на сопоставление.

Адреса дочернего контракта менеджера:

```
Mumbai: 0xb5505a6d998549090530911180f38aC5130101c6
Mainnet: 0xA6FA4fB5f76172d178d61B04b0ecd319C5d1C0aa
```

Обязательно укажите адрес контракта развернутого дочернего токена при отправке заявки на сопоставление.

> Отметим, что контракт Ethereum необходимо развернуть, как показано на следующем шаге (впрочем, на Ethereum никакого минтинга осуществлять не нужно). Это требуется для того, чтобы можно было при необходимости вывести токены в Ethereum.

### Контракт, подлежащий развертыванию на Ethereum {#contract-to-be-deployed-on-ethereum}

- Контракт токена необходимо развернуть в цепочке Ethereum, при этом он должен выглядеть следующим образом.
    - MintableERC20 -  [https://github.com/maticnetwork/pos-portal/blob/master/flat/DummyMintableERC20.sol](https://github.com/maticnetwork/pos-portal/blob/master/flat/DummyMintableERC20.sol)
    - MintableERC721 - [https://github.com/maticnetwork/pos-portal/blob/master/flat/DummyMintableERC721.sol](https://github.com/maticnetwork/pos-portal/blob/master/flat/DummyMintableERC721.sol)
    - MintableERC1155 - [https://github.com/maticnetwork/pos-portal/blob/master/flat/DummyMintableERC1155.sol](https://github.com/maticnetwork/pos-portal/blob/master/flat/DummyMintableERC1155.sol)

- Что особенно важно, контракт `MintableAssetProxy`, контракту, развернутому на Ethereum, должна быть отведена роль минтера в контракте актива, развернутом на Ethereum. Только этот прокси-адрес predicate должен обладать правами минтинга токенов на Ethereum.

- Эту роль можно предоставить, вызвав функцию grantRole() в контрактах токенов в корневой цепочке. Первым параметром является значение константы PREDICATE_ROLE, равное **0x12ff340d0cd9c652c747ca35727e68c547d0f0bfa7758d2e77f75acef481b4f2**, а вторым параметром является прокси-адрес predicate токена, который приведен ниже,


    ```jsx
    Ethereum Mainnet
    "MintableERC20PredicateProxy"  : "0x9923263fA127b3d1484cFD649df8f1831c2A74e4",
    "MintableERC721PredicateProxy" : "0x932532aA4c0174b8453839A6E44eE09Cc615F2b7",
    "MintableERC1155PredicateProxy": "0x2d641867411650cd05dB93B59964536b1ED5b1B7",
    ```

    ```jsx
    Goerli Testnet
    "MintableERC20PredicateProxy"  : "0x37c3bfC05d5ebF9EBb3FF80ce0bd0133Bf221BC8",
    "MintableERC721PredicateProxy" : "0x56E14C4C1748a818a5564D33cF774c59EB3eDF59",
    "MintableERC1155PredicateProxy": "0x72d6066F486bd0052eefB9114B66ae40e0A6031a",
    ```

