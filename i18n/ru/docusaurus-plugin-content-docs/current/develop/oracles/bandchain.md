---
id: bandchain
title: BandChain
sidebar_label: Bandchain
description: "Запрос данных из традиционных web-API."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

Протокол Band позволяет запрашивать данные из традиционных web-API и использовать их в блокчейне. Для упрощения запросов оракулов и оплаты разработчики могут отправлять запросы через BandChain (блокчейн на базе cosmos) и использовать данные в децентрализованном приложении через связь между цепочками. Интеграцию данных оракулов можно выполнить за 3 простых шага:

1. **Выбор скриптов оракула**

    Скрипт оракула — это хэш, являющийся уникальынм идентификатором типа данных, запрашиваемого из цепочки Band. Эти скрипты можно найти [**здесь**](https://guanyu-devnet.cosmoscan.io/oracle-scripts). Эти скрипты используются в качестве одного из параметров при отправке запроса оракулу.

2. **Запрос данных из BandChain**

Это можно сделать двумя способами:

- Использование проводника BandChain

    Вы можете нажать на предпочитаемый скрипт оракула, а затем использовать вкладку исполнения для передачи параметров и получения ответа от BandChain. Ответ будет содержать результат и доказательство evm. Это доказательство необходимо скопировать, и оно будет использовано на заключительном шаге. Документация BandChain по запросу оракула с использованием проводника находится [**здесь**](https://docs.bandchain.org/dapp-developers/requesting-data-from-bandchain/requesting-data-via-explorer).

    <img src={useBaseUrl("img/bandchain/executeoracle.png")} />

    Выше приведен пример отправки запроса оракула для получения значений случайных чисел. Значение 100 передается параметру max_range запроса оракула. В качестве ответа мы получаем хэш. При нажатии на хэш мы видим полные детали ответа.

- Использование библиотеки BandChain-Devnet JS

    Вы можете отправить запрос Bandchain напрямую, используя библиотеку bandchain Devnet. При запросе в качестве ответа отправляется **доказательство evm**. Это доказательство можно использовать для заключительного шага интеграции BandChain. Документация BandChain по запросу оракула с использованием библиотеки BandChain-Devnet JS приведена [**здесь**](https://docs.bandchain.org/dapp-developers/requesting-data-from-bandchain/requesting-data-via-js-library). Полезная нагрузка запроса для оракула случайных чисел выглядит следующим образом. Убедитесь, что тело запроса передается в формате application/json.

3. **Использование данных в смарт-контрактах**

  Заключительный шаг заключается в развертывании контракта валидации и сохранении ответов на запрос оракула в переменные состояния контракта подтверждения. После установки этих переменных состояния доступ к ним может выполняться так и тогда, как это требуется децентрализованному приложению. Эти переменные состояния также можно обновлять на новые значения, повторно запрашивая скрипты оракула у децентрализованного приложения. Ниже приведен контракт подтверждения, который сохраняет значение случайного числа, используя скрипт оракула случайных чисел.

  ```jsx
  pragma solidity 0.5.14;
  pragma experimental ABIEncoderV2;

  import "BandChainLib.sol";
  import "IBridge.sol";

  contract SimplePriceDatabase {
    using BandChainLib for bytes;

    bytes32 public codeHash;
    bytes public params;
    IBridge public bridge;

    uint256 public latestPrice;
    uint256 public lastUpdate;

    constructor(
      bytes32 _codeHash ,
      bytes memory _params,
      IBridge _bridge
    ) public {
      codeHash = _codeHash;
      params = _params;
      bridge = _bridge;
    }

    function update(bytes memory _reportPrice) public {
      IBridge.VerifyOracleDataResult memory result = bridge.relayAndVerify(_reportPrice);
      uint64[] memory decodedInfo = result.data.toUint64List();

      require(result.codeHash == codeHash, "INVALID_CODEHASH");
      require(keccak256(result.params) == keccak256(params), "INVALID_PARAMS");
      require(uint256(decodedInfo[1]) > lastUpdate, "TIMESTAMP_MUST_BE_OLDER_THAN_THE_LAST_UPDATE");

      latestPrice = uint256(decodedInfo[0]);
      lastUpdate = uint256(decodedInfo[1]);
    }
  }
  ```

  При развертывании необходимо передать 3 параметра. Первый параметр — codeHash, который представляет собой скрипт хэша оракула. Второй параметр — это объект параметров запроса скрипта оракула. Он передается в байтовом формате.  BandChain предоставляет REST API для конвертации объекта параметра JSON в байтовый формат. Детали информации об API можно найти [**здесь**](https://docs.bandchain.org/references/encoding-params). К полученному от этого API ответа необходимо добавить 0x. Третий параметр — это адрес контракта Bandchain, который уже развернут в сети Polygon. Протокол Band поддерживает тестовую сеть Polygon TestnetV3: 0x3ba819b03fb8d34995f68304946eefa6dcff7cbf.

  Также важно отметить, что контракт подтверждения должен импортировать библиотеку помощника и интерфейс с именами BandChainLib.sol и IBridge.sol соответственно. Их можно найти по следующим ссылкам: библиотека [**Bandchain**](https://docs.bandchain.org/references/bandchainlib-library)   и интерфейс [**IBridge**](https://docs.bandchain.org/references/ibridge-interface).

  После развертывания контракта подтверждения доступ к переменным состояния можно произвести посредством запроса из децентрализованного приложения. Точно так же существует возможность создания нескольких контрактов подтверждения для разных встроенных скриптов оракулов. Интерфейс IBridge имеет метод с именем relayAndVerify, который проверяет значения, которые каждый раз обновляются в контракте подтверждения. Метод обновления в контракте подтверждения включает логику для обновления переменных состояния. Доказательство evm, полученное в результате запроса скрипта оракула, должно быть передано методу обновления. Каждый раз при обновлении значения контракт BandChain, развернутый в Polygon, проверяет данные перед их сохранением в переменной состояния контракта.

  bandChain предоставляет децентрализованную сеть оракулов, которую децентрализованные приложения могут использовать для усиления своей логики смарт-контрактов. Документацию BandChain по развертыванию контракта, сохранению значений и их обновлению можно найти [**здесь**](https://docs.bandchain.org/dapp-developers/requesting-data-from-bandchain/requesting-data-via-js-library).