---
id: nightfall-wallet
title: Portefeuille Nightfall
sidebar: Nightfall Wallet
description: "Guide du portefeuille Polygon Nightfall."
keywords:
  - docs
  - matic
  - polygon
  - nightfall
  - wallet
image: https://matic.network/banners/matic-network-16x9.png

---

Le portefeuille Polygon Nightfall est un portefeuille de navigateur capable d'interagir avec la
version bêta du mainnet Nightfall.

:::info Utiliser le portefeuille Nightfall pour effectuer des dépôts, des transferts et des retraits

### Restrictions {#restrictions}

Pendant que Nightfall atteint un état de maturité, les restrictions suivantes sont appliquées :


| Jeton ERC20 | Dépôt max. | Retrait max. |
|-------------|-------------|--------------|
| MATIC | 250 MATIC | 1000 MATIC |
| WETH | 0,25 WETH | 1 WETH |
| DAI | 250 DAI | 1000 DAI |
| USDT | 250 USDT | 1000 USDT |
| USDC | 250 USDC | 1000 USDC |

:::

:::caution Mesures de sécurité

Le portefeuille Nightfall est testé sur un navigateur Chrome. Sur la version bêta, le kilométrage peut varier d'un navigateur
à l'autre.

**Nous vous recommandons fortement d'utiliser Nightfall sur Chrome**.

:::



## Commencer {#getting-started}

Visitez le [portefeuille du mainnet](https://wallet-beta.polygon.technology) du web Polygon ou
[le portefeuille du testnet](https://wallet.testnet.polygon-nightfall.technology/), connectez votre compte MetaMask
et sélectionnez le portefeuille de Polygon à gauche. Si vous avez besoin d'aide à propos de MetaMask, reportez-vous à la
[documentation Polygon sur MetaMask](../../develop/metamask/tutorial-metamask.md)

![](../imgs/tools-wallet/polygon-wallet-click-nf.png)

À ce stade, le portefeuille vous invitera à basculer vers le réseau Polygon, et une fenêtre contextuelle Metamask
demandera de confirmer le basculement.

![](../imgs/tools-wallet/polygon-network.png)

Ensuite, dans la section supérieure du portefeuille, cliquez sur le menu déroulant et sélectionnez `Polygon Nightfall`, et une
nouvelle demande de basculement vers le mainnet d'Ethereum apparaîtra. Veuillez accepter de passer au mainnet d'Ethereum
pour utiliser Polygon Nightfall.

![](../imgs/tools-wallet/polygon-network-dropdown-nf.png)

Si vous travaillez sur un testnet, l'URL du portefeuille vous mènera immédiatement à la page d'accueil du portefeuille Polygon Nightfall.

![](../imgs/tools-wallet/wallet-main-screen.png)

Lors de votre première visite, votre portefeuille Nightfall devra être créé. Une fenêtre contextuelle devrait apparaître pour générer une mnémonique et créer le portefeuille. Cliquez sur `Generate Mnemonic`, puis sur `Create Wallet`. **Notez que vous pouvez uniquement utiliser ce portefeuille sur votre appareil actuel**.

![](../imgs/tools-wallet/generate-mnemonic-create-wallet.png)

:::caution Sauvegardez vos engagements et vos mnémoniques

Vos clés de portefeuille et vos transactions sont stockées dans le navigateur (IndexedDb). C'est identique à la mnémonique que vous avez configurée lorsque vous accédez au portefeuille Nightfall pour la première fois.

Veillez à stocker cette mnémonique en lieu sûr. C'est la seule façon de pouvoir produire des preuves compatibles avec vos fonds sur L2. Il en va de même pour vos engagements : assurez-vous de les stocker en toute sécurité en appuyant sur `export commitments` chaque fois que vous utilisez un autre navigateur ou une autre machine.

:::

**Si vous perdez vos engagements, vos fonds sont perdus à jamais**


À ce stade, vous devriez être en mesure de voir à la fois votre Metamask et vos adresses de portefeuille Nightfall (en haut à droite).

**Patientez quelques minutes supplémentaires jusqu'à ce que la configuration du portefeuille soit terminée avant de commencer à effectuer des transactions**.

Dans le coin inférieur gauche du portefeuille, l'état du portefeuille s'affichera comme `Syncing Nightfall`. Dans cet état, le portefeuille récupère les
circuits ZK et l'état du réseau requis pour effectuer les transactions.

![](../imgs/tools-wallet/wallet-state-syncing.png)

Veuillez patienter jusqu'à ce que le statut du portefeuille passe à `Nightfall Synced`

![](../imgs/tools-wallet/wallet-state-synced.png)


## Comment connecter un portefeuille matériel Ledger à Nightfall {#how-to-connect-a-ledger-hardware-wallet-to-nightfall}
Il y a un guide pour connecter votre portefeuille matériel Ledger à Metamask sur le site officiel de Metamask [ici](https://support.ledger.com/hc/en-us/articles/4404366864657-How-to-access-your-Ledger-Ethereum-ETH-account-via-Metamask?docs=true).

Assurez-vous de connecter l'application Ethereum dans votre portefeuille et d'activer la « signature aveugle » dans les paramètres de l'application Ethereum.


### Votre adresse de portefeuille {#your-wallet-address}
Obtenez votre adresse de portefeuille Nightfall à partir de la page Actifs Nightfall en cliquant sur `Receive`.

![](../imgs/tools-wallet/nightfall-wallet-address.png)

## Comment effectuer des dépôts {#how-to-make-deposits}
À partir de la page Actifs Nightfall, cliquez sur le bouton `Deposit` à droite de l'actif choisi ou accédez à la page Pont L2.

1. Vérifiez que le mode de transfert est défini sur `Deposit`
2. Vérifiez que le jeton souhaité est sélectionné (WETH, MATIC, etc.)
3. Saisissez la valeur à déposer dans votre portefeuille Nightfall, cliquez sur `Transfer`
4. Vérifiez la transaction dans la fenêtre contextuelle
5. Cliquez sur `Create Transaction`

![](../imgs/tools-wallet/deposit-click-transfer.png)

Un processus démarrera pour calculer la preuve à divulgation nulle de connaissance et préparer la transaction - accordez à Metamask l'accès aux soldes de votre compte. Une fois que cela est terminé, cliquez sur `Send Transaction` - accordez à Metamask d'autres autorisations pour l'interaction contractuelle.

![](../imgs/tools-wallet/deposit-tx-created-and-ready-to-be-sent.png)

Accédez à la page Transactions pour [afficher votre dépôt](#view-transactions).

### Informations importantes sur les dépôts {#important-information-about-deposits}
- [Les montants des dépôts sont restreints](#note-the-following-deposit-and-withdrawal-restrictions) pendant la phase bêta

## Comment effectuer des transferts {#how-to-make-transfers}
À partir de la page Actifs Nightfall, cliquez sur le bouton `Send` à droite de l'actif choisi.

1. Saisissez une adresse valide existante sur Polygon Nightfall L2.
2. Vérifiez que le jeton souhaité est sélectionné (WETH, MATIC, etc.)
3. Saisissez la valeur à transférer de votre portefeuille Nightfall, cliquez sur `Continue`

![](../imgs/tools-wallet/send-nf.png)

Un processus démarrera pour calculer la preuve à divulgation nulle de connaissance et préparer la transaction. Une fois cela terminé, cliquez sur `Send Transaction`.

Accédez à la page Transactions pour [afficher votre transfert](#view-transactions).

### Informations importantes sur les transferts {#important-information-about-transfers}
Les circuits de transfert de preuve à divulgation nulle de connaissance actuels utilisés dans Nightfall limitent les montants de transfert pour qu'ils correspondent exactement à la valeur
d'un engagement existant, ou d'une combinaison linéaire de deux engagements existants.

Pour illustrer les restrictions de transfert avec un exemple, observez les ensembles d'engagements suivants :

- Ensemble A : [1, 1, 1, 1, 1, 1]
- Ensemble B : [2, 2, 2]
- Ensemble C : [2, 4]

Quand les trois ensembles ont des sommes totales équivalentes de 6, seuls les transferts suivants sont disponibles :

- Ensemble A : tout transfert entre 0 et 2 (les deux sont exclus)
- Ensemble B : tout transfert entre 0 et 4 (les deux sont exclus)
- Ensemble C : tout transfert entre 0 et 6 (les deux sont exclus)

Pour continuer avec l'exemple, si Alex possède l'ensemble C d'engagements, les transferts disponibles incluent tout montant compris entre 0 et 6, à l'exclusion des deux valeurs limites. Si Alex décide de transférer 3,5 à Bob, Alex se retrouvera avec un seul engagement de 2,5 et Bob recevra un engagement de 3,5 une fois le bloc proposé.

En revanche, si Alex décide de transférer un montant de 6 à Bob, la preuve à divulgation nulle de connaissance échouera, car il n'y aura pas de combinaison valide d'engagements.

**Il est important de noter que ces valeurs représentent des engagements détenus**, et non, par exemple, des dépôts. De plus amples informations sont disponibles dans la section [engagements](../protocol/commitments.md) de ces documents.

## Comment effectuer des retraits {#how-to-make-withdrawals}
À partir de la page Actifs Nightfall, cliquez sur le bouton `Withdraw` à droite de l'actif choisi ou accédez à la page Pont L2.

1. Vérifiez que le mode de transfert est défini sur `Withdraw`
2. Vérifiez que le jeton souhaité est sélectionné (WETH, MATIC, etc.)
3. Saisissez la valeur à transférer de votre portefeuille Nightfall, cliquez sur `Transfer`
4. Vérifiez la transaction dans la fenêtre contextuelle
5. Cliquez sur `Create Transaction`

Un processus démarrera pour calculer la preuve à divulgation nulle de connaissance et préparer la transaction. Une fois cela terminé, cliquez sur `Send Transaction`.

Accédez à la page Transactions pour [afficher votre retrait](#view-transactions). À l'expiration de la période de finalisation d'une semaine, l'utilisateur sera
en mesure de finaliser et de demander le montant du retrait.

### Informations importantes sur les retraits {#important-information-about-withdrawals}
- La valeur de retrait doit correspondre exactement au montant de l'un des engagements détenus (en savoir plus [sur les engagements](#learn-about-commitments))
- Les retraits ont une période de finalisation d'**une semaine** à partir du moment où le bloc comprenant la transaction de retrait a été créé. Une fois cette période écoulée, vous pouvez finaliser le retrait pour que vos fonds soient envoyés à votre compte Ethereum.
- [Les montants des retraits sont limités](#note-the-following-deposit-and-withdrawal-restrictions) pendant la phase bêta
- Les retraits sont une transaction sur la chaîne, les frais de gaz sont dus pendant la demande de transaction et également lorsque le retrait est finalisé.

![](../imgs/tools-wallet/cooling-off-vs-ready.png)

## Afficher les transactions {#view-transactions}
Vérifiez l'état de vos dépôts, transferts et retraits sur la page Transactions. Notez que chaque transaction est traitée dès qu'il y a suffisamment de transactions pour produire un bloc ou après 6 heures.

![](../imgs/tools-wallet/transactions.png)
