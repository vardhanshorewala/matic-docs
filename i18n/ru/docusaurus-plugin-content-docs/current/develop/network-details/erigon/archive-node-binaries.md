---
id: archive-node-binaries
title: Настройка архивного нода с двоичными файлами
sidebar_label: Set up an Archive Node with Binaries
description: "Использование двоичных файлов для настройки архивного нода."
keywords:
  - erigon
  - archive
  - node
  - binary
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip

Для настройки архивного нода применяется тот же процесс, что и для <ins>развертывания полного нода с двоичными файлами</ins>. Однако при этом для него требуется незначительное изменение конфигурации. В файл `start.sh` нужно включить следующий параметр:

```makefile
--gcmode 'archive'
```
