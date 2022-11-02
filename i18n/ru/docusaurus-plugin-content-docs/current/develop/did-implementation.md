---
id: did-implementation
title: Реализация Polygon DID
sidebar_label: Identity
description: Узнайте о реализации DID на Polygon
keywords:
  - docs
  - polygon
  - matic
  - DID
  - identity
image: https://matic.network/banners/matic-network-16x9.png
slug: did-implementation/getting-started
---

Это руководство по начальным действиям для пользователей, которые хотят использовать пакеты реализаций, выпущенные командой Polygon, для генерации и публикации Polygon DID в реестре Polygon.

Реализация метода Polygon DID включает 3 пакета, а именно polygon-did-registrar, polygon-did-resolver и polygon-did-registry-contract. Пользователь, желающий включить эти функциональные возможности, чтобы либо регистрировать, либо считывать DID в сети Polygon или из нее, может использовать приведенное ниже руководство.

DID (децентрализованный идентификатор) — это, по сути, уникальный идентификатор, созданный без участия центрального органа.  DID в контексте проверяемых учетных данных используется для подписания документов, тем самым способствуя подтверждению принадлежности документа пользователю в случае необходимости.

## Метод Polygon DID {#polygon-did-method}

Определение метода Polygon DID соответствует спецификациям и стандартам DID-Core. DID URI состоит из трех компонентов, разделенных двоеточиями. Это схема, за которой следует имя метода, а в конце идет метод-специфический идентификатор. Для Polygon URI имеет вид
```
did:polygon:<Ethereum address>
```
Здесь схема — это «did», имя метода — «polygon», а метод-специфическим идентификатором является адрес ethereum.

## Реализация Polygon DID {#polygon-did-implementation}

Polygon DID можно реализовать с помощью двух пакетов. Пользователь может импортировать соответствующие библиотеки npm и использовать их для включения методологий Polygon DID в соответствующие приложения. Подробная информация о реализации представлена в следующем разделе.

## Создание DID {#create-did}

Для начала необходимо создать DID. Создание в случае Polygon DID — это инкапсуляция двух шагов, когда пользователю сначала нужно сгенерировать DID uri для себя, а затем зарегистрировать его в реестре Polygon.

### Шаг 1 — Создание DID {#step-1-create-did}

Чтобы создать в вашем проекте Polygon DID URI, необходимо сначала установить
```
npm i @ayanworks/polygon-did-registrar --save
```
После завершения установки пользователь может использовать его следующим образом
```
import { createDID } from "polygon-did-registrar";
```
Функция createdDID помогает пользователю сгенерировать DID URI. При создании DID возможны два сценария.

1) Пользователь уже владеет кошельком и хочет сгенерировать DID, соответствующий этому же кошельку.
```
const {address, publicKey58, privateKey, DID} = await createDID(network, privateKey);
```
2) Если пользователь не имеет кошелька и хочет сгенерировать кошелек, он может использовать
```
const {address, publicKey58, privateKey, DID} = await createDID(network);
```
Сетевой параметр в обоих случаях указывает на то, где пользователь хочет создать DID: на тестовой сети Polygon или на основной сети Polygon.

Образец входного значения
```
network :"testnet | mainnet"
privateKey? : "0x....."
```
Таким образом, в конце шага 1 будет сгенерирован DID URI.
```
DID mainnet: did:polygon:0x...
DID testnet: did:polygon:testnet:0x...
```

### Шаг 2 — Регистрация DID {#step-2-register-did}

Чтобы зарегистрировать DID URI и соответствующий документ DID в реестре, пользователю сначала необходимо использовать `polygon-did-registrar` следующим образом
```
import { registerDID } from "polygon-did-registrar";
```
В качестве предварительного условия для регистрации DID пользователю необходимо убедиться, что в кошельке, соответствующем DID, имеется необходимое количество токенов.
 Когда в кошельке будет иметься требуемый остаток токенов, можно будет вызвать функцию registerDID, как описано ниже
```
const txHash = await registerDID(did, privateKey, url?, contractAddress?);
```
Параметры `did` и `privateKey` являются обязательными, а вот вводить `url` и `contractAddress` не обязательно.
 Если пользователь не введет два последних параметра, библиотека возьмет из DID URI конфигурации сети со значениями параметров по умолчанию.

Если все параметры соответствуют спецификациям и всё введено в надлежащем порядке, то функция registerDID возвращает хэш транзакции, а в противном случае возвращается соответствующая ошибка.

Итак, вы успешно выполнили задачу регистрации DID в сети Polygon.

## Решение DID {#resolve-did}

Для начала установите следующие библиотеки.
```
npm i @ayanworks/polygon-did-resolver --save
```
и
```
npm i did-resolver --save
```

Чтобы прочитать документ DID, зарегистрированный в реестре, любой пользователь с DID polygon URI может сначала импортировать в свой проект
```
import * as didResolvers from "did-resolver";
import * as didPolygon from '@ayanworks/polygon-did-resolver';
```
после импорта пакетов можно извлечь документ DID с помощью
```
const myResolver = didPolygon.getResolver()
const resolver = new DIDResolver(myResolver)

const didResolutionResult = this.resolver.resolve(did)
```
где объект didResolutionResult имеет следующий вид
```
didResolutionResult:
{
    didDocument,
    didDocumentMetadata,
    didResolutionMetadata
}
```

Следует отметить, что пользователь не будет нести расходы на газ, пытаясь решить DID.

## Обновление документа DID {#update-did-document}

Чтобы инкапсулировать проект с возможностью обновления документа DID, пользователю необходимо сначала использовать `polygon-did-registrar` следующим образом
```
import { updateDidDoc } from "polygon-did-registrar";
```
Затем нужно просто вызвать функцию
```
const txHash = await updateDidDoc(did, didDoc, privateKey, url?, contractAddress?);
```
Следует отметить, что отправить заявку на обновление документа DID может только владелец DID.

В данном случае приватный ключ должен также хранить некоторое количество соответствующих токенов Matic.

Если пользователь не предоставит конфигурацию с `url` и `contractAddress`, библиотека возьмет из DID URI конфигурации сети с параметрами по умолчанию.

## Удаление документа DID {#delete-did-document}

С помощью реализации Polygon DID пользователь может также отозвать свой документ DID из реестра.
 Пользователю сначала необходимо использовать `polygon-did-registrar` следующим образом
```
import { deleteDidDoc } from "polygon-did-registrar";
```
Затем использовать
```
const txHash = await deleteDidDoc(did, privateKey, url?, contractAddress?);
```

Среди параметров интересно отметить, что `url` и `contractAddress` являются необязательными параметрами, при этом, если они не будут предоставлены пользователем, функцией будет выбрана конфигурация по умолчанию на основании DID URI.

Важно, чтобы приватный ключ хранил необходимые токены Matic в соответствии с конфигурацией сети в DID, иначе транзакция даст сбой.


## Внесение изменений в репозиторий {#contributing-to-the-repository}

Используйте стандартный рабочий процесс с заявками на создание параллельного ответвления (fork), создание собственной ветви (branch) и включение кода (pull), чтобы предложить изменения в репозиторий. Сделайте имена ветвей информативными, например включив в них номер выпуска или ошибки.

### Репозитории Github {#github-repositories}

```
https://github.com/ayanworks/polygon-did-registrar
```

```
https://github.com/ayanworks/polygon-did-resolver
```
