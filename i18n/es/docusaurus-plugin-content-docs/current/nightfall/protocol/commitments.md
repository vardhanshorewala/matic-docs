---
id: commitments
title: Compromisos y anuladores
sidebar_label: Commitment and Nullifiers
description: "Transferencia única y doble."
keywords:
  - docs
  - polygon
  - nightfall
  - commitment
  - nullifier
image: https://matic.network/banners/matic-network-16x9.png
---


## ¿Qué son los compromisos? {#what-are-commitments}
Un compromiso es una primitiva criptográfica que permite a un usuario a comprometerse con un valor elegido
mientras lo mantiene oculto a otros, con la capacidad de revelar el valor comprometido más adelante.
De esta manera se logra la confidencialidad del valor y del destinatario.

Cada vez que un usuario realiza una transacción utilizando Nightfall, la billetera del navegador calcula una
prueba de conocimiento cero (ZKP) y crea (o anula) un compromiso.
Por ejemplo, creas un compromiso cuando haces un depósito o una transferencia y anulas un compromiso cuando
realizas una transferencia o retiro.

El cómputo ZKP depende de [circuitos](../protocol/circuits.md) que definen las reglas que una
transacción debe seguir para ser correcta.

El compromiso es utilizado para ocultar las siguientes propiedades:
- **dirección ERC del token**
- **Id. del token**
- **Valor**
- **Propietario**

Los compromisos se almacenan en una estructura de *árbol de Merkle*. La raíz de este *árbol de Merkle* se almacena en cadena.

![](../imgs/commitment.png)

### UTXO {#utxo}
Los compromisos se crean durante los depósitos y las transferencias, y se gastan durante las transacciones de transferencias y retiros. **Los compromisos no se agregan juntos**. Al gastar un compromiso, el valor del compromiso gastado se limita al valor de hasta dos compromisos que se posean.

Los circuitos actuales de transferencia y de retiro ZKP utilizados en Nightfall se restringen a 2 entradas - 2 salidas (compromiso de transferencia/retiro y cambio) excluyendo los pagos.
Si el conjunto de compromisos de un transactor contiene principalmente compromisos de valores bajos (polvo), puede que les resulte difícil realizar futuras transferencias.

Observa los valores de los siguientes conjuntos

- **Conjunto A**: [1, 1, 1, 1, 1, 1]
- **Conjunto B**: [2, 2, 2]
- **Conjunto C**: [2, 4]

Mientras que los tres conjuntos tienen sumas totales equivalentes, la transferencia de valor máximo que se puede realizar por los conjuntos *A*, *B* y *C* son 2, 4 y 6 respectivamente. Esta es una de las razones por las que se prefieren los valores de los compromisos grandes. La estrategia de selección de compromiso utilizada mitiga este riesgo al priorizar el uso de pequeños compromisos de valor al tiempo que minimiza la creación de compromisos de polvo.


## ¿Qué son los anuladores? {#what-are-nullifiers}
Un **anulador** es el resultado de la combinación de un compromiso y la clave anuladora. Una vez que el anulador se transmite en cadena, se considera que el compromiso. está usado.
Los anuladores se almacenan en cadena como parte de los datos de llamada durante la propuesta de bloque.

![](../imgs/nullifier.png)



