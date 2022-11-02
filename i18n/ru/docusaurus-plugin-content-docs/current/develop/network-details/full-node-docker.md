---
id: full-node-docker
title: Запуск полного нода с помощью Docker
sidebar_label: Run a full node with Docker
description:  Руководство по запуску полного нода с использованием Docker.
keywords:
  - docs
  - matic
  - docker
  - node
image: https://matic.network/banners/matic-network-16x9.png
---

Команда Polygon распространяет официальные образы Docker, которые можно использовать для запуска нодов в Polygon mainnet. Эти инструкции предназначены для запуска полного нода, но их также можно адаптировать для запуска дозорных нодов и валидаторов.


:::note Снимки

Вы обнаружите, что синхронизация с нуля может занимать очень много времени. Если вы хотите ускорить процесс, вы можете следовать приведенным здесь инструкциям: https://docs.polygon.technology/docs/develop/network-details/snapshot-instructions-heimdall-bor/

Это будут самые актуальные инструкции, но приблизительная процедура приведена в шагах, описанных ниже:
```bash
# stop your containers at this point. Since you're importing a snapshot you don't need to run them anymore
aria2c -x6 -s6 https://matic-blockchain-snapshots.s3-accelerate.amazonaws.com/matic-mainnet/heimdall-snapshot-2022-07-06.tar.gz
tar xzf heimdall-snapshot-2022-07-06.tar.gz -C /mnt/data/heimdall/data/

aria2c -x6 -s6 https://matic-blockchain-snapshots.s3-accelerate.amazonaws.com/matic-mainnet/bor-fullnode-snapshot-2022-07-01.tar.gz
tar xzf bor-fullnode-snapshot-2022-07-01.tar.gz -C /mnt/data/bor/bor/chaindata
# at this point, you can start your containers back up. Pay attention to the logs to make sure everything looks good
```
:::

## Предварительные условия {#prerequisites}
Общая конфигурация для работы полного нода Polygon требует **не менее** 4 процессоров/ядер и 16 ГБ ОЗУ. Для этого руководства мы будем использовать AWS и тип экземпляра `t3.2xlarge`. Приложение может работать на архитектурах x86 и Arm.

Эти инструкции основаны на Docker, поэтому им легко следовать в любой операционной системе, однако в данном случае мы используем в качестве примера Ubuntu.

Для полного нода требуется не менее 1,5 терабайт дискового пространства на SSD-накопителе (или более быстром накопителе).

Для взаимодействия с одноранговыми системами на полном ноде Polygon обычно должны быть открыты порты 30303 и 26656. При настройке брандмауэра или групп безопасности для AWS необходимо убедиться, что эти порты открыты наряду со всеми другими портами, которые вам необходимы для доступа к машине.

TLDR:

- Используйте машину, имеющую не менее 4 ядер и 16 ГБ ОЗУ
- Убедитесь, что у вас имеется не менее 1,5 ТБ свободного пространства на быстром накопителе
- Используйте публичный IP-адрес и откройте порты 30303 и 26656

## Начальная настройка {#initial-setup}
На этом этапе у вас должен быть доступ к оболочке на машине linux с привилегиями root.


![img](/img/full-node-docker/term-access.png)

### Docker {#docker}
Скорее всего, Docker не будет установлен в вашей операционной системе по умолчанию. Следуйте инструкциям для вашего конкретного дистрибутива, которые можно найти здесь: https://docs.docker.com/engine/install/

Мы следуем инструкциям для Ubuntu. Эти шаги описаны ниже, однако ознакомьтесь с официальными инструкциями на случай, если они были обновлены.

```bash
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

```

Сейчас вы должны уже установить Docker. Для проверки вы можете запустить следующую команду:

```bash
sudo docker run hello-world
```

![img](/img/full-node-docker/hello-world.png)

Во многих случаях запускать Docker от имени пользователя `root` неудобно, и поэтому после установки мы выполним приведенные [здесь](https://docs.docker.com/engine/install/linux-postinstall/) шаги, чтобы взаимодействовать с Docker без необходимости работать как пользователь `root`:

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
```

Теперь вы можете выйти из системы, снова войти и запускать команды Docker без `sudo`.

### Настройка дисков {#disk-setup}
Точные шаги на данном этапе могут существенно различаться в зависимости от ваших потребностей. Скорее всего, ваша система представляет собой корневой раздел на одном устройстве, где работает операционная система. Вероятно вы захотите иметь одно или несколько устройств для фактического хранения данных блокчейна. Для целей остальной части этого руководства мы смонтируем это дополнительное устройство здесь: `/mnt/data`.

В этом примере у меня есть устройство с 4 ТБ свободного пространства, расположенное здесь: `/dev/nvme1n1`. Сейчас я смонтирую его, выполнив описанные ниже шаги:

```bash
sudo mkdir /mnt/data
sudo mount /dev/nvme1n1 /mnt/data
```

Мы используем `df -h`, чтобы убедиться, что устройство смонтировано правильно.

![img](/img/full-node-docker/space.png)

Если все выглядит нормально, мы можем создать на смонтированном томе домашние каталоги для Bor и Heimdall.

```bash
sudo mkdir /mnt/data/bor
sudo mkdir /mnt/data/heimdall
```

В зависимости от сценария и операционной системы вы можете захотеть создать запись в `/etc/fstab`, чтобы ваше устройство было смонтировано при перезагрузке системы.

В нашем случае мы выполняем следующие шаги:

```bash
# Use blkid to get the UUID for the device that we're mounting
blkid

# Edit the fstab file  and add a line to mount your device
# UUID={your uuid}		/mnt/data	{your filesystem}	defaults	0	1
sudo emacs /etc/fstab

# use this to verify the fstab actually works
sudo findmnt --verify --verbose
```

Теперь вы должны иметь возможность выполнить перезагрузку и убедиться, что система загружает смонтированное устройство правильно.

### Настройка Heimdall {#heimdall-setup}
Теперь у нас имеется хост с Docker и мы смонтировали емкое устройство хранения для обеспечения работы программного обеспечения нода Polygon. Теперь мы настроим и запустим Heimdall.

Вначале убедимся, что мы можем запустить Heimdall с Docker. Выполните следующую команду:

```bash
docker run -it 0xpolygon/heimdall:0.2.11 heimdallcli version
```

Если вы запускаете Heimdall с Docker впервые, требуемый образ будет получен автоматически, и так же будет выведена информация о версии.

![img](/img/full-node-docker/heimdall-version.png)

Если вы захотите проверить детали образа Heimdall или найти другой тег, вы можете посмотреть репозиторий в Docker Hub: https://hub.docker.com/repository/docker/0xpolygon/heimdall

Сейчас давайте запустим команду Heimdall `init` для настройки нашего домашнего каталога.

```bash
docker run -v /mnt/data/heimdall:/heimdall-home:rw --entrypoint /usr/local/bin/heimdalld -it 0xpolygon/heimdall:0.2.11 init --home=/heimdall-home
```

Давайте разделим эту команду на части на случай, если что-то пойдет не так. Мы используем `docker run` для запуска команды через Docker. Опция `-v /mnt/data/heimdall:/heimdall-home:rw` очень важна. Она монтирует папку, которую мы создали ранее, `/mnt/data/heimdall` из нашей системы хоста в `/heimdall-home` внутри контейнера как том Docker. `rw` разрешает команде выполнять запись в этот том Docker. Домашний каталог Heimdall в контейнере Docker для любых целей: `/heimdall-home`. Аргумент `--entrypoint /usr/local/bin/heimdalld` переопределяет точку входа по умолчанию для этого контейнера. Опция `-it` используется для интерактивного запуска команды. Наконец, мы указываем, какой образ мы хотим запустить с `0xpolygon/heimdall:0.2.11`. После этого аргументы `init --home=/heimdall-home` передаются в исполняемый модуль heimdalld. Нам нужно запустить команду `init`, и опция `--home` используется для указания расположения домашнего каталога.

После запуска команды `init` ваш каталог `/mnt/data/heimdall` должен иметь определенную структуру и выглядеть так:

![img](/img/full-node-docker/heimdall-tree.png)

Теперь нам необходимо внести немного обновлений, прежде чем запускать Heimdall. Вначале мы отредактируем файл `config.toml`.

```bash
# Open the config.toml and and make three edits
# moniker = "YOUR NODE NAME HERE"
# laddr = "tcp://0.0.0.0:26657"
# seeds = "LATEST LIST OF SEEDS"
sudo emacs /mnt/data/heimdall/config/config.toml
```

Если у вас нет списка сидов, вы можете найти его в документации по настройке полного нода. В нашем случае наш файл содержит следующие три строки:

```
moniker="examplenode01"

# ...

laddr = "tcp://0.0.0.0:26657"

# ...

seeds="f4f605d60b8ffaaf15240564e58a81103510631c@159.203.9.164:26656,4fb1bc820088764a564d4f66bba1963d47d82329@44.232.55.71:26656,2eadba4be3ce47ac8db0a3538cb923b57b41c927@35.199.4.13:26656,3b23b20017a6f348d329c102ddc0088f0a10a444@35.221.13.28:26656,25f5f65a09c56e9f1d2d90618aa70cd358aa68da@35.230.116.151:26656"
```

Теперь ваш файл `config.toml` готов, и вам потребуется внести два небольших изменения в файл `heimdall-config.toml`. Используйте свой любимый редактор для обновления этих двух настроек:

```
# RPC endpoint for ethereum chain
eth_rpc_url = "http://localhost:9545"

# RPC endpoint for bor chain
bor_rpc_url = "http://localhost:8545"
```

`eth_rpc_url` следует заменить на URL-адрес, который вы используете для Ethereum Mainnet RPC. В нашем случае `bor_rpc_url` изменяется на http://bor:8545. После внесения изменений наш файл будет содержать следующие строки:

```
# RPC endpoint for ethereum chain
eth_rpc_url = "https://eth-mainnet.g.alchemy.com/v2/ydmGjsREDACTED_DONT_USE9t7FSf"

# RPC endpoint for bor chain
bor_rpc_url = "http://bor:8545"

```

Команда по умолчанию `init` предоставляет `genesis.json`, но это не будет работать с Polygon Mainnet или Mumbai. Если вы настраиваете узел mainnet, вы сможете запустить эту команду для загрузки правильного файла генезиса:

```bash
sudo curl -o /mnt/data/heimdall/config/genesis.json https://raw.githubusercontent.com/maticnetwork/heimdall/develop/builder/files/genesis-mainnet-v1.json
```

Если вы хотите убедиться, что у вас правильный файл, вы можете проверить это с помощью данного хэша:

```
# sha256sum genesis.json
498669113c72864002c101f65cd30b9d6b159ea2ed4de24169f1c6de5bcccf14  genesis.json
```

## Запуск Heimdall {#starting-heimdall}
Прежде чем запускать Heimdall, мы создадим сеть Docker, чтобы контейнеры могли легко взаимодействовать друг с другом через сеть, используя имена. Чтобы создать сеть, необходимо запустить следующую команду:

```bash
docker network create polygon
```

Теперь мы выполним запуск Heimdall. Выполните следующую команду:

```bash
docker run -p 26657:26657 -p 26656:26656 -v /mnt/data/heimdall:/heimdall-home:rw --net polygon --name heimdall --entrypoint /usr/local/bin/heimdalld -d --restart unless-stopped  0xpolygon/heimdall:0.2.11 start --home=/heimdall-home
```

Многие элементы этой команды будут выглядеть знакомо. Давайте поговорим о том, что изменилось. Опции `-p 26657:26657` и `-p 26656:26656` отвечают за сопоставление портов. Эта команда дает Docker указание сопоставить порт хоста `26657` с портом контейнера `26657` и сделать то же самое для `26656`. Опция `--net polygon` указывает Docker запустить этот контейнер в сети Polygon. `--name heimdall` присваивает контейнеру имя, которое полезно использовать для отладки, однако это имя будет использоваться для подключения к Heimdall других контейнеров. Аргумент `-d` предписывает Docker запустить этот контейнер в фоновом режиме. Опция `--restart unless-stopped` предписывает Docker автоматически перезапускать контейнер, пока он не будет остановлен вручную. Наконец, запуск используется для обеспечения фактической работы приложения вместо простой настройки домашнего каталога через `init`.

Сейчас будет полезно проверить и посмотреть, что происходит. Следующие две команды могут быть полезными:

```bash
# ps will list the running docker processes. At this point you should see one container running
docker ps

# This command will print out the logs directly from the heimdall application
docker logs -ft heimdall
```

Теперь Heimdall нужно начать синхронизацию. Когда вы посмотрите на журналы, вы должны будете увидеть реестр информации, распределенной следующим образом:

```
2022-07-14T23:00:28.917026245Z I[2022-07-14|23:00:28.916] Executed block                               module=state height=5 validTxs=0 invalidTxs=0
2022-07-14T23:00:28.920182861Z I[2022-07-14|23:00:28.920] Committed state                              module=state height=5 txs=0 appHash=15743B4710AE8204D86DFC15ACBA964FC0EAB43D5587FE090E54DD9BA0679D68
2022-07-14T23:00:28.932189412Z I[2022-07-14|23:00:28.932] Executed block                               module=state height=6 validTxs=0 invalidTxs=0
2022-07-14T23:00:28.934951336Z I[2022-07-14|23:00:28.934] Committed state                              module=state height=6 txs=0 appHash=15743B4710AE8204D86DFC15ACBA964FC0EAB43D5587FE090E54DD9BA0679D68
2022-07-14T23:00:28.947276333Z I[2022-07-14|23:00:28.947] Executed block                               module=state height=7 validTxs=0 invalidTxs=0
2022-07-14T23:00:28.950327247Z I[2022-07-14|23:00:28.950] Committed state                              module=state height=7 txs=0 appHash=15743B4710AE8204D86DFC15ACBA964FC0EAB43D5587FE090E54DD9BA0679D68
2022-07-14T23:00:28.965016034Z I[2022-07-14|23:00:28.964] Executed block                               module=state height=8 validTxs=0 invalidTxs=0
2022-07-14T23:00:28.967835073Z I[2022-07-14|23:00:28.967] Committed state                              module=state height=8 txs=0 appHash=15743B4710AE8204D86DFC15ACBA964FC0EAB43D5587FE090E54DD9BA0679D68
2022-07-14T23:00:28.979591550Z I[2022-07-14|23:00:28.979] Executed block                               module=state height=9 validTxs=0 invalidTxs=0
```

Если вы не увидите такую информацию, возможно ваш нод не может найти достаточно пиров. Еще одна полезная команда на данном этапе — вызов RPC для проверки статуса синхронизации Heimdall:

```bash
curl localhost:26657/status
```

При этом будет возвращен ответ следующего вида:

```jsx
{
  "jsonrpc": "2.0",
  "id": "",
  "result": {
    "node_info": {
      "protocol_version": {
        "p2p": "7",
        "block": "10",
        "app": "0"
      },
      "id": "0698e2f205de0ffbe4ca215e19b2ee7275d2c334",
      "listen_addr": "tcp://0.0.0.0:26656",
      "network": "heimdall-137",
      "version": "0.32.7",
      "channels": "4020212223303800",
      "moniker": "examplenode01",
      "other": {
        "tx_index": "on",
        "rpc_address": "tcp://0.0.0.0:26657"
      }
    },
    "sync_info": {
      "latest_block_hash": "812700055F33B175CF90C870B740D01B0C5B5DCB8D22376D2954E1859AF30458",
      "latest_app_hash": "83A1568E85A1D942D37FE5415F3FB3CBD9DFD846A42CBC247DFD6ABB9CE7E606",
      "latest_block_height": "16130",
      "latest_block_time": "2020-05-31T17:06:31.350723885Z",
      "catching_up": true
    },
    "validator_info": {
      "address": "3C6058AF387BB74D574582C2BEEF377E7A4C0238",
      "pub_key": {
        "type": "tendermint/PubKeySecp256k1",
        "value": "BOIKA6z1q3l5iSJoaAiagWpwUw3taAhiEMyZ9ffxAMznas2GU1giD5YmtnrB6jzp4kkIqv4tOmuGYILSdy9+wYI="
      },
      "voting_power": "0"
    }
  }
}
```

На этапе начальной настройки важно обратить особое внимание на поле `sync_info`. Если `catching_up` не соответствует действительности, это означает, что полная синхронизация Heimdall не выполнена. Вы можете посмотреть другие свойства в `sync_info`, чтобы понять, насколько отстает Heimdall.

## Запуск Bor {#starting-bor}
Сейчас у вас должен быть нод, на котором успешно запущен Heimdall. Вам следует подготовиться к запуску Bor.

Прежде чем мы начнем использовать Bor, нам нужно будет запустить сервер Heimdall rest. Эта команда запускает REST API, который используется Bor для извлечения информации из Heimdall. Команда запуска сервера:

```bash
docker run -p 1317:1317 -v /mnt/data/heimdall:/heimdall-home:rw --net polygon --name heimdallrest --entrypoint /usr/local/bin/heimdalld -d --restart unless-stopped 0xpolygon/heimdall:0.2.11 rest-server --home=/heimdall-home --node "tcp://heimdall:26657"
```

Существует два разных компонента этой команды, на которые следует обратить внимание. Вместо команды `start` мы запускаем команду `rest-server`. Также мы передаем `~–node “tcp://heimdall:26657”~`, указывая серверу REST, как следует взаимодействовать с Heimdall.

Если эта команда выполняется успешно, при запуске `docker ps` вы увидите два контейнера команд, которые сейчас работают. Кроме того, если вы запустите эту команду, вы увидите базовый вывод:

```bash
curl localhost:1317/bor/span/1
```

Bor будет использовать этот интерфейс. Так что, если вы не увидите вывода JSON, это будет означать, что что-то идет не так.

Теперь загрузим файл генезиса специально для Bor:

```bash
sudo curl -o /mnt/data/bor/genesis.json 'https://raw.githubusercontent.com/maticnetwork/bor/develop/builder/files/genesis-mainnet-v1.json'
```

Давайте еще раз проверим `sha256 sum` для этого файла:

```
# sha256sum genesis.json
5c10eadfa9d098f7c1a15f8d58ae73d67e3f67cf7a7e65b2bd50ba77eeac67e1  genesis.json
```

Теперь нам нужно инициализировать домашний каталог Bor. Эта команда аналогична тому, что мы делали для Heimdall:

```bash
docker run -v /mnt/data/bor:/bor-home:rw -it  0xpolygon/bor:0.2.16 --datadir /bor-home init /bor-home/genesis.json
```
Большинство частей этой команды должны выглядеть очень знакомо. Вместо `--home` мы устанавливаем флаг `--datadir`, чтобы сообщить bor, где нужно сохранять данные.

Вы можете посмотреть подробную информацию об образе Bor здесь: https://hub.docker.com/repository/docker/0xpolygon/bor

После загрузки файла генезиса и запуска `init` домашний каталог Bor должен выглядеть примерно так.

```bash
tree /mnt/data/bor/
/mnt/data/bor/
├── bor
│   ├── LOCK
│   ├── chaindata
│   │   ├── 000001.log
│   │   ├── CURRENT
│   │   ├── LOCK
│   │   ├── LOG
│   │   └── MANIFEST-000000
│   ├── lightchaindata
│   │   ├── 000001.log
│   │   ├── CURRENT
│   │   ├── LOCK
│   │   ├── LOG
│   │   └── MANIFEST-000000
│   └── nodekey
├── genesis.json
└── keystore

4 directories, 13 files
```

На этом этапе мы должны быть готовы запустить Bor. Мы используем эту команду:

```bash
docker run -p 30303:30303 -p 8545:8545 -v /mnt/data/bor:/bor-home:rw --net polygon --name bor -d --restart unless-stopped  0xpolygon/bor:0.2.16 --datadir /bor-home \
  --port 30303 \
  --bor.heimdall 'http://heimdallrest:1317' \
  --http --http.addr '0.0.0.0' \
  --http.vhosts '*' \
  --http.corsdomain '*' \
  --http.port 8545 \
  --ipcpath /bor-home/bor.ipc \
  --http.api 'eth,net,web3,txpool,bor' \
  --syncmode 'full' \
  --bor-mainnet \
  --miner.gasprice '30000000000' \
  --miner.gaslimit '20000000' \
  --miner.gastarget '20000000' \
  --txpool.nolocals \
  --txpool.accountslots 16 \
  --txpool.globalslots 32768 \
  --txpool.accountqueue 16 \
  --txpool.globalqueue 32768 \
  --txpool.pricelimit '30000000000' \
  --txpool.lifetime '1h30m0s' \
  --maxpeers 200 \
  --bootnodes "enode://0cb82b395094ee4a2915e9714894627de9ed8498fb881cec6db7c65e8b9a5bd7f2f25cc84e71e89d0947e51c76e85d0847de848c7782b13c0255247a6758178c@44.232.55.71:30303,enode://88116f4295f5a31538ae409e4d44ad40d22e44ee9342869e7d68bdec55b0f83c1530355ce8b41fbec0928a7d75a5745d528450d30aec92066ab6ba1ee351d710@159.203.9.164:30303"
```

Если все пройдет хорошо, вы увидите много журналов, которые будут выглядеть так:

```

2022-07-14T23:52:13.192421406Z INFO [07-14|23:52:13.192] Started P2P networking                   self=enode://2397c716686829ecec1e08d8b4517535ac8b7fbf60895c78fd4cdec72f6c7ddaf550c7ca13f3dc505e901ddbd874350e40e29a6d36de1e9649cee30461bd9ae0@127.0.0.1:30303
2022-07-14T23:52:13.193420223Z INFO [07-14|23:52:13.193] IPC endpoint opened                      url=/bor-home/bor.ipc
2022-07-14T23:52:13.193685711Z INFO [07-14|23:52:13.193] HTTP server started                      endpoint=[::]:8545 auth=false prefix= cors=* vhosts=*
2022-07-14T23:52:14.674891110Z INFO [07-14|23:52:14.674] New local node record                    seq=1,657,842,733,191 id=35307c36bf4af514 ip=34.239.165.211 udp=30303 tcp=30303
2022-07-14T23:52:15.689214682Z ERROR[07-14|23:52:15.689] Snapshot extension registration failed   peer=7501eaab err="peer connected on snap without compatible eth support"
2022-07-14T23:52:27.851630533Z INFO [07-14|23:52:27.851] Block synchronisation started
2022-07-14T23:52:28.355760797Z INFO [07-14|23:52:28.355] Downloader queue stats                   receiptTasks=0 blockTasks=0 itemSize=675.23B throttle=8192
2022-07-14T23:52:28.370721935Z WARN [07-14|23:52:28.370] Caller gas above allowance, capping      requested=9,223,372,036,854,775,807 cap=50,000,000
2022-07-14T23:52:28.380999947Z INFO [07-14|23:52:28.380] ✅ Committing new span                    id=1                startBlock=256 endBlock=6655 validatorBytes=f8b6d906822710940375b2fc7140977c9c76d45421564e354ed42277d9078227109442eefcda06ead475cde3731b8eb138e88cd0bac3d901822710945973918275c01f50555d44e92c9d9b353cadad54d905822710947fcd58c2d53d980b247f1612fdba93e9a76193e6d90482271094b702f1c9154ac9c08da247a8e30ee6f2f3373f41d90282271094b8bb158b93c94ed35c1970d610d1e2b34e26652cd90382271094f84c74dea96df0ec22e11e7c33996c73fcc2d822 producerBytes=f8b6d906822710940375b2fc7140977c9c76d45421564e354ed42277d9078227109442eefcda06ead475cde3731b8eb138e88cd0bac3d901822710945973918275c01f50555d44e92c9d9b353cadad54d905822710947fcd58c2d53d980b247f1612fdba93e9a76193e6d90482271094b702f1c9154ac9c08da247a8e30ee6f2f3373f41d90282271094b8bb158b93c94ed35c1970d610d1e2b34e26652cd90382271094f84c74dea96df0ec22e11e7c33996c73fcc2d822
2022-07-14T23:52:28.382875009Z WARN [07-14|23:52:28.382] Caller gas above allowance, capping      requested=9,223,372,036,854,775,807 cap=50,000,000
2022-07-14T23:52:28.383068667Z INFO [07-14|23:52:28.382] Fetching state updates from Heimdall     fromID=1 to=2020-05-30T07:47:16Z
2022-07-14T23:52:28.383082140Z INFO [07-14|23:52:28.382] Fetching state sync events               queryParams="from-id=1&to-time=1590824836&limit=50"
2022-07-14T23:52:28.396655197Z WARN [07-14|23:52:28.396] Caller gas above allowance, capping      requested=9,223,372,036,854,775,807 cap=50,000,000
2022-07-14T23:52:28.396782824Z WARN [07-14|23:52:28.396] Caller gas above allowance, capping      requested=9,223,372,036,854,775,807 cap=50,000,000
2022-07-14T23:52:28.396835015Z INFO [07-14|23:52:28.396] Fetching state updates from Heimdall     fromID=1 to=2020-05-30T16:32:10Z
2022-07-14T23:52:28.396840863Z INFO [07-14|23:52:28.396] Fetching state sync events               queryParams="from-id=1&to-time=1590856330&limit=50"
2022-07-14T23:52:28.407306186Z WARN [07-14|23:52:28.407] Caller gas above allowance, capping      requested=9,223,372,036,854,775,807 cap=50,000,000
2022-07-14T23:52:28.440565699Z INFO [07-14|23:52:28.440] ✅ Committing new span                    id=1                startBlock=256 endBlock=6655 validatorBytes=f8b6d906822710940375b2fc7140977c9c76d45421564e354ed42277d9078227109442eefcda06ead475cde3731b8eb138e88cd0bac3d901822710945973918275c01f50555d44e92c9d9b353cadad54d905822710947fcd58c2d53d980b247f1612fdba93e9a76193e6d90482271094b702f1c9154ac9c08da247a8e30ee6f2f3373f41d90282271094b8bb158b93c94ed35c1970d610d1e2b34e26652cd90382271094f84c74dea96df0ec22e11e7c33996c73fcc2d822 producerBytes=f8b6d906822710940375b2fc7140977c9c76d45421564e354ed42277d9078227109442eefcda06ead475cde3731b8eb138e88cd0bac3d901822710945973918275c01f50555d44e92c9d9b353cadad54d905822710947fcd58c2d53d980b247f1612fdba93e9a76193e6d90482271094b702f1c9154ac9c08da247a8e30ee6f2f3373f41d90282271094b8bb158b93c94ed35c1970d610d1e2b34e26652cd90382271094f84c74dea96df0ec22e11e7c33996c73fcc2d822
2022-07-14T23:52:28.441101234Z WARN [07-14|23:52:28.441] Caller gas above allowance, capping      requested=9,223,372,036,854,775,807 cap=50,000,000
2022-07-14T23:52:28.441350164Z INFO [07-14|23:52:28.441] Fetching state updates from Heimdall     fromID=1 to=2020-05-30T16:34:22Z
```

Существует несколько способов проверить состояние синхронизации Bor. Самый простой — использовать `curl`:

```bash
curl 'localhost:8545/' \
--header 'Content-Type: application/json' \
-d '{
	"jsonrpc":"2.0",
	"method":"eth_syncing",
	"params":[],
	"id":1
}'
```

При запуске этой команды вы получите примерно такой результат:

```jsx
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "currentBlock": "0x2eebf",
    "healedBytecodeBytes": "0x0",
    "healedBytecodes": "0x0",
    "healedTrienodeBytes": "0x0",
    "healedTrienodes": "0x0",
    "healingBytecode": "0x0",
    "healingTrienodes": "0x0",
    "highestBlock": "0x1d4ee3e",
    "startingBlock": "0x0",
    "syncedAccountBytes": "0x0",
    "syncedAccounts": "0x0",
    "syncedBytecodeBytes": "0x0",
    "syncedBytecodes": "0x0",
    "syncedStorage": "0x0",
    "syncedStorageBytes": "0x0"
  }
}
```

Это укажет `currentBlock`, который был синхронизирован, а также `highestBlock`, о котором нам известно. Если нод уже синхронизирован, мы должны получить `false`.

В зависимости от настроек системы у нас может быть возможность использовать консоль для запроса состояния нода. Вот как это можно сделать.

```bash
# first we'll open a shell in the running bor container
docker exec -it bor /bin/sh

# next, we'll open the console which can be used to execute various commands
bor attach /bor-home/bor.ipc

# now we can run eth.syncing to see what's going on
eth.syncing
```

Вы получите определенный вывод, который поможет понять текущий ход выполнения.

```jsx
> eth.syncing
{
  currentBlock: 204991,
  healedBytecodeBytes: 0,
  healedBytecodes: 0,
  healedTrienodeBytes: 0,
  healedTrienodes: 0,
  healingBytecode: 0,
  healingTrienodes: 0,
  highestBlock: 30731838,
  startingBlock: 0,
  syncedAccountBytes: 0,
  syncedAccounts: 0,
  syncedBytecodeBytes: 0,
  syncedBytecodes: 0,
  syncedStorage: 0,
  syncedStorageBytes: 0
}
```
