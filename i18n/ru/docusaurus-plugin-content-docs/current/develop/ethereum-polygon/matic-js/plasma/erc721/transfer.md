---
id: transfer
title: трансфер
keywords:
- 'plasma client, erc721, transfer, polygon, sdk'
description: 'Выполнить трансфер токенов от одного пользователя другому.'
---

Метод `transfer` выполняет трансфер токенов от одного пользователя другому.

```
const erc721Token = plasmaClient.erc721(<token address>);

const result = await erc721Token.transfer(<tokenid>,<from>,<to>);

```
