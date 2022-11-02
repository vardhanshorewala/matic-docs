---
id: client-setup
title: Настройка клиента архивного нода
sidebar_label: Set up an Archive Node Client
description: "Системные требования и настройка клиента."
keywords:
  - erigon
  - archive
  - node
image: https://matic.network/banners/matic-network-16x9.png
---

## Системные требования: {#system-requirements}

### Архивный нод: {#archive-node}

- 16-ядерный процессор
- 64 ГБ ОЗУ
- В основном io1 или выше с не менее, чем 20k+ iops и дисковой структурой на базе raid-0.

### Клиент Erigon: {#erigon-client}

- Для архивного нода в Polygon Mainnet: 5 ТБ.
- Для архивного нода Polygon Mumbai: 1 ТБ.
- SSD или NVMe. Помните, что производительность SSD снижается при приближении к максимальной емкости.
- ОЗУ: >= 16 ГБ, 64-битная архитектура
- Версия Golang >= 1.18, GCC 10+

:::note HDD не рекомендуется

При использовании HDD Erigon всегда остается на N блоков позади конца цепочки, но не упадет назад.

:::

## Настройка клиента Erigon {#erigon-client-setup}

### Как выполнить установку {#how-to-install}
Запустите следующие команды для установки Erigon:

```bash
git clone --recurse-submodules -j8 https://github.com/maticnetwork/erigon.git
cd erigon
git checkout v0.0.2
make erigon
```

При этом должен быть создан двоичный файл в ```./build/bin/erigon```

Используйте тег `v0.0.2` в нашем разветвленном репозитории для получения стабильной версии.

### Как начать {#how-to-start}

Для запуска Erigon запустите

```
erigon --chain=mumbai
```

- Используйте `chain=mumbai` для тестовой сети Mumbai
- Используйте `chain=bor-mainnet` для Mainnet

### Как настроить Erigon {#how-to-configure-erigon}

- Если вы захотите сохранить файлы Erigon не в расположении по умолчанию, используйте `-datadir`


    ```
    erigon --chain=mumbai --datadir=<your_data_dir>
    ```

- Если вы не используете локальный **heimdall**, используйте `-bor.heimdall=<your heimdall url>`. По умолчанию он будет пытаться подключиться к `localhost:1317`.


    ```makefile
    erigon --chain=mumbai --bor.heimdall=<your heimdall url> --datadir=<your_data_dir>
    ```

Например, если вы хотите подключиться к Mumbai, используйте

    - [https://heimdall.api.matic.today](https://heimdall.api.matic.today/)

Для Mainnet:

    - [https://heimdall.api.matic.network](https://tendermint.api.matic.network/)

### Советы для ускорения синхронизации {#tips-for-a-faster-sync}

- Используйте машину с высокими показателями IOPS и большим объемом ОЗУ для более быстрой начальной синхронизации
- Используйте команды ниже для увеличения скорости загрузки/выгрузки снимка:

```makefile
--torrent.upload.rate="512mb" --torrent.download.rate="512mb"
```

:::note

Замените `512` любой пропускной способностью, с которой может справиться ваша машина.

:::

