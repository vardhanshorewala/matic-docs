---
id: accounts
title: ¿Qué son cuentas?
sidebar_label: Accounts
description: "Cuentas de contratos y EOA "
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
El estado global de Ethereum se compone de cuentas que interactúan entre sí a través de un marco de transmisión de mensajes. La interacción más básica es el envío de un valor (como las tokens MATIC, Ether) la criptomoneda nativa de la cadena de bloques de Ethereum.
 Cada cuenta está identificada por un identificador hexadecimal de 20 bytes que se denomina dirección y que se genera a partir de la clave pública de la cuenta.
 Existen dos tipos de cuentas:

1. Cuenta de propiedad externa: se trata de una cuenta controlada por una clave privada, y si posees la clave privada asociada a la cuenta tienes la capacidad de enviar tokens y mensajes desde ella.
2. Cuenta de propiedad del contrato: se trata de una cuenta que tiene un código de contrato inteligente asociado y su clave privada no es propiedad de nadie

Estos pueden ser diferenciados de la siguiente manera:

**Cuentas de propiedad externa**

1. puede enviar transacciones (transferencia de Ether o activación del código de contrato)
2. se controla por claves privadas
3. no tiene ningún código asociado

**Cuenta de propiedad del contrato**

1. tiene código asociado
2. La ejecución de código se activa mediante transacciones o mensajes (llamadas) recibidos de otros contratos
3. cuando se ejecuta, realiza operaciones de complejidad arbitraria (Turing completo), manipula su propio almacenamiento persistente, es decir, puede tener su propio estado permanente, puede llamar a otros contratos.

### **dirigirse:recursos**

[Lee más sobre las cuentas](https://github.com/ethereum/homestead-guide/blob/master/source/contracts-and-transactions/account-types-gas-and-transactions.rst#externally-owned-accounts-eoas)
