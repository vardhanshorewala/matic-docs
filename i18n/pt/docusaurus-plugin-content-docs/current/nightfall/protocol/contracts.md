---
id: contracts
title: Contratos Inteligentes
sidebar_label: Smart Contracts
description: "Shield, proponentes, desafios e computações da Árvore de Merkle."
keywords:
  - docs
  - polygon
  - nightfall
  - smart
  - contracts
  - shield
image: https://matic.network/banners/matic-network-16x9.png
---

Os contratos definem as regras que cada interveniente do Nightfall precisa seguir para operar na rede. Os contratos inteligentes incluem:

- [Shield.sol](#shield)
- [Proposers.sol](#proposers)
- [Challenges.sol](#challenges)
- [MerkleTree_Computations.sol](#merkletree_computations)

## Shield {#shield}
Este contrato permite que um utilizador envie uma transação para processamento por um Proponente. Se for uma transação de depósito, aceitará pagamento. Também permite que qualquer pessoa solicite que o estado do contrato Shield (raiz de compromisso e listas de nulificadores) seja atualizado. Quando o estado for atualizado, todas as retiradas na atualização serão processadas.

Não há necessidade fundamental de publicar uma transação de transferência ou retirada para o blockchain: está simplesmente a agir como um quadro de mensagens para proponentes para incorporar a transação num bloco da Camada 2.

Como o Nightfall interage com contratos de ERC reais, as seguintes verificações não podem ser tornadas privadas:

- Durante o **Depósito/Retirada**, o endereço de token de ERC é válido.
- Durante o **Depósito**, o utilizador tem saldo e possui token para criar compromisso.

## Proponentes {#proposers}
O contrato inclui funcionalidade para registar, cancelar registo, pagar e alternar proponentes e propor um novo bloco de Camada 2 para o blockchain. A primeira versão do Nightfall aceita apenas um único proponente de Boot operado pela Polygon. Nas próximas versões, esta restrição será levantada quando forem permitidos múltiplos proponentes.

## Desafios {#challenges}
A funcionalidade permite que um bloco seja desafiado como incorreto.

## MerkleTree_Stateless {#merkletree_stateless}
Uma versão stateless (função pura) do original `MerkleTree.sol`, usada por  `Challenges.sol`para ajudar a computar desafios de blocos on-chain.

## Outros contratos {#other-contracts}
- `Utils.sol`— recolhe funcionalidades que são usadas em vários contratos ou que, se deixadas em linha, afetariam a legibilidade do código.
- `Config.sol` — tem constantes semelhantes a um arquivo de config. Node.js.
- `Structures.sol`— define estruturas, enumerações, eventos, mapeamentos e variáveis de estado globais. Torna-os mais fáceis de encontrar.

## Capacidade de atualização {#upgradability}
Pelo menos inicialmente, a Polygon mantém a capacidade de atualizar os contratos do Nightfall após a implantação. Para isso, usamos [plugins de atualização](https://docs.openzeppelin.com/upgrades-plugins/1.x/) do Openzeppelin para truffle.

A Polygon usa um módulo de [implantação](https://github.com/EYBlockchain/nightfall_3/tree/master/nightfall-deployer) para atualizar contratos. O `deployer`tem 4 migrações armazenadas na sua pasta de migração. As três primeiras migrações executam uma implantação "normal" do conjunto de contrato Polygon Nightfall. No entanto, certificam-se de que todos os contratos (mas não bibliotecas) são implantados com um proxy para permitir que sejam atualizados posteriormente. A quarta migração é usada para atualizar contratos.
