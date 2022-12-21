---
id: circuits
title: Circuitos e Transações
sidebar_label: Circuits and Transactions
description: "Tipos de circuitos no Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - circuits
  - deposit
  - transfer
image: https://matic.network/banners/matic-network-16x9.png
---

Os circuitos são usados para definir as regras que uma transação deve seguir para ser considerada correta. Existem, em geral, três tipos de circuitos, um para cada tipo transação:

- [Depósito](#deposit)
- [Transferência](#transfer)
- [Retirada](#withdraw)

Cada transação inclui uma prova ZK seguindo as restrições especificadas nestes circuitos. Os utilizadores constroem esta prova usando uma carteira, ou através de um servidor de Cliente. Uma prova é gerada apenas se todos os seguintes casos forem verdadeiros:

- O novo [compromisso](./commitments#what-are-commitments) é válido
- O [compromisso](./commitments#what-are-commitments) antigo é válido e propriedade do remetente
- O [nulificador] (./commitments#what-are-nullifiers) é válido
- O caminho/raiz da árvore Merkle é válido
- O Ciphertext que contém o compromisso é válido


## Depósito {#deposit}
Os depósitos convertem tokens de ERC publicamente visíveis num compromisso de token que detém o mesmo valor ou ID de token que o token original, e a chave pública do Nightfall do proprietário de compromisso pretendido.

Uma Prova de Depósito ZK comprova que o proponente criou um compromisso $Z_A$ with a public key $pk_A$válido.

O circuito verifica então que $Z_A$ == H(@ | ɑ | $pk_A$ | σ) As informações reveladas de uma transação de depósito incluem o endereço que cunhou o novo compromisso e o endereço e valor do token de ERC que está a ser usado.

![](../imgs/deposit.png)

## Transferência {#transfer}
As transferências permitem a transmissão de até dois compromissos do mesmo ativo entre duas partes anulando os compromissos anteriores e criando até dois novos compromissos:
- Um será enviado para o destinatário, com o valor do montante transferido
- O outro será criado com o valor da alteração (diferença entre a soma de valores de compromissos usados menos o valor transferido) e propriedade do transmissor.

Um Prova de Transferência ZK comprova que o proponente anulou até dois compromissos antigos que existiam na Árvore Merkle, criou um novo e criptografou as suas informações para o destinatário.

Em ambos os casos, as informações reveladas serão que um endereço de Ethereum anulou compromissos entre o pool de compromissos que pertence ao transmissor, e que novos compromissos foram criados. As informações sobre o novo proprietário, que compromissos foram gastos ou o valor transferido permanecem privadas.

O primeiro diagrama mostra as etapas para anular um compromisso existente (ou compromissos) e adicionar informações à estrutura dados de `transaction`.

![](../imgs/transfer_a.png)

O segundo diagrama apresenta as etapas necessárias para gerar e criptografar o compromisso recém-criado.

![](../imgs/transfer_b.png)

## Retirada {#withdraw}
A Retirada é a operação de anular um compromisso existente no Nightfall e convertê-lo em tokens de ERC publicamente visíveis com o mesmo valor e ID de token que o compromisso anulado. A Retirada é a operação oposta ao Depósito. Da mesma forma que as transferências, as retiradas aceitam como entrada até dois compromissos.

Uma Prova de Retirada ZK comprova que o proponente anulou até dois compromissos antigos que existiam na Árvore Merkle.

As informações reveladas durante uma retirada incluem o endereço que retirou o compromisso e a ID e o endereço de token/valor do token retirado.

![](../imgs/withdraw.png)

### Período de reflexão {#cooling-off-period}

As retiradas exigem um `COOLING OFF`período de uma semana para serem finalizadas. Isto ocorre devido à natureza otimista do Nightfall, uma vez que um novo bloco é considerado correto até que algum desafiador envie uma prova de fraude. Os fundos são mantidos durante uma semana e podem ser retirados para a Camada 1.

# Taxas {#fees}

O proponente cobra uma taxa para integrar a transação recebida num bloco de Camada 2. Existem dois tipos de taxas diferentes para a proposta, dependendo da transação:
- Os depósitos pagam taxas de ETH diretamente na Camada 1.
- As Transferências e as Retiradas pagam taxas no MATIC na camada 2.
