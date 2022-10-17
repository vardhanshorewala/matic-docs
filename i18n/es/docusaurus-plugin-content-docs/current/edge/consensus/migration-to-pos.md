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

Esta sección te guía a través de la migración desde los modos PoA PoS (prueba de participación) IBFT, y viceversa, para un grupo en ejecución - sin la necesidad de restablecer la cadena de bloques.

## Cómo migrar a PoS {#how-to-migrate-to-pos}

Deberás detener todos los nodos, agregar la configuración de bifurcación dentro de genesis.json mediante el comando, `ibft switch`y reinicia los nodos.

````bash
polygon-edge ibft switch --chain ./genesis.json --type PoS --deployment 100 --from 200
````

Para cambiar a PoS, deberá especificar 2 alturas de bloque:`deployment` y`from`. `deployment` es la altura para implementar el contrato de replanteo y `from`es la altura de inicio de PoS. El contrato de participación se desplegará en el domicilio`0x0000000000000000000000000000000000001001` at the`deployment`, al igual que en el caso del contrato pre-desplegado.

Consulte [Prueba de participación](/docs/edge/consensus/pos-concepts) para más detalles acerca del contrato de participación.

:::warning Los validadores necesitan participar manualmente

Cada validador debe participar después de que se implemente el contrato en`deployment` y antes de `from`para ser un validador al comienzo de PoS. Cada validador actualizará al propio validador establecido en la participación del contrato al inicio de PoS.

Para obtener más información acerca de participación, visite la [Configure y use Prueba de Participación](/docs/edge/consensus/pos-stake-unstake).

:::
