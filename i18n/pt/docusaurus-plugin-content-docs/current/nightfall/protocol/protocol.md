---
id: protocol
title: Protocolo de Nightfall
sidebar_label: Nightfall Protocol
description: "O Processo de Nightfall."
keywords:
  - docs
  - polygon
  - nightfall
  - protocol
  - chain
  - block
  - structure
  - layer
image: https://matic.network/banners/matic-network-16x9.png
---

Assumimos que pelo menos 1 Proponente se tenha registado no sistema, colocando um Stake mínimo.

## Registo de transação {#transaction-posting}
Existem dois mecanismos para registar novas transações:

- [On-chain](#on-chain)
- [Off-chain](#off-chain)

### On-chain {#on-chain}
O processo começa com um Operador que cria uma transação chamando `submitTransaction` em `Shield.sol`. O Operador paga uma taxa ao contrato Shield para a transação, que pode ser qualquer coisa que o Operador decida. Isto será pago ao Proponente que incorpora a transação num bloco. Atualmente, o proponente e a instância Optimist subjacente provavelmente vão escolher as taxas mais elevadas para incorporar num bloco, da mesma forma que um mineiro faria. A chamada de transação faz com que um evento blockchain seja publicado, contendo os seus detalhes. Se for um Depósito, o contrato Shield retira pagamento do token ERC da Camada 1 em questão.

### Off-chain {#off-chain}
As transações de Transferência e Retirada têm a opção de ser enviadas diretamente para proponentes de escuta, em vez de serem enviadas on-chain através do processo acima. Estas transações off-chain pouparão aos Operadores o custo de envio on-chain de um depósito (~45 mil gás), mas exigem um maior grau de confiança entre os operadores e os proponentes a quem eles escolhem se conectar. É mais fácil para proponentes que se comportem mal censurar as transações recebidas off-chain do que as recebidas on-chain, uma vez que essas transações não são transmitidas para todos os proponentes de escuta. Neste caso, os operadores devem considerar uma transação como confiável somente após o período de reflexão (uma semana).

## Aceitação da transação {#transaction-acceptance}
Quando os Proponentes recebem qualquer transação, realizam uma série de verificações para validar se a transação está bem formada e que a prova é confirmada em relação ao hash de entrada pública. Se todas as verificações forem aprovadas, a transação é adicionada ao mempool do Proponente para ser considerada num Bloco.

## Montagem e submissão de blocos {#block-assembly-and-submission}
Os Proponentes aguardam até que o contrato Shield os atribua como o proponente atual. O Proponente atual recebe, da sua própria instância Optimist interna, um novo bloco que contém transações do seu mempool. Para cada transação, irá calcular a Árvore Merkle do novo compromisso que viria a existir se esta transação fosse adicionada ao contrato Shield.

O bloco contém, portanto, os hashes das transações incluídas no bloco e a raiz da Árvore Merkle do compromisso como existiria após o processamento de todas as transações no bloco (Raiz do Compromisso). Em seguida, o Proponente envia este bloco para o contrato inteligente do Estado.

Quando um bloco é proposto, as informações a seguir são gravadas on-chain:

- Estrutura de dados do bloco
```
  struct Block {
    uint48 leafCount; // note this is defined to be the number of leaves BEFORE the commitments in this block are added
    address proposer;
    bytes32 root; // the 'output' commitment root after adding all commitments
    uint256 blockNumberL2;
    bytes32 previousBlockHash;
    bytes32 transactionHashesRoot;
  }
```
- Transações no bloco
```
    struct Transaction {
        uint112 value;
        uint112 fee;
        TransactionTypes transactionType;
        TokenType tokenType;
        uint64[2] historicRootBlockNumberL2; // number of L2 block containing historic root
        uint64[2] historicRootBlockNumberL2Fee; //number of L2 block containing historic root fee
        bytes32 tokenId;
        bytes32 ercAddress;
        bytes32 recipientAddress;
        bytes32[2] commitments;
        bytes32[2] nullifiers;
        bytes32[1] commitmentFee;
        bytes32[2] nullifiersFee;
        bytes32[2] compressedSecrets;
        uint256[4] proof;
    }
```

## Desafios {#challenges}
Os blocos poderão ser desafiados na fila durante uma semana, durante a qual a sua correção poderá ser desafiada chamando uma das funções desafiantes. Os desafios que podem ser feitos são:

- **INVALID_PROOF** - a prova dada numa transação não verifica como verdadeira;
- **INVALID_PUBLIC_INPUT_HASH** - o hash de entrada pública de uma transação não é o hash correto das entradas públicas;
- **HISTORIC_ROOTHISTORIC_ROOT_EXISTS** - a raiz da Árvore Merkle do compromisso usada para criar a prova da transação nunca existiu;
- **DUPLICATE_NULLIFIER** - um nulificador, dado como parte de uma transação, está presente na lista de nulificadores gastos;
- **HISTORIC_ROOTHISTORIC_ROOT_INVALID** - a raiz de compromisso atualizada que resulta do processamento das transações no bloco não está correta;
- **DUPLICATE_TRANSACTION** - uma transação idêntica à incluída neste bloco já foi incluída num bloco anterior;
- **TRANSACTION_TYPE_INVALID** - a transação não está bem formada com base no tipo de transação (por exemplo, Depósito, Transferência, Retirada).

Se o desafio for bem-sucedido, ou seja, a computação on-chain mostrar que é um desafio válido, as seguintes ações são tomadas:

- O hash do bloco em questão e de todos os blocos subsequentes são removidos da fila.
- O stake do bloco, enviado pelo Proponente, é pago ao Desafiador.
- Os Operadores com a transação no bloco são reembolsados com a taxa que teriam pago ao Proponente e quaisquer fundos depositados detidos pelo contrato Shield no caso de uma transação de Depósito.

