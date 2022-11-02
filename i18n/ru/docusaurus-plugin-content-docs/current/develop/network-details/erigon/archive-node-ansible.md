---
id: archive-node-ansible
title: Настройка архивного нода с помощью Ansible
sidebar_label: Set up an Archive Node with Ansible
description: "Использование Ansible для настройки архивного нода."
keywords:
  - erigon
  - archive
  - node
  - ansible
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip

Для настройки архивного нода применяется тот же процесс, что и для <ins>развертывания полного нода</ins>. Однако при этом для него требуется незначительное изменение конфигурации. В файл `start.sh` нужно включить следующий параметр:

```makefile
--gcmode 'archive'
```
