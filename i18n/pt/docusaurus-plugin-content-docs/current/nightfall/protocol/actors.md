---
id: actors
title: Intervenientes
sidebar_label: Actors
description: "Tipos de intervenientes no Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - transactor
  - proposer
  - challenger
  - liquidity
  - provider
image: https://matic.network/banners/matic-network-16x9.png
---

Existem quatro intervenientes envolvidos na rede:

- [Operadores](#transactor)
- [Proponentes](#proposer)
- [Desafiadores](#challenger)

## Operador {#transactor}
Um Operador é um cliente regular do serviço. Pretendem efetuar transações, ou seja, depósito, transferência e retirada de forma privada. Normalmente, estes clientes usarão uma carteira web ou um servidor dedicado (Cliente) para executar as provas ZK necessárias para gerar as transações.

## Proponente {#proposer}
Um Proponente recolhe as transações de clientes e propõe novas atualizações ao estado do contrato Shield. Por estado, queremos dizer especificamente as variáveis de armazenamento associadas a uma transação ZKP: nulificadores e raízes de compromisso. As propostas de atualização contêm várias transações integradas num Bloco de Camada 2. Apenas um hash do estado final que existiria depois de todas as transações no Bloco serem processadas é armazenado na chain. As transações tornam-se definitivas após um período de uma semana.

Qualquer pessoa pode se tornar um Proponente, mas deve postar algum stake. O stake destina-se a incentivar um bom comportamento. Os Proponentes ganham dinheiro fornecendo blocos corretos, recolhendo taxas de operadores. São um pouco análogos aos Mineradores num blockchain convencional.

## Desafiador {#challenger}
Um Desafiador supervisiona a exatidão de blocos propostos no prazo de uma semana após o bloco ter sido submetido. Qualquer pessoa pode ser um Desafiador. Os Desafiadores utilizam o stake postado por proponentes ao construir os seus blocos quando enviam com sucesso um desafio.


## Notas {#notes}
Na implementação de referência da Polygon, tanto o Proponente como o Desafiador descarregam algumas funcionalidades para um módulo comum chamado Optimist. Este módulo Optimist fornece alguns serviços a vários Proponentes e Desafiadores, tal como gerar e desafiar blocos (Proponente e Desafiadores precisariam de assinar estas transações), sincronizando com eventos de blockchain, etc.

Para além dos intervenientes descritos acima, há um interveniente adicional chamado Cliente. Um Cliente atua como um serviço de confiança que recolhe as transações do utilizador, executa as provas ZK em seu nome, envia transações para o Proponente, presta atenção a eventos blockchain etc. Em resumo, o Cliente atua como um retransmissor de confiança para um grupo de utilizadores que quer descarregar computação de prova pesada e que confiam uns nos outros.

A alternativa ao Cliente é usar a carteira de navegador, um serviço sem servidor fornecido pela Polygon. Esta carteira gere todas as atividades de transação para um único utilizador e, ao mesmo tempo, mantém a privacidade.
