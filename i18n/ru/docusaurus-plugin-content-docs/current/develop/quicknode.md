---
id: quicknode
title: Развертывание смарт-контракта на Polygon с использованием Brownie и QuickNode
sidebar_label: Using QuickNode
description:  Развертывание смарт-контрактов с использованием Brownie и Quicknode.
keywords:
  - docs
  - matic
  - quicknode
  - polygon
  - python
  - web3.py
  - contract
image: https://matic.network/banners/matic-network-16x9.png
---

## Обзор {#overview}

Python — один из самых универсальных языков программирования, который используется во всех технических областях, от создания тестовых моделей для исследований до разработки решений для тяжелой промышленности. Это руководство подробно расскажет вам о процессе развертывания смарт-контрактов с помощью инструмента на базе Python под названием [Brownie](https://eth-brownie.readthedocs.io/en/latest/index.html#brownie), который используется для написания и развертывания смарт-контрактов, а также с помощью [QuickNode](https://www.quicknode.com/chains/matic?utm_source=polygon_docs&utm_campaign=ploygon_docs_contract_guide).

### Предварительные условия {#prerequisites}

- Python3 установлен.

- Нод Polygon.

- Текстовый редактор.

- Командная строка.

## Что вы узнаете {#what-you-will-learn}

- Используйте инфраструктуру Brownie для разработки и тестирования смарт-контракта
- Используйте ноды тестовой сети Quicknode для Polygon.

## Что вы сделаете {#what-you-will-do}

1. Настройте Brownie
2. Получите доступ к тестовым нодам Quicknode
3. Скопмилируйте и разверните смарт-контракт
4. Проверьте данные развернутого контракта.

## Что такое Brownie? {#what-is-brownie}
-----------------

Для развертывания смарт-контрактов чаще всего используются библиотеки на базе JavaScript, такие как [web3.js](https://web3js.readthedocs.io/), [ethers.js](https://docs.ethers.io/), [Truffle](https://www.trufflesuite.com/docs/truffle/) и [Hardhat](https://hardhat.org/). Python — универсальный и широко используемый язык программирования, который также можно использовать для смарт-контрактов и разработки web3; [web3.py](https://web3py.readthedocs.io/en/stable/) — привлекательная библиотека Python, выполняющая задачи web3. Инфраструктура Brownie построена на базе web3.py.

[Brownie](https://eth-brownie.readthedocs.io/en/latest/index.html#brownie) — это инфраструктура на базе Python, предназначенная для разработки и тестирования смарт-контрактов. Brownie поддерживает контракты Solidity и Vyper и даже предоставляет возможности тестирования контрактов через [pytest](https://github.com/pytest-dev/pytest).

Чтобы продемонстрировать процесс написания и развертывания смарт-контракта с помощью Brownie, мы используем проекты шаблонов [Brownie-mixes](https://github.com/brownie-mix). В частности, мы используем шаблон реализации ERC-20 [token mix](https://github.com/brownie-mix/token-mix).

## Шаг 1: Установка зависимостей {#step-1-installing-dependencies}
-----------------------

Система Brownie построена на базе python3, и поэтому вам нужно установить его для работы с Brownie. Давайте проверим, установлен ли python3 в нашей системе. Для этого введите в строку терминала или командную строку следующее:

```
python3 -V
```

В результате выведется установленная версия python3. Если python3 не установлен, загрузите и установите его с официального сайта [python](https://www.python.org/downloads/).

Давайте создадим каталог проекта, прежде чем устанавливать Brownie, и сделаем этот каталог проекта нашим текущим рабочим каталогом:

```
mkdir brownieDemo
cd brownieDemo
```

После установки python3 мы установим brownie с помощь pip, диспетчера пакетов Python. Pip имеет функцию, аналогичную функции npm для JavaScript. Введите в терминал или командную строку следующее:

```
pip3 install eth-brownie
```
***Если установку не удастся выполнить, вы можете использовать следующую команду: ***

```
sudo pip3 install eth-brownie
```

Чтобы проверить правильность установки Brownie, введите brownie в строке терминала / командной строке, после чего появится следующий вывод:

![img](/img/quicknode/brownie-commands.png)

Чтобы получить token mix, просто введите следующее в строку терминала/командную строку:

```
brownie bake token
```

При этом будет создан новый токен каталога в нашем каталоге brownieDemo.


### Файловая структура {#file-structure}
Прежде всего, давайте перейдем в каталог _token_:

```
cd token
```

Теперь откройте каталог _token_ в вашем текстовом редакторе. В папке ***contracts/*** вы найдете файл **Token.sol**, который является нашим основным контрактом. Вы можете писать собственные контракты или изменять этот. В папке ***scripts/*** вы найдете скрипт ***token.py*** на python, который будет использоваться для развертывания контракта, и необходимые изменения на базе контрактов.

![img](/img/quicknode/token-sol.png)

Это контракт ERC-20.  Вы можете узнать больше о стандартах и контрактах ERC-20 в этом [руководстве ERC-20](https://www.quicknode.com/guides/solidity/how-to-create-and-deploy-an-erc20-token).

## Шаг 2: Загрузка вашего нода Polygon {#step-2-booting-your-polygon-node}
-------------------------

QuickNode имеет глобальную сеть узлов тестовой сети Polygon Mainnet и Mumbai, которые также обслуживают [бесплатный публичный Polygon RPC](https://docs.polygon.technology/docs/develop/network-details/network/#:~:text=https%3A//rpc%2Dmainnet.matic.quiknode.pro), однако если у вас появляется ограничения скорости, вы можете подписаться на [бесплатный пробный узел от QuickNode](https://www.quicknode.com/chains/matic?utm_source=polygon_docs&utm_campaign=ploygon_docs_contract_guide).

![img](/img/quicknode/http_URL.png)

Скопируйте URL-адрес HTTP, который потребуется на следующем шаге.

## Шаг 3: Настройка сети и аккаунта {#step-3-network-and-account-setup}
--------------------------------------

Нам потребуется настроить конечную точку QuickNode с Brownie. Для этого введите в строку терминала или командную строку следующее:

```
brownie networks add Ethereum matic_mumbai host=YOUR_QUICKNODE_URL chainid=3
```

Замените **YOUR_QUICKNODE_URL** на URL-адрес Mumbai, полученный на предыдущем шаге.

В приведенной выше команде `Ethereum` — это имя среды, а `matic_mumbai` — специальное имя сети; вы можете присвоить своей пользовательской сети любое имя.

Далее нам нужно создать новый кошелек с помощью Brownie, и для этого вам следует ввести в строку терминала или командную строку следующее:
 Вам будет предложено задать пароль для вашей учетной записи.

```
brownie accounts generate testac
```

При этом будет сгенерирована учетная запись с мнемонической фразой. Сохраните ее в автономном режиме. testac — это имя нашего аккаунта. Вы можете выбрать любое имя, которое вам понравится.

![img](/img/quicknode/new-account.png)

:::note

Мнемонические фразы можно использовать для восстановления аккаунта или для импорта аккаунта в другие [кошельки без ответственного хранения](https://www.quicknode.com/guides/web3-sdks/how-to-do-a-non-custodial-transaction-with-quicknode). Аккаунт, который вы видите на иллюстрации выше, был только что создан специально для этого руководства.

:::

Скопируйте адрес аккаунта, чтобы мы могли получить немного тестовых ETH, которые потребуются для развертывания нашего контракта.

## Шаг 4: Получение тестовых MATIC {#step-4-getting-test-matic}
------------------

Нам потребуется несколько тестовых MATIC, чтобы заплатить комиссию за газ для развертывания смарт-контракта.

Скопируйте адрес аккаунта, который мы сгенерировали на предыдущем шаге, вставьте его в поле адреса [Polygon faucet](https://faucet.polygon.technology/) и нажмите «Отправить». faucet отправит вам 0,2 тестовых MATIC.

![img](/img/quicknode/faucet.png)

## Шаг 5: Развертывание нашего контракта {#step-5-deploying-our-contract}
--------------------

Перед развертыванием контракта его следует скомпилировать, используя:

```
brownie compile
```

![img](/img/quicknode/brownie-compile.png)

Теперь откройте в текстовом редакторе **scripts/token.py** и внесите следующие изменения:

```python
#!/usr/bin/python3

from brownie import Token, accounts

def main():

    acct = accounts.load('testac')

    return Token.deploy("Test Token", "TST", 18, 1e21, {'from': acct})
```

Изменения в файле token.py:

Строка 7: Мы добавили эту строку для импорта аккаунта testac, который мы создали ранее и сохранили в переменной **acct**.

Строка 8: В этой строке мы отредактировали часть «'From':», указав нашу переменную аккаунта.

Наконец, мы развернем наш контракт:

```
brownie run token.py --network matic_mumbai
```

matic_mumbai — это имя пользовательской сети, которую мы создали ранее. В диалоге у вас будет запрошен пароль, который мы задали ранее при создании аккаунта. После запуска вышеуказанной команды вам потребуется получить хэш транзакции, и Brownie подождет подтверждения транзакции. После подтверждения транзакции она будет возвращать адрес развертывания нашего контракта в тестовой сети Polygon Mumbai.

![img](/img/quicknode/brownie-run.png)

Вы сможете проверить развернутый контракт, скопировав и вставив адрес контракта в [Polygonscan Mumbai](https://mumbai.polygonscan.com/).

![img](/img/quicknode/polygonscan.png)

## Шаг 6: Тестирование контракта {#step-6-testing-the-contract}

Brownie также предлагает возможности тестирования функций смарт-контрактов. В нем используется инфраструктура `pytest` для удобного генерирования тестов. Дополнительную информацию о написании тестов на Brownie [можно найти в документации](https://eth-brownie.readthedocs.io/en/latest/tests-pytest-intro.html#).

**Вот так развертываются контракты в Polygon с помощью Brownie и QuickNode.**

Как и Polygon, QuickNode всегда применяет подход, ставящий образование во главу угла, предоставляя разработчикам [руководства](https://www.quicknode.com/guides?utm_source=polygon_docs&utm_campaign=ploygon_docs_contract_guide), [документацию](https://www.quicknode.com/docs/polygon?utm_source=polygon_docs&utm_campaign=ploygon_docs_contract_guide), [обучающие видео](https://www.youtube.com/channel/UC3lhedwc0EISreYiYtQ-Gjg/videos) и [сообщество разработчиков #web3](https://discord.gg/DkdgEqE), которые всегда готовы помочь друг другу.

:::tip

Чтобы связаться с командой Quicknode, напишите им или отметьте их в Twitter [@QuickNode](https://twitter.com/QuickNode).

:::
