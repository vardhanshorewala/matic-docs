---
id: nightfall-wallet
title: Carteira Nightfall
sidebar: Nightfall Wallet
description: "Guia da carteira Polygon Nightfall."
keywords:
  - docs
  - matic
  - polygon
  - nightfall
  - wallet
image: https://matic.network/banners/matic-network-16x9.png

---

A carteira Polygon Nightfall é uma carteira de navegador que é capaz de interagir com o lançamento beta do Nightfall mainnet.

:::info Use a carteira Nightfall para fazer depósitos, transferências e retiradas

### Restrições {#restrictions}

Enquanto Nightfall atinge um estado maduro, as seguintes restrições são aplicáveis:


| Token ERC-20 | Depósito máximo | Retirada máxima |
|-------------|-------------|--------------|
| MATIC | 250 MATIC | 1000 MATIC |
| WETH | 0,25 WETH | 1 WETH |
| DAI | 250 DAI | 1000 DAI |
| USDT | 250 USDT | 1000 USDT |
| USDC | 250 USDC | 1000 USDC |

:::

:::caution Medidas de segurança

A carteira Nightfall é testada num navegador Chrome. Durante o Beta, a quilometragem pode variar noutros navegadores.

**Recomendamos vivamente que use o Nightfall no Chrome**.

:::



## Introdução {#getting-started}

Visite a [carteira mainnet](https://wallet-beta.polygon.technology) na web Polygon ou [carteira testnet](https://wallet.testnet.polygon-nightfall.technology/), conecte a sua conta MetaMask e selecione a carteira da Polygon à esquerda. Se precisar de ajuda com o MetaMask, consulte a [documentação do Polygon no MetaMask](../../develop/metamask/tutorial-metamask.md)

![](../imgs/tools-wallet/polygon-wallet-click-nf.png)

Neste ponto, a carteira irá pedir-lhe para mudar para a rede da Polygon e um pop-up MetaMask vai solicitar confirmação da mudança.

![](../imgs/tools-wallet/polygon-network.png)

Em seguida, na secção superior da carteira, clique no menu suspenso e selecione `Polygon Nightfall` e irá aparecer uma uma nova solicitação para mudar para Mainnet Ethereum. Aceite mudar para Mainnet Ethereum para operar com o Polygon Nightfall.

![](../imgs/tools-wallet/polygon-network-dropdown-nf.png)

Se estiver a trabalhar na testnet, o URL da carteira leva-o imediatamente para a página de destino da carteira Polygon Nightfall.

![](../imgs/tools-wallet/wallet-main-screen.png)

Na sua primeira visita, a sua carteira Nightfall terá que ser criada. Deverá aparecer um pop-up para gerar um mnemónico e criar a carteira. Clique em `Generate Mnemonic` e, em seguida, `Create Wallet`. **Note que apenas pode usar esta carteira no seu dispositivo atual**.

![](../imgs/tools-wallet/generate-mnemonic-create-wallet.png)

:::caution Faça o backup dos seus compromissos e mnemónicos

As chaves e transações da sua carteira são armazenadas no navegador (IndexedDb). Idêntico ao mnemónico que configurou quando acedeu à Carteira do Nightfall pela primeira vez.

Certifique-se de que armazena este mnemónico num lugar seguro. É a única forma de poder produzir provas compatíveis com os seus fundos na Camada 2. O mesmo acontece com os seus compromissos: certifique-se de que os armazena com segurança ao clicar `export commitments`sempre que utilizar outro navegador ou máquina.

:::

**Se perder os seus compromissos, os seus fundos são perdidos para sempre**


Neste ponto, deverá ser capaz de ver os seus endereços do MetaMask e da carteira Nightfall (canto superior direito).

**Aguarde mais alguns minutos para concluir a configuração da carteira antes de começar a executar transações**.

No canto inferior esquerdo da carteira, o estado da carteira aparecerá como `Syncing Nightfall`. Neste estado, a carteira está a recuperar os circuitos ZK e o estado da rede necessários para executar transações.

![](../imgs/tools-wallet/wallet-state-syncing.png)

Aguarde até o estado da carteira mudar para `Nightfall Synced`

![](../imgs/tools-wallet/wallet-state-synced.png)


## Como conectar uma carteira física de Ledger ao Nightfall {#how-to-connect-a-ledger-hardware-wallet-to-nightfall}
Existe um guia para conectar a sua carteira física de Ledger com MetaMask no site oficial do MetaMask [aqui](https://support.ledger.com/hc/en-us/articles/4404366864657-How-to-access-your-Ledger-Ethereum-ETH-account-via-Metamask?docs=true).

Certifique-se de conectar a aplicação Ethereum na sua carteira e permitir "assinatura cega" nas configurações da aplicação Ethereum.


### O seu endereço da carteira {#your-wallet-address}
Obtenha o seu endereço da carteira Nightfall a partir da página dos Ativos Nightfall clicando em `Receive`.

![](../imgs/tools-wallet/nightfall-wallet-address.png)

## Como fazer depósitos {#how-to-make-deposits}
Na página Ativos Nightfall, clique no botão `Deposit` à direita do ativo escolhido ou navegue para a página Bridge da Camada 2.

1. Verifique se o modo Transferência está definido para `Deposit`
2. Verifique se o token desejado está selecionado (WETH, MATIC etc.)
3. Introduza o valor a ser depositado na sua carteira Nightfall, clique `Transfer`
4. Reveja a transação no pop-up
5. Clique `Create Transaction`

![](../imgs/tools-wallet/deposit-click-transfer.png)

Será iniciado um processo para calcular ZKP e preparar a transação - conceda ao MetaMask acesso aos seus saldos de conta. Quando isto terminar, clique `Send Transaction` - conceda ao MetaMask mais permissões para interação do contrato.

![](../imgs/tools-wallet/deposit-tx-created-and-ready-to-be-sent.png)

Vá para a página Transações para [visualizar o seu depósito](#view-transactions).

### Informações importantes sobre os depósitos {#important-information-about-deposits}
- [Os valores dos depósitos são restritos](#note-the-following-deposit-and-withdrawal-restrictions) na versão Beta

## Como fazer transferências {#how-to-make-transfers}
Na página Ativos Nightfall, clique no botão `Send` à direita do ativo escolhido.

1. Introduza um endereço válido existente no Polygon Nightfall Camada 2
2. Verifique se o token desejado está selecionado (WETH, MATIC etc.)
3. Introduza o valor a ser transferido da sua carteira Nightfall, clique `Continue`

![](../imgs/tools-wallet/send-nf.png)

Será iniciado um processo para calcular ZKP e preparar a transação. Quando isto terminar, clique `Send Transaction`.

Vá para a página Transações para [visualizar a sua transferência](#view-transactions).

### Informações importantes sobre transferências {#important-information-about-transfers}
Os circuitos de transferências ZKP atuais utilizados no Nightfall restringem os valores de transferência para corresponder exatamente ao valor de um compromisso existente ou qualquer combinação linear de dois compromissos existentes.

Para ilustrar as restrições de transferência com um exemplo, observe os seguintes conjuntos de compromissos:

- Conjunto A: [1, 1, 1, 1, 1, 1]
- Conjunto B: [2, 2, 2]
- Conjunto C: [2, 4]

Embora os três conjuntos tenham somas totais equivalentes de 6, apenas as seguintes transferências estão disponíveis:

- Conjunto A: Qualquer transferência entre 0 e 2 (ambos excluídos)
- Conjunto B: Qualquer transferência entre 0 e 4 (ambos excluídos)
- Conjunto C: Qualquer transferência entre 0 e 6 (ambos excluídos)

Para continuar com o exemplo, se o Alex possui o Conjunto C de compromissos, as transferências disponíveis incluem qualquer valor entre 0 e 6, excluindo ambos os valores-limite. Se Alex decidir transferir 3,5 para Bob, o Alex passará a ter um único compromisso de 2,5, e Bob receberá um compromisso de 3,5 quando o bloco for proposto.

Por outro lado, se Alex decidir transferir um valor de 6 para Bob, a prova ZK vai falhar porque não haverá uma combinação válida de compromissos.

**É importante observar que estes valores representam compromissos detidos**, não, por exemplo, depósitos. Estão disponíveis informações adicionais na secção de [compromissos](../protocol/commitments.md) destes documentos.

## Como fazer retiradas {#how-to-make-withdrawals}
Na página Ativos Nightfall, clique no botão `Withdraw` à direita do ativo escolhido ou navegue para a página Bridge da Camada 2.

1. Verifique se o modo Transferência está definido para `Withdraw`
2. Verifique se o token desejado está selecionado (WETH, MATIC etc.)
3. Introduza o valor a ser retirado da carteira Nightfall, clique `Transfer`
4. Reveja a transação no pop-up
5. Clique `Create Transaction`

Será iniciado um processo para calcular ZKP e preparar a transação. Quando isto terminar, clique `Send Transaction`.

Vá para a página Transações para [visualizar a sua retirada](#view-transactions). Após o período de finalização de uma semana expirar, o utilizador poderá finalizar e solicitar o valor de retirada.

### Informações importantes sobre retiradas {#important-information-about-withdrawals}
- O valor de retirada deve corresponder exatamente ao valor num dos compromissos detidos (mais sobre [compromissos](#learn-about-commitments))
- As retiradas têm um período de finalização de **uma semana** a partir do momento em que o bloco, incluindo a transação de retirada, foi criado. Uma vez decorrido este período de tempo, pode finalizar a retirada para que os seus fundos sejam enviados para a sua conta Ethereum.
- [Os valores de retirada são restritos](#note-the-following-deposit-and-withdrawal-restrictions) na versão Beta
- As retiradas são uma transação on-chain e pagarão taxas de gás durante a solicitação de transação e também quando a retirada é finalizada.

![](../imgs/tools-wallet/cooling-off-vs-ready.png)

## Visualizar transações {#view-transactions}
Verifique o estado dos seus depósitos, transferências e retiradas na página Transações. Observe que cada transação é processada logo que existam transações suficientes para produzir um bloco ou após 6 horas.

![](../imgs/tools-wallet/transactions.png)
