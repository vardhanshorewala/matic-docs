---
id: faq
title: Perguntas frequentes
sidebar_label: FAQ
description: Perguntas frequentes sobre o Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip
Se não encontrar a sua pergunta nesta lista, envie a pergunta no <ins>**[servidor de discord Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR)**</ins>.
:::

## Onde posso encontrar os Contratos Inteligentes? {#where-can-i-find-the-smart-contracts}

Os contratos Polygon Nightfall foram implantados na [testnet Goerli](../deployments/testnet.md) e na [mainnet](../deployments/mainnet.md).

## Qual é o estado da auditoria de segurança Polygon Nightfall? {#what-s-the-state-of-polygon-nightfall-s-security-audit}
O Polygon Nightfall está atualmente a ser submetido a uma auditoria de segurança que se espera estar concluída durante o terceiro trimestre. Entretanto, várias restrições foram adicionadas ao protocolo:

- Proponente único em execução e gerido por Polygon
- [Valores limitados de depósito e retirada](../tools/nightfall-wallet.md#deposit-and-withdraw-restrictions)

## Como faço para configurar a minha Carteira Nightfall? {#how-do-i-set-up-my-nightfall-wallet}
Há um tutorial sobre carteira completo [aqui](../tools/nightfall-wallet.md) com todos os detalhes sobre como começar com a carteira Polygon Nightfall.

## Como conectar uma carteira física Ledger à Carteira Nightfall? {#how-do-i-connect-a-ledger-hardware-wallet-to-nightfall-wallet}
Há uma secção no tutorial sobre carteira que explica [como conectar uma carteira física Ledger com MetaMask](../tools/nightfall-wallet.md#how-to-connect-a-ledger-hardware-wallet-to-nightfall).

## Quanto tempo levam as transferências na rede Polygon Nightfall do início ou fim? {#how-long-do-transfers-take-on-polygon-nightfall-network-from-start-to-finish}
O proponente atual reúne transações de utilizadores e faz blocos de até 32 transações. Assim que forem recolhidas transações suficientes para construir um bloco, a transação será processada.

Além disso, há um limite máximo no período de geração de blocos, para que pelo menos um bloco seja proposto a cada 6 horas (independentemente do número de transações recolhidas pelo proponente).

## Com quem posso realizar transações? {#who-can-i-transact-with}
Para transferir ativos no Polygon Nightfall, basta o `Destination Wallet Address`. Leia o tutorial sobre carteira para entender [como compartilhar o seu Endereço de Carteira](../tools/nightfall-wallet.md#your-wallet-address) para receber fundos.

## Onde os compromissos são copiados? {#where-are-commitments-backed-up}

As provas de Conhecimento Zero são computadas no navegador para que as chaves secretas permaneçam consigo, e a carteira mantenha o controlo de todos os seus compromissos no IndexedDb. Qualquer pessoa com acesso a dados pode descobrir os seus compromissos, embora não possam roubá-los sem as suas chaves. As chaves só são descriptografadas quando entra no mnemónico. Assim, apenas deve usar a carteira numa máquina em que confie.

Por enquanto, estes dados não são exportados para nenhum lugar. Sendo assim, se usar um navegador numa máquina diferente, não terá acesso aos seus compromissos, a menos que transfira os conteúdos do IndexedDB. Fornecemos um mecanismo para exportar e importar compromissos através da carteira.

## Privacidade de transações {#privacy-of-transactions}
É importante entender que transações de depósito e retirada não são privadas. Isto porque interagem com a Camada 1 e a Camada 1 não é privada. Isto significa que todos sabem se criar um compromisso de Camada 2 e a quantia que ela contém. Da mesma forma, se retornar um token para a Camada 1 destruindo um compromisso de Camada 2, todos sabem quem o recebeu e o valor.

A privacidade vem inteiramente de transferências dentro da Camada 2. Do ponto de vista do blockchain Ethereum, elas são inteiramente privadas. Os únicos dados revelados são o seu endereço IP quando envia uma transação de transferência para um proponente de blocos. Para o Beta inicial, o Polygon executa os únicos proponentes.


## Como retirar fundos? {#how-to-withdraw-funds}
Os fundos podem ser retirados com uma carteira Polygon Nightfall. As retiradas têm um período de finalização **de uma semana** a partir do momento em que o bloco, incluindo a transação de retirada, foi criado. Uma vez decorrido este período de tempo, pode finalizar a retirada para enviar os seus fundos para a sua conta Ethereum.

## Quanto as transações custarão no Nightfall? {#how-much-will-transactions-cost-on-nightfall}
Existem dois tipos de transações que acarretam custos diferentes:

- Transações on-chain: estas transações são enviadas para o contrato inteligente e exigem taxas de gás no Ethereum para serem mineradas. Qualquer proponente pode colocar esta transação num bloco. Atualmente, `deposit` e `finalize withdrawal` são transações on-chain.
- Transações off-chain: estas transações são enviadas diretamente para o proponente. Atualmente, todos `transfer` e `withdrawals` estão configurados como transações off-chain.

## Que tokens posso usar na rede Nightfall? {#which-tokens-can-i-use-on-nightfall-network}
Os tokens a seguir estão operacionais no Nightfall:

- MATIC
- WETH
- DAI
- USDC

## Preciso de tokens MATIC para usar o Nightfall? {#do-i-need-matic-tokens-to-use-nightfall}
Sim. Terá de depositar alguns tokens MATIC no Nightfall para poder pagar por `transfers` e `withdrawals`.

## Onde posso enviar um relatório de bugs ou contactar Nightfall para ajuda adicional? {#where-can-i-submit-a-bug-report-or-contact-nightfall-for-additional-help}
A melhor maneira é entrar no [servidor de discord Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR) e enviar a sua pergunta.
