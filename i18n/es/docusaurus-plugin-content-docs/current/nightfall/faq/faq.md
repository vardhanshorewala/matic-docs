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

Si no encuentras tu pregunta en esta lista, envía tu pregunta en el <ins>**[servidor de Discord de Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR)**</ins>.

:::

## ¿Dónde puedo encontrar los contratos inteligentes? {#where-can-i-find-the-smart-contracts}

Los contratos de Polygon Nightfall se han desplegado en la [red de prueba Goerli](../deployments/testnet.md) y [red principal](../deployments/mainnet.md).

## ¿Cuál es la declaración de la auditoría de seguridad de Polygon Nightfall? {#what-s-the-state-of-polygon-nightfall-s-security-audit}
Polygon Nightfall está actualmente sometida a la auditoría de seguridad que se planea que debe terminar durante el 3er. trimestre. Mientras tanto, se han agregado varias restricciones al protocolo:

- Único proponente que se ejecuta y administra por Polygon
- [Depósitos restringidos y retiros de cantidades](../tools/nightfall-wallet.md#deposit-and-withdraw-restrictions)

## ¿Cómo configuro mi billetera de Nightfall? {#how-do-i-set-up-my-nightfall-wallet}
Hay un tutorial completo de billetera [aquí](../tools/nightfall-wallet.md) con todos los detalles sobre cómo comenzar con la billetera Polygon Nightfall.

## ¿Cómo me conecto a una billetera de hardware Ledger a la billetera de Nightfall? {#how-do-i-connect-a-ledger-hardware-wallet-to-nightfall-wallet}
Existe una sección en el tutorial de la billetera que explica [cómo conectar una billetera de Hardware Ledger con Metamask](../tools/nightfall-wallet.md#how-to-connect-a-ledger-hardware-wallet-to-nightfall).

## ¿Cuánto tiempo toman las transferencias en la red de Polygon Nightfall desde el inicio hasta el final? {#how-long-do-transfers-take-on-polygon-nightfall-network-from-start-to-finish}
El proponente actual toma transacciones de los usuarios y hace bloques de hasta 32 transacciones. Tan pronto como se recopilan suficientes transacciones para construir un bloque, las transacciones se procesarán.

Además, existe un límite superior en el periodo de generación del bloque de manera que se proponga al menos un bloque cada 6 horas (independientemente del número de transacciones recolectadas por el proponente).

## ¿Con quién puedo transaccionar? {#who-can-i-transact-with}
Para transferir activos dentro de Polygon Nightfall solo se necesita la `Destination Wallet Address`. Lee el tutorial de billetera para comprender [cómo compartir tu dirección de billetera](../tools/nightfall-wallet.md#your-wallet-address) para recibir fondos.

## ¿En dónde se respaldan los compromisos? {#where-are-commitments-backed-up}

Las pruebas de cero conocimientos se calculan en el navegador de manera que tus claves secretas permanecen contigo, y la billetera realiza un seguimiento de cualquier compromiso que poseas, en su IndexedDb. Cualquier persona con acceso a estos datos puede averiguar qué compromisos posees, aunque no pueden robarlos sin tus claves. Las claves solo se desencriptan cuando ingresas a la mnemotécnica. Por lo tanto, solo deberías usar la billetera en una máquina en la que confíes.

Por ahora, estos datos no se exportan en ninguna parte. Por lo tanto, si usas un navegador en una máquina diferente, no tendrás acceso a tus compromisos a menos que transfieras el contenido de IndexedDB. Proporcionamos un mecanismo para exportar e importar compromisos a través de la billetera.

## Privacidad de transacciones {#privacy-of-transactions}
Es importante entender que el depósito y retiro de transacciones no son privadas. Eso se debe a que interactúan con la capa 1 y con la capa 1 que no es privada. Esto significa que todo el mundo sabe si tú creas un compromiso de la capa 2 y cuánto contiene. Del mismo modo, si regresas un token de regreso a la capa 1 mediante la destrucción de un compromiso de la capa 2, todo el mundo sabe quién lo recibió y cuánto.

La privacidad viene enteramente de transferencias dentro de la capa 2. Desde el punto de vista de la cadena de bloques Ethereum, estas son privadas por completo. Los únicos datos filtrados es tu dirección IP cuando envías una transacción de transferencia a un proponente de bloques. Para la Beta temprana, Polygon ejecuta los únicos proponentes.


## ¿Cómo retirar fondos? {#how-to-withdraw-funds}
Los fondos pueden retirarse con la billetera de Polygon Nightfall. Los retiros tienen un periodo de finalización de **una semana** desde el momento en que se creó el bloque incluyendo las transacciones de retiro. Cuando este periodo haya transcurrido, puedes finalizar la retirada para que tus fondos sean enviados a tu cuenta de Ethereum.

## ¿Cuánto costarán las transacciones en Nightfall? {#how-much-will-transactions-cost-on-nightfall}
Existen dos tipos de transacciones que soportan costos diferentes:

- Las transacciones en cadena: estas transacciones se envían al contrato Smart y requieren que las tarifas de gas en Ethereum sean minadas. Cualquier proponente puede tomar esta transacción y ponerla en un bloque. Actualmente,`deposit` y `finalize withdrawal` son transacciones en cadena.
- Las transacciones fuera de la cadena: estas transacciones se envían directamente al proponente. Actualmente, todas `transfer` y `withdrawals` son configuradas como transacciones fuera de la cadena.

## ¿Cuáles tokens puedo usar en la red Nightfall? {#which-tokens-can-i-use-on-nightfall-network}
Los siguientes tokens son operativos en Nightfall:

- MATIC
- WETH
- DAI
- USDC

## ¿Necesito tokens MATIC para usar Nightfall? {#do-i-need-matic-tokens-to-use-nightfall}
Sí. Deberá depositar algunos tokens MATIC en Nightfall para poder pagar `transfers` y `withdrawals`.

## ¿Dónde puedo enviar un informe de errores o contactar a Nightfall para ayuda adicional? {#where-can-i-submit-a-bug-report-or-contact-nightfall-for-additional-help}
La mejor manera es unirse a nuestro [servidor discord de Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR) y enviar su pregunta.
