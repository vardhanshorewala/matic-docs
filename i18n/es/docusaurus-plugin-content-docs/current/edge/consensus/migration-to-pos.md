---
id: migration-to-pos
title: Migración desde PoA a PoS
description: "Cómo migrar desde el modo PoS (prueba de participación) al modo PoS IBFT viceversa."
keywords:
  - docs
  - polygon
  - edge
  - migrate
  - PoA
  - PoS
---

## Resumen {#overview}

Esta sección te guía a través de la migración desde los modos PoA PoS (prueba de participación) IBFT, y viceversa, para un cluster en ejecución

##  {#how-to-migrate-to-pos}



````bash
polygon-edge ibft switch --chain ./genesis.json --type PoS --deployment 100 --from 200
````





:::warning



:::
