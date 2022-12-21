---
id: overview
title: Visão geral
sidebar_label: Overview
description: Uma visão geral do Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - privacy
  - rollup
  - zk
image: https://matic.network/banners/matic-network-16x9.png
---

A Polygon acredita que no futuro próximo ver-se-á muitas empresas interagindo entre si através de contratos inteligentes para executar a lógica de negócios e gerir a troca de bens e serviços.

Em colaboração com a [Ernst & Young](https://blockchain.ey.com/), a Polygon oferece uma solução de rollup pública, de Camada 2, centrada em privacidade chamada Polygon Nightfall para habilitar acessibilidade e privacidade para empresas que pretendem usar Ethereum.

## Um protocolo ZK-Proof para empresas {#a-zk-proof-protocol-for-enterprises}

O Polygon Nightfall faz parte de um conjunto de soluções de escalabilidade da Polygon, que inclui [Polygon Hermez](https://polygon.technology/solutions/polygon-hermez/),
[Polygon Miden](https://polygon.technology/solutions/polygon-miden/)
e [Polygon Zero](https://polygon.technology/solutions/polygon-zero/).
A principal diferença é que o Nightfall é um rollup centrado na privacidade, concebido para casos de utilização empresarial, combinando os conceitos de rollups otimistas e criptografia Zero-Knowledge (ZK) para oferecer transações privadas e escaláveis.

Embora o Nightfall permita escalabilidade, também está definido para remover uma grande barreira que as empresas enfrentam hoje ao usar blockchain: a falta de privacidade de transações. O Nightfall adiciona uma camada de privacidade para que os parâmetros chave de transação (ou seja, valor e destino) não possam ser rastreados. Estes dois recursos alimentaram o interesse de empresas privadas que consideram o Nightfall como uma maneira de executar a sua lógica de negócios e coordenar com a sua cadeia de alimentação numa rede descentralizada a um preço sustentável, tudo isso enquanto mantém segurança e privacidade.

## Pilares do Nightfall {#nightfall-s-pillars}

A principal proposta de valor do Polygon Nightfall é permitir transferências seguras, privadas e de baixo custo de dados numa rede descentralizada.

![](../imgs/overview.png)

## Privacidade {#privacy}

O Polygon Nightfall usa provas ZK para enviar transações privadas. Um utilizador pode gerar uma prova ZK da transação sem revelar parâmetros chave de transação como o destino ou o valor da transação. Mais detalhes sobre o componente de privacidade do Nightfall estão disponíveis no guia de [protocolo](../protocol/protocol.md).

## Segurança {#security}

> O Nightfall está atualmente a ser submetido a uma auditoria de segurança que se espera estar concluída em meados de junho de 2022. Quando o processo de auditoria estiver concluído, os resultados serão publicados aqui.

> Como uma nova rede com um período de bootstrap, o Nightfall tem medidas de segurança transitórias para proteger o sistema com o objetivo de remover e deixar totalmente descentralizado.

O Polygon Nightfall é uma construção de Camada 2 porque tira partido do Ethereum usando a sua segurança como um blockchain robusto e público. O Nightfall depende de certos pressupostos que garantem a recuperação de ativos. Esses pressupostos são baseados em várias decisões de design e arquitetura que giram em torno do ZK-SNARKS, que usam determinados primitivos criptográficos, como hashes e assinaturas. Finalmente, o Nightfall incorpora regras de operação em diferentes contratos inteligentes para garantir que os operadores não bloqueiam as transações de utilizador e que os utilizadores possam retirar os seus ativos em qualquer altura.

Em resumo, o Nightfall faz os seguintes pressupostos de segurança:

1. Pressupostos de segurança do Ethereum.
2. Pressupostos do Groth16 (conhecimento de pressuposto exponente).
3. Determinados pressupostos criptográficos de primitivos como hashes (Poseidon) e assinaturas.
4. Pressupostos de segurança de software que dependem de design e implementação corretos.

## Eficiência {#efficiency}

Os proponentes de blocos recolhem transações de vários utilizadores e agrupam-nos num bloco de L2. Os tamanhos padrão do bloco L2 contêm cerca de 32 transações.

Os custos de gás esperados para um depósito, transferência e retirada são 9000, 1200 e 9500. Este custo é devido para armazenar 574 Bytes de calldata por transação, além de calldata fixo e computação para processar um bloco L2. Os custos serão até 80% menores após [EIP 4488](https://eips.ethereum.org/EIPS/eip-4488).

## Transferências não negáveis {#non-deniable-transfers}

Como parte da prova de ZK de transação de transferência, o Nightfall inclui criptografar os segredos (endereço de token, valor, identificação e sal) necessários para processar o compromisso transferido. Isso força o utilizador a criptografar os segredos com uma chave conhecida pelo destinatário. Como a chave faz parte da prova ZK, o destinatário apoia-se em negação plausível visto que o remetente pode provar que a chave de criptografia correta foi usada.

## Descentralização {#decentralization}

Os Validadores e os [Desafiadores](docs/nightfall/protocol/actors) são parte integrante do Nightfall. Asseguram que as transações e os blocos L2 produzem de forma atempada e correta. Um mecanismo de consenso baseado em Proof of Stake (PoS) é usado para selecionar o próximo [Proponente](docs/nightfall/protocol/actors) da rede. Por outro lado, os Desafiadores monitorizam o funcionamento correto da rede ao lançar desafios quando um bloco incorreto é detetado e ao reter o stake avançado pelo Proponente.


## Prova futura {#future-proof}
Graças à flexibilidade fornecida pela implementação do Optimistic rollup do Nightfall, é possível incluir novas transações no futuro sem comprometer as transações existente apenas definindo e registando um novo tipo de circuito que implementou a transação em ZK.

## Referências {#references}

1. [Uma abordagem multilateral ao escalonamento ZK](https://messari.io/article/polygon-a-multi-sided-approach-to-zk-scaling)
2. [A visão de Paul Brody sobre o Nightfall](https://www.linkedin.com/pulse/say-hello-nightfall-paul-brody-1f/)
