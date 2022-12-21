---
id: commitments
title: Engagements et nullificateurs
sidebar_label: Commitment and Nullifiers
description: "Transfert simple et double."
keywords:
  - docs
  - polygon
  - nightfall
  - commitment
  - nullifier
image: https://matic.network/banners/matic-network-16x9.png
---


## Que sont les engagements ? {#what-are-commitments}
Un engagement est une primitive cryptographique qui permet à un utilisateur de s'engager sur une valeur choisie
tout en le cachant aux autres, avec la possibilité de révéler la valeur engagée plus tard.
La confidentialité de la valeur et du destinataire est atteinte de cette manière.

Chaque fois qu'un utilisateur effectue une transaction à l'aide de Nightfall, le portefeuille du navigateur calcule une
Preuve à divulgation nulle de connaissance (ZKP) et crée (ou annule) un engagement.
Par exemple, vous créez un engagement lorsque vous effectuez un dépôt ou un transfert et annulez un engagement lorsque vous
effectuez un transfert ou un retrait.

Le calcul ZKP s'appuie sur des [circuits](../protocol/circuits.md) qui définissent les règles qu'une
la transaction doit suivre pour être correcte.

L'engagement est utilisé pour masquer les propriétés suivantes :
- **Adresse ERC du jeton**
- **Identifiant du jeton**
- **Valeur**
- **Propriétaire**

Les engagements sont stockés dans une structure *arbre de Merkle*. La racine de cet *arbre de Merkle* est stockée sur la chaîne.

![](../imgs/commitment.png)

### UTXO {#utxo}
Les engagements sont créés pendant les dépôts et les transferts, et sont dépensés pendant les transferts et les retraits. **Les engagements ne sont pas agrégés ensemble**. Lors de la dépense d'un engagement, la valeur de l'engagement dépensé est limitée à la valeur d'un maximum de deux engagements détenus.

Les circuits de transfert et de retrait ZKP actuels utilisés dans Nightfall sont limités à 2 entrées - 2 sorties (transfert/retrait d'engagement et changement) hors paiements.
Si l'ensemble des engagements d'un acteur contient principalement des engagements de faible valeur (résidu), il peut être difficile pour lui d'effectuer des transferts futurs.

Observez les ensembles de valeurs suivants

- **Ensemble A** : [1, 1, 1, 1, 1, 1]
- **Ensemble B** : [2, 2, 2]
- **Ensemble C** : [2, 4]

Alors que les trois ensembles ont des sommes totales équivalentes, le transfert de valeur maximale qui peut être traité par les ensembles *A*, *B* et *C* est respectivement de 2, 4 et 6. C'est l'une des raisons pour lesquelles les grandes valeurs d'engagement sont préférées. La stratégie de sélection des engagements utilisée atténue ce risque en donnant la priorité à l'utilisation d'engagements de faible valeur, tout en minimisant la création d'engagements relatifs aux résidus.


## Que sont les nullificateurs ? {#what-are-nullifiers}
Un **nullificateur** est le résultat de la combinaison d'un engagement et de la clé du nullificateur. Une fois que le nullificateur est diffusé sur la chaîne, l'engagement est considéré comme dépensé.
Les nullificateurs sont stockés sur la chaîne dans le cadre des données d'appel pendant la proposition de bloc.

![](../imgs/nullifier.png)



