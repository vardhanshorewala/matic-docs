---
id: versions
title: História
sidebar_label: History of changes
description: "Versões implantadas"
keywords:
  - docs
  - polygon
  - nightfall
  - changelog
image: https://matic.network/banners/matic-network-16x9.png
---


## Beta 1.0 {#beta-1-0}
Beta 1.0 foi lançada em 17 de maio de 2022. Incluiu o mecanismo básico para ter a prova de conceito do Nightfall implantada. Apoiou uma `coarse`implementação única `Proposer`e primeira das transações. Também forneceu uma versão preliminar de uma carteira de utilizador. A versão implantada pode ser encontrada [aqui](https://github.com/EYBlockchain/nightfall_3/commit/bc3e475de3e2877f14430f9599e5b38ea960765b)

## Beta 2.0 {#beta-2-0}
A versão implantada pode ser encontrada [aqui](https://github.com/EYBlockchain/nightfall_3/commit/4c2af01ac95af5ea6f5b40071d73a1624f06ba46) Foram efetuadas várias melhorias:
- **Cobrança de taxas**

Capacidade de os proponentes cobrarem taxas para transações. Este recurso incentivará múltiplos proponentes.
- **Implantação do Challenger**

A rede agora inclui um challenger que monitora os blocos do proponente.
- **Transações de circuitos**

Maior flexibilidade e melhor desempenho ao gerar o ZKP de quaisquer transações.  Tanto `transfer`como `withdrawal` aceitam até dois compromissos e variação de retorno. No que diz respeito ao desempenho, as transações agora são otimizadas para que a prova leve menos tempo.

| Operações | Restrições antes | Restrições depois |
|-----------|--------------------|------------------|
| Depósito | 84.766 | 1277 |
| Transferência | 499.119 | 67.694 |
| Retirada | 168.883 | 53.348 |

Parte da otimização foi possível ao mudar para Poseidon

- **Criptografia secreta**

Passámos do El-Gamal para um processo de criptografia [KEM-DEM](../protocol/secrets) que resultou em vários benefícios:
- Simplificação do processo de criptografia/descriptografia
- Redução das restrições e dos custos de gás on-chain.

- **Implantação do challenger**

