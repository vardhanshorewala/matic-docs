---
id: custom-restrictions
title: Пользовательские ограничения (ERC20/ERC721)
# sidebar_label: Adding
description: "Как добавить пользовательские ограничения в токены ERC20."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

**Как добавить пользовательские ограничения в токен ERC20 на Polygon**

Токены ERC20 на Polygon chain представляют собой стандартные контракты, автоматически развертываемые контрактами на корневой цепочке Plasma во время регистрации нового токена ERC20 на Polygon. Их нельзя модифицировать, чтобы обеспечить сопоставление всех переходов из одного состояния в другое с доказательствами мошенничества в контрактах на корневой цепочке, благодаря чему эти контракты, по сути, способны обеспечивать такую же безопасность, как сеть Ethereum.

Однако в реальных условиях владельцу токена ERC20 может понадобиться добавить в контракт пользовательские ограничения, особенно в отношении функции `transfer`.

**TL;DR**

- Реализуйте функцию `beforeTransfer` в реализации интерфейса IParentToken (https://github.com/maticnetwork/contracts/blob/master/contracts/child/misc/IParentToken.sol) и разверните на Polygon chain.

**На этой странице подробно описывается процесс добавления пользовательских ограничений трансфера в токен ERC20:**

- При добавлении токена ERC20 в Polygon (т. е. при его сопоставлении с Polygon) функция в корневом контракте(link) ожидает
    - адрес контракта токена корневой цепочки,
    - метаданные о токене и
    - адрес владельца

    При этом также автоматически развертывается соответствующий стандартный контракт токена ERC20 на Polygon chain, сопоставляемый с корневым контрактом токена. Кроме того, необходимо предоставить адрес владельца, что в дальнейшем позволяет санкционировать развертывание дополнительного контракта, с помощью которого владелец токена ERC20 может добавить ограничения трансфера в контракт в Polygon chain.

- Чтобы определить пользовательскую логику в стандартной функции `transfer` в токене ERC20, необходимо реализовать интерфейс `IParentToken`; см. ссылку здесь - https://github.com/maticnetwork/contracts/blob/master/contracts/child/misc/IParentToken.sol

- Функция перехвата `beforeTransfer` — это тот элемент, где может исполняться пользовательская логика перед каждым трансфером.
- Реализованный контракт должен
    - последовать этому интерфейсу,
    - вернуть значение `bool` и,
    - в случае контрактов ERC20, в нем не должно быть операторов `require`, а вместо этого он должен вернуть `false`
- Вот пример реализации контракта `IParentToken`:

<script src="https://gist.github.com/anurag-arjun/c7382e2abaf0822e6ec7e988eb46c92e.js"></script>

- Только адрес владельца, указанный во время регистрации токена, будет способен добавить/обновить адрес родительского контракта (реализация `IParentToken` с перехватом `beforeTransfer`) в стандартном контракте ChildToken на Polygon
- К вашему сведению, вы можете получить адрес стандартного контракта ChildToken (автоматически развернутого корневыми контрактами на Polygon), запросив сопоставление `rootToChildToken` в реестровом контракте (https://github.com/maticnetwork/contracts/blob/master/contracts/common/Registry.sol)

    ```solidity
    contract Registry is Governable {
    mapping(bytes32 => address) contractMap;
    mapping(address => address) public rootToChildToken;
    mapping(address => address) public childToRootToken;
    ...
    }
    ```

- Владение реализованным таким образом родительским контрактом (реализация `IParentToken` с перехватом `beforeTransfer`) может быть передано путем вызова функции `setParent` в контракте ChildERC20 на Polygon chain - см. https://github.com/maticnetwork/contracts/blob/master/contracts/child/ChildERC20.sol

    ```js
    function setParent(address _parent) public isParentOwner {
        require(_parent != address(0x0));
        parent = _parent;
    }
    ```
