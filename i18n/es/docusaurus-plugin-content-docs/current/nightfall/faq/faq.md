---
id: faq
title: Preguntas frecuentes
sidebar_label: FAQ
description: Preguntas frecuentes acerca de Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip

Si no encuentras tu pregunta en esta lista, envía tu pregunta en el <ins>**[servidor Discord de Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR)**</ins>
:::

## ¿Dónde puedo encontrar los contratos inteligentes? {#where-can-i-find-the-smart-contracts}

Los contratos Polygon nightfall están desplegados en [la red de pruebas Goerli](../deployments/testnet.md) y en [mainnet](../deployments/mainnet.md).

## ¿Cuál es el estado de la auditoría de seguridad de Polygon Nightfall? {#what-s-the-state-of-polygon-nightfall-s-security-audit}
Actualmente, Polygon Nightfall está bajo auditoría de seguridad que está prevista terminar durante el tercer trimestre. Mientras tanto, se añadieron varias restricciones al protocolo:

- Un proponente único en ejecución y gestionado por Polygon
- [Restricción de los importes de depósito y retiro](../tools/nightfall-wallet.md#deposit-and-withdraw-restrictions)

## ¿Cómo configuro mi billetera Nightfall? {#how-do-i-set-up-my-nightfall-wallet}
Puedes encontrar un tutorial completo de la billetera [aquí](../tools/nightfall-wallet.md) con todos los detalles sobre cómo empezar con la billetera Polygon Nightfall.

## ¿Cómo conectar una billetera Ledger Hardware a la billetera Nightfall? {#how-do-i-connect-a-ledger-hardware-wallet-to-nightfall-wallet}
Hay una sección en el tutorial de la billetera que explica [cómo conectar una billetera Ledger Hardware con Metamask](../tools/nightfall-wallet.md#how-to-connect-a-ledger-hardware-wallet-to-nightfall).

## ¿Cuánto tiempo toman las transferencias en la red de Polygon Nightfall de principio a fin? {#how-long-do-transfers-take-on-polygon-nightfall-network-from-start-to-finish}
El proponente actual toma las transacciones de los usuarios y hace bloques de hasta 32 transacciones. La transacción se procesará tan pronto como se cobren suficientes transacciones para construir un bloque.

Además, hay un límite superior en el período de generación de bloques para que por lo menos se proponga un bloque cada 6 horas (independientemente del número de transacciones cobradas por el proponente).

## ¿Con quién puedo hacer transacciones? {#who-can-i-transact-with}
Para realizar transferencia de activos dentro de Polygon Nightfall solo se necesita la `Destination Wallet Address`. Lee el tutorial de la billetera para entender [cómo compartir tu dirección de la billetera](../tools/nightfall-wallet.md#your-wallet-address) para recibir fondos.

## ¿Dónde están respaldados los compromisos? {#where-are-commitments-backed-up}

Las pruebas de conocimiento cero se calculan en el navegador para que tus claves secretas permanezcan contigo, y la billetera realiza un seguimiento de cualquier compromiso que poseas, en su IndexedDb. Cualquier persona con acceso a estos datos puede averiguar qué compromisos posees, aunque no pueden robarlos sin tus claves. Las claves solo se descifran al ingresar el mnemónico. Por lo tanto, solo deberías usar la billetera en una máquina en la que confías.

Por ahora, estos datos no se exportan a ninguna parte. Por lo tanto, si usas un navegador en una máquina diferente, no tendrás acceso a tus compromisos a menos que transfieras los contenidos del IndexedDB. Proporcionamos un mecanismo para exportar e importar compromisos a través de la billetera.

## Privacidad de las transacciones {#privacy-of-transactions}
Es importante entender que las transacciones de depósito y retiro no son privadas. Eso se debe a que interactúan con la capa 1 y esta no es privada. Esto significa que todo el mundo sabe si creas un compromiso capa 2 y cuánto contiene. Del mismo modo, si devuelves un token a la capa 1 al destruir un compromiso de la capa 2, todo el mundo sabe quién lo recibió y cuánto.

La privacidad viene por completo de transferencias dentro de la capa 2. Desde el punto de vista de la cadena de bloques Ethereum, estas son completamente privadas. El único dato filtrado es tu dirección IP cuando envías una transacción de transferencia a un Proponente de bloques. Para la beta inicial, Polygon ejecuta los únicos proponentes.


## ¿Cómo retirar fondos? {#how-to-withdraw-funds}
Los fondos pueden ser retirados de la billetera Polygon Nightfall. Los retiros tienen un período de finalización de**una semana** desde el momento en que se creó el bloque que incluye la transacción de retiro. Una vez transcurrido este período de tiempo, puedes finalizar el retiro para que tus fondos sean enviados a tu cuenta Ethereum.

## ¿Cuánto costarán las transacciones en Nightfall? {#how-much-will-transactions-cost-on-nightfall}
Hay dos tipos de transacciones que poseen diferentes costos:

- Transacciones en cadena: estas transacciones se envían al contrato inteligente y requieren que se minen las tarifas de gas de Ethereum. Cualquier proponente puede tomar esta transacción y ponerla en un bloque. Actualmente, `deposit` y `finalize withdrawal` son transacciones en cadena.
- Transacciones fuera de la cadena: estas transacciones se envían directamente al proponente Actualmente, todas las `transfer` y `withdrawals` son configuradas como transacciones fuera de cadena.

## ¿Qué tokens puedo usar en la red Nightfall? {#which-tokens-can-i-use-on-nightfall-network}
Los siguientes tokens son operativos en Nightfall:

- MATIC
- WETH
- DAI
- USDC

## ¿Necesito tokens MATIC para usar Nightfall? {#do-i-need-matic-tokens-to-use-nightfall}
Sí. Necesitarás depositar algunos tokens MATIC en Nightfall para poder pagar por `transfers` y `withdrawals`.

## ¿Dónde puedo presentar un informe de errores o contactar a Nightfall para recibir ayuda adicional? {#where-can-i-submit-a-bug-report-or-contact-nightfall-for-additional-help}
La mejor manera es unirse a nuestro [servidor Discord de Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR) y enviar tu pregunta.
