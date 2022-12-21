---
id: commitments
title: Compromisos y Nulificadores
sidebar_label: Commitment and Nullifiers
description: "Transferencias únicas y dobles."
keywords:
  - docs
  - polygon
  - nightfall
  - commitment
  - nullifier
image: https://matic.network/banners/matic-network-16x9.png
---


## ¿Qué son los compromisos? {#what-are-commitments}
Un compromiso es una primitiva criptográfica que permite al usuario comprometerse con un valor elegido
mientras mantienes oculto a otros, con la habilidad de revelar el valor comprometido más tarde.
La confidencialidad del valor y el destinatario se alcanza de esta manera.

Cada vez que un usuario realiza una transacción usando Nightfall, la billetera del navegador calcula una prueba
de conocimiento cero (ZKP) y crea (o nulifica) un compromiso.
Por ejemplo, creas un compromiso cuando haces un depósito o transferencia y nulificas un compromiso cuando
haces una transferencia o retiro.

El cálculo de ZKP se basa en [circuitos](../protocol/circuits.md) que definen las reglas que una
transacción debe seguir para ser correcta.

El compromiso se utiliza para ocultar las siguientes propiedades:
- **Dirección ERC del token**
- **Id del token**
- **Valor**
- **Propietario**

Los compromisos se almacenan en una estructura de *Árbol Merkle*. La raíz de este *Árbol Merkle* se almacena en la cadena.

![](../imgs/commitment.png)

### UTXO {#utxo}
Los compromisos se crean durante los depósitos y transferencias, y se gastan durante las transacciones de transferencias y retiros. **Los compromisos no se agregan juntos**. Cuando gastas un compromiso, el valor del compromiso gastado se limita al valor de hasta dos compromisos que se poseen.

Los circuitos actuales de transferencia y retiro de ZKP utilizados en Nightfall están restringidos a 2 entradas - 2 salidas (compromiso de transferencia/retiro y cambio), sin incluir los pagos.
Si un conjunto de compromisos de un transactor contiene principalmente compromisos (polvo), de bajo valor pueden encontrar difícil realizar transferencias futuras.

Observa los siguientes conjuntos de valores

- **Conjunto A**: [1, 1, 1, 1, 1, 1]
- **Conjunto B**: [2, 2, 2]
- **Conjunto C**: [2, 4]

Si bien los tres conjuntos tienen sumas totales equivalentes, la transferencia de valor máxima que pueden realizar los conjuntos *A*, *B*, y *C* son 2, 4, y 6 respectivamente. Esta es una de las razones por las que se prefieren los valores de los compromisos largos. La estrategia de selección de compromisos utilizada mitiga este riesgo al priorizar el uso de los compromisos de valor pequeño, mientras también minimizan la creación de compromisos de polvo.


## ¿Qué son los Nulificadores? {#what-are-nullifiers}
Un **Nulificador** es el resultado de la combinación de un compromiso y la clave nulificadora. Una vez que el nulificador se transmite en la cadena, el compromiso se considera gastado.
Los nulificadores se almacenan en la cadena como parte de los datos de la llamada durante la propuesta de bloque.

![](../imgs/nullifier.png)



