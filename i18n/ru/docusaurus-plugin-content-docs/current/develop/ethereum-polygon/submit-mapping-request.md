---
id: submit-mapping-request
title: Запрос на сопоставление
description:  "Шаги по отправке запроса на сопоставление."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

import useBaseUrl from '@docusaurus/useBaseUrl';

Сопоставление необходимо для перевода ваших активов между Ethereum и Polygon. Мы предлагаем два моста для выполнения этой задачи. Более подробную информацию о мостах можно найти [здесь](/docs/develop/ethereum-polygon/getting-started).

### Шаги по отправке запроса на сопоставление {#steps-to-submit-a-mapping-request}

Запрос по сопоставление необходимо отправлять через [https://mapper.polygon.technology/](https://mapper.polygon.technology/). Вы можете нажать кнопку «Сопоставить новый токен» в правом верхнем углу для создания нового запроса на сопоставление.

<img src={useBaseUrl("img/token-mapping/mapping-tool.png")} />


- Тип [моста](/docs/develop/ethereum-polygon/getting-started) необходимо выбрать из выпадающего списка **«Выбрать тип сопоставления»**.
- Тип токена может выбрать посредством переключения между тремя вкладками, помеченными «ERC20», «ERC721» и «ERC1155». Для сопоставления любого другого стандарта токенов вы можете связаться с командой Polygon в [Discord](https://discord.com/invite/0xPolygon) или создать квитанцию [здесь](https://support.polygon.technology/support/home) и сохранить «Сопоставление токенов» в названии квитанции.
- Опция **«Выбрать сеть»** позволит вам выбрать сеть, в которой вам нужно будет выполнить сопоставление. Для сопоставления mainnet вы можете выбрать опцию **Ethereum - Polygon Mainnet**, а для сопоставления тестовой сети — опцию **тестовая сеть Goerli - Mumbai**.
- Введите адрес токена Ethereum/Goerli в поле **«Адрес токена Ethereum»**. Убедитесь, что код контракта токена проверяется в проводниках блокчейна [Ethereum](https://etherscan.io/)/[Goerli](https://goerli.etherscan.io/).
- Если вам потребуется стандартный дочерний токен ERC20/ERC721/ERC1155, вы можете оставить поле **«Адрес токена Polygon»** пустым. Однако, если вам потребуется пользовательский дочерний токен (стандартные функции ERC + пользовательские функции), вы сможете следовать этому [руководству](/docs/develop/ethereum-polygon/pos/mapping-assets) для создания пользовательского дочернего токена. Когда вы развернете пользовательский дочерний токен, вы сможете указать адрес контракта в поле **«Адрес токена Polygon»**. Убедитесь, что вы также проверяете код контракта дочернего токена в проводнике [Polygon](https://polygonscan.com/)/[Mumbai](https://mumbai.polygonscan.com/)
- Если корневой токен проверен, поля **name**, **symbol** and **decimals** заполняются автоматически, и их нельзя редактировать.
- Вы можете выбрать варианты токена **«Polygon Mintable»** или **«Non Polygon Mintable»** из выпадающего списка. Более подробную информацию о поддерживающих минтинг токенах Polygon Mintable можно найти [здесь](/docs/develop/ethereum-polygon/mintable-assets).
- Для связи необходимо обязательно указать ваш адрес электронной почты.

В случае сопоставления пользовательского дочернего токена вам нужно заполнить определенный чеклист, прежде чем вы сможете отправить заявку на сопоставление. Токены, которые уже существуют в Ethereum, и которые необходимо переместить в цепочку Polygon chain, рассматриваются как токены типа Non Polygon-Mintable, не поддерживающие минтинг. Токены, для которых выполняется минтинг в Polygon, а затем перенос в Ethereum, называются токенами Polygon Mintable (поддерживающие минтинг токены Polygon). Давайте посмотрим чеклист для обоих этих типов токенов

### Сопоставление чеклиста {#mapping-checklist}

**Non Polygon-Mintable**

1. Контракт дочернего токена имеет функции депозита и вывода. (контракт образца шаблона - [ERC20](https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildERC20.sol#L1492-#L1508), [ERC721](https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildERC721.sol#L2157-#L2238), [ERC1155](https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildERC1155.sol#L1784-#L1818))
2. Право вызова функции депозита имеет только адрес ChildChainManagerProxy. (ChildChainManagerProxy - в [Mumbai](https://mumbai.polygonscan.com/address/0xb5505a6d998549090530911180f38aC5130101c6/transactions) , в [Polygon Mainnet](https://polygonscan.com/address/0xA6FA4fB5f76172d178d61B04b0ecd319C5d1C0aa/) )
3. Функция минтинга является внутренней функцией (ее вызывает функция депозита внутри сети )

**Polygon Mintable ( руководство -** [https://docs.polygon.technology/docs/develop/ethereum-polygon/mintable-assets](https://docs.polygon.technology/docs/develop/ethereum-polygon/mintable-assets) )

1. Функция депозита и вывода присутствует в контракте дочернего токена. (контракт образца шаблона - [ERC20](https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildMintableERC20.sol#L1492-#L1519), [ERC721](https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildMintableERC721.sol#L2160-#L2275), [ERC1155](https://github.com/maticnetwork/pos-portal/blob/master/flat/ChildMintableERC1155.sol#L1784-#L1851))
2. Право вызова функции депозита имеет только адрес ChildChainManagerProxy. (ChildChainManagerProxy - в [Mumbai](https://mumbai.polygonscan.com/address/0xb5505a6d998549090530911180f38aC5130101c6/transactions) , в [Polygon Mainnet](https://polygonscan.com/address/0xA6FA4fB5f76172d178d61B04b0ecd319C5d1C0aa/) )
3. Контракт корневой цепочки является стандартным контрактом [ERC20](https://github.com/maticnetwork/pos-portal/blob/master/flat/DummyMintableERC20.sol#L1481)/[ERC721](https://github.com/maticnetwork/pos-portal/blob/master/flat/DummyMintableERC721.sol#L2169)/[ERC1155](https://github.com/maticnetwork/pos-portal/blob/master/flat/DummyMintableERC1155.sol#L1785)
4. Функцию минтинга в корневом контракте может вызывать только соответствующий токен с именем PredicateProxyAddress (адреса PredicateProxy для каждого типа токена можно найти [здесь](/docs/develop/ethereum-polygon/mintable-assets#contract-to-be-deployed-on-ethereum).
