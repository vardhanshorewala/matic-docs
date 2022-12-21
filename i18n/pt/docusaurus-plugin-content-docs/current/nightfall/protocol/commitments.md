---
id: commitments
title: Compromissos e Nulificadores
sidebar_label: Commitment and Nullifiers
description: "Transferência única e dupla."
keywords:
  - docs
  - polygon
  - nightfall
  - commitment
  - nullifier
image: https://matic.network/banners/matic-network-16x9.png
---


## O que são compromissos? {#what-are-commitments}
Um compromisso é um primitivo de criptografia que permite que um utilizador se comprometa com um valor escolhido enquanto o mantém oculto de outros, com a capacidade de revelar o valor comprometido posteriormente. A confidencialidade do valor e do destinatário é alcançada desta maneira.

Sempre que um utilizador executa uma transação usando o Nightfall, a carteira do navegador calcula uma Prova de Conhecimento Zero (ZKP) e cria (ou anula) um compromisso. Por exemplo, cria um compromisso quando efetua um depósito ou transferência, e anula um compromisso quando efetua uma transferência ou retirada.

A computação ZKP depende de [circuitos](../protocol/circuits.md) que definem as regras que uma transação deve seguir para estar correta.

O compromisso é usado para ocultar as seguintes propriedades:
- **Endereço de ERC do token**
- **Identificação do token**
- **Valor**
- **Proprietário**

Os compromissos são armazenados numa estrutura de *Árvore de Merkle*. A raiz desta *Árvore de Merkle* é armazenada on-chain.

![](../imgs/commitment.png)

### UTXO {#utxo}
Os compromissos são criados durante os depósitos e as transferências, e são gastos durante as transações de transferências e retiradas. **Os compromissos não são agregados juntos**. Quando se gasta um compromisso, o valor do compromisso gasto é limitado ao valor de até quaisquer dois compromissos detidos.

Os circuitos de transferência e retirada de ZKP atuais usados no Nightfall são restritos a 2 entradas e 2 saídas (compromisso de transferência/retirada e câmbio), excluindo os pagamentos. Se o conjunto de compromissos de um operador contiver principalmente compromissos de baixo valor (poeira), podem ter dificuldade em realizar futuras transferências.

Observe os conjuntos de valores a seguir

- **Conjunto A**: [1, 1, 1, 1, 1, 1]
- **Conjunto B**: [2, 2, 2]
- **Conjunto C**: [2, 4]

Embora todos os três conjuntos tenham somas totais equivalentes, a transferência de valor máximo que pode ser efetuada pelos conjuntos *A*, *B* e *C* são 2, 4 e 6, respetivamente. Esta é uma das razões pelas quais se dá preferência a grandes valores de compromissos. A estratégia de seleção de compromissos adotada reduz este risco, dando prioridade à utilização de compromissos de pequeno valor, ao mesmo tempo que também minimiza a criação de compromissos de poeira.


## O que são nulificadores? {#what-are-nullifiers}
Um **nulificador** é o resultado de uma combinação de um compromisso e da chave de nulificador. Quando o nulificador é transmitido on-chain, o compromisso é considerado gasto. Os nulificadores são armazenados on-chain como parte dos dados de chamada durante a proposta de blocos.

![](../imgs/nullifier.png)



