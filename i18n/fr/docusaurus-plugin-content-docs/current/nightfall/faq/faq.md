---
id: faq
title: FAQ
sidebar_label: FAQ
description: Foire aux questions sur Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip

Si vous ne trouvez pas votre question dans cette liste, veuillez soumettre votre question sur le <ins>**[serveur discord Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR)**</ins>.

:::

## Où puis-je trouver les contrats intelligents ? {#where-can-i-find-the-smart-contracts}

Les contrats Polygon Nightfall ont été déployés dans le [testnet Goerli](../deployments/testnet.md) et dans le [mainnet](../deployments/mainnet.md).

## Quel est l'état de l'audit de sécurité de Polygon Nightfall ? {#what-s-the-state-of-polygon-nightfall-s-security-audit}
Polygon Nightfall fait actuellement l'objet d'un audit de sécurité qui devrait être terminé au cours du troisième trimestre. Entre-temps, plusieurs restrictions ont été ajoutées au protocole :

- Proposant unique en cours de fonctionnement et géré par Polygon
- [Montants de dépôt et de retrait limités](../tools/nightfall-wallet.md#deposit-and-withdraw-restrictions)

## Comment configurer mon portefeuille Nightfall ? {#how-do-i-set-up-my-nightfall-wallet}
Il existe un tutoriel complet sur le portefeuille [ici](../tools/nightfall-wallet.md) avec tous les détails sur la façon de commencer avec un portefeuille Polygon Nightfall.

## Comment puis-je connecter un portefeuille matériel Ledger au portefeuille Nightfall ? {#how-do-i-connect-a-ledger-hardware-wallet-to-nightfall-wallet}
Il y a une section dans le tutoriel sur le portefeuille qui explique [comment connecter un portefeuille matériel Ledger avec Metamask](../tools/nightfall-wallet.md#how-to-connect-a-ledger-hardware-wallet-to-nightfall).

## Combien de temps les transferts prennent-ils sur le réseau Polygon Nightfall du début à la fin ? {#how-long-do-transfers-take-on-polygon-nightfall-network-from-start-to-finish}
Le proposant actuel prend les transactions des utilisateurs et fait des blocs jusqu'à 32 transactions. Dès que suffisamment de transactions sont collectées pour construire un bloc, la transaction est traitée.

En outre, il y a une limite supérieure à la période de génération de bloc de sorte qu'au moins un bloc est proposé toutes les 6 heures (quel que soit le nombre de transactions collectées par le proposant).

## Avec qui puis-je faire des transactions ? {#who-can-i-transact-with}
Pour transférer des actifs dans Polygon Nightfall, on a uniquement besoin de `Destination Wallet Address`. Lisez le tutoriel sur le portefeuille pour savoir [comment partager votre adresse de portefeuille](../tools/nightfall-wallet.md#your-wallet-address) pour recevoir des fonds.

## Où les engagements sont-ils sauvegardés ? {#where-are-commitments-backed-up}

Les preuves à divulgation nulle de connaissance sont calculées dans le navigateur, de sorte que vos clés secrètes restent avec vous, et le portefeuille garde une trace de tous les engagements que vous possédez, dans son IndexedDb. Toute personne ayant accès à ces données peut savoir quels engagements vous possédez, bien qu'elle ne puisse pas les voler sans vos clés. Les clés ne sont décryptées que lorsque vous entrez dans la mnémonique. Ainsi, vous devriez uniquement utiliser le portefeuille sur une machine en laquelle vous avez confiance.

Pour l'instant, ces données ne sont exportées nulle part. Ainsi, si vous utilisez un navigateur sur une autre machine, vous n'aurez accès à vos engagements que si vous transférez les contenus IndexedDB. Nous fournissons un mécanisme pour exporter et importer des engagements dans le portefeuille.

## Confidentialité des transactions {#privacy-of-transactions}
Il est important de comprendre que les opérations de dépôt et de retrait ne sont pas privées. En effet, elles interagissent avec la couche 1 et la couche 1 n'est pas privée. Cela signifie que tout le monde sait que vous créez un engagement de couche 2 et combien il contient. De même, si vous renvoyez un jeton à la couche 1 en détruisant un engagement de couche 2, tout le monde sait qui l'a reçu et combien.

La confidentialité provient entièrement des transferts au sein de la couche 2. Du point de vue de la blockchain Ethereum, ceux-ci sont entièrement privés. La seule donnée divulguée est votre adresse IP, lorsque vous envoyez une transaction de transfert à un proposant de bloc. Pour les premières versions bêta, Polygon gère les seuls proposants.


## Comment retirer des fonds ? {#how-to-withdraw-funds}
Les fonds peuvent être retirés avec le portefeuille Polygon Nightfall. Les retraits ont une période de finalisation d'**une semaine** à partir du moment où le bloc comprenant la transaction de retrait a été créé. Une fois ce délai écoulé, vous pouvez finaliser le retrait pour que vos fonds soient envoyés à votre compte Ethereum.

## Combien coûteront les transactions sur Nightfall ? {#how-much-will-transactions-cost-on-nightfall}
Il existe deux types de transactions qui ont des coûts différents :

- Transactions sur la chaîne : ces transactions sont envoyées au contrat intelligent et nécessitent des frais de gaz sur Ethereum pour être minées. N'importe quel proposant peut prendre cette transaction et la mettre dans un bloc. Actuellement, `deposit` et `finalize withdrawal` sont des transactions sur la chaîne.
- Transactions hors chaîne : ces transactions sont envoyées directement au proposant. Actuellement, tous les `transfer` et `withdrawals` sont configurés comme des transactions hors chaîne.

## Quels jetons puis-je utiliser sur le réseau Nightfall ? {#which-tokens-can-i-use-on-nightfall-network}
Les jetons suivants sont opérationnels sur Nightfall :

- MATIC
- WETH
- DAI
- USDC

## Ai-je besoin de jetons MATIC pour utiliser Nightfall ? {#do-i-need-matic-tokens-to-use-nightfall}
Oui. Vous devrez déposer quelques jetons MATIC sur Nightfall pour pouvoir payer pour `transfers` et `withdrawals`.

## Où puis-je soumettre un rapport de bug ou contacter Nightfall pour obtenir de l'aide supplémentaire ? {#where-can-i-submit-a-bug-report-or-contact-nightfall-for-additional-help}
La meilleure façon est de rejoindre notre [serveur discord Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR) et de soumettre votre question.
