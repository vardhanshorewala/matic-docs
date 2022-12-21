---
id: actors
title: Acteurs
sidebar_label: Actors
description: "Types d'acteurs sur Nightfall"
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

Il y a quatre acteurs impliqués dans le réseau :

- [Transacteurs](#transactor)
- [Proposants](#proposer)
- [Challengers](#challenger)

## Transacteur {#transactor}
Un transacteur est un client régulier du service. Ils souhaitent effectuer des transactions, c'est-à-dire effectuer des dépôts, des transferts et des retraits à titre privé.
Ces clients utilisent généralement un portefeuille web ou un serveur dédié (Client) pour effectuer les preuves à divulgation nulle de connaissance requises pour générer les transactions.

## Proposant {#proposer}
Un proposant collecte les transactions auprès des clients et propose de nouvelles mises à jour de l'état du
contrat Shield.
Par état, nous entendons spécifiquement les variables de stockage associées à une transaction de preuve à divulgation nulle de connaissance :
les nullificateurs et les roots d'engagement.
Les propositions de mise à jour contiennent plusieurs transactions, regroupées dans un bloc de couche 2. Seul un hachage
de l'état final qui existerait après le traitement de toutes les transactions dans le bloc
est stocké sur la chaîne. Les transactions deviennent définitives au bout d'une semaine.

N'importe qui peut devenir un proposant, mais il doit poster un stake. Le stake est destiné à inciter à la bonne conduite.
Les proposants gagnent de l'argent en fournissant des blocs corrects, en collectant des frais auprès des opérateurs. Ils sont quelque peu analogues aux mineurs dans une blockchain conventionnelle.

## Challenger {#challenger}
Un challenger supervise l'exactitude des blocs proposés dans la semaine suivant la soumission du bloc. N'importe qui peut être un challenger.
Les challengers prennent le stake posté par les proposants lorsqu'ils construisent leurs blocs, lorsqu'ils envoient avec succès un challenge.


## Remarques {#notes}
Dans l'implémentation de référence de Polygon, le proposant et le challenger déchargent certaines fonctionnalités vers un module commun appelé Optimist.
Ce module Optimist fournit certains services à un certain nombre de proposants et de challengers, tels que la génération et la contestation de blocs
(Les proposants et les challengers devront signer ces transactions), en synchronisation avec les événements de la blockchain, etc.

Outre les acteurs décrits ci-dessus, il existe un acteur supplémentaire appelé Client. Un client agit comme un service de confiance qui collecte les transactions des utilisateurs, effectue les preuves à divulgation nulle de connaissance en leur nom, envoie les transactions au proposant, écoute les événements de la blockchain, etc. En résumé, le client agit en tant que relayeur de confiance pour une collection d'utilisateurs qui veulent décharger des calculs de preuve lourds et qui se font confiance.

L'alternative pour le client est d'utiliser le portefeuille du navigateur, un service sans serveur fourni par Polygon. Ce portefeuille gère toutes les activités de transaction pour un seul utilisateur, tout en préservant la confidentialité.
