---
id: contracts
title: Contrats intelligents
sidebar_label: Smart Contracts
description: "Bouclier, proposants, challenges et calculs de l'arbre de Merkle."
keywords:
  - docs
  - polygon
  - nightfall
  - smart
  - contracts
  - shield
image: https://matic.network/banners/matic-network-16x9.png
---

Les contrats définissent les règles que chaque acteur Nightfall doit suivre pour fonctionner dans le réseau.
Les contrats intelligents comprennent :

- [Shield.sol](#shield)
- [Proposers.sol](#proposers)
- [Challenges.sol](#challenges)
- [MerkleTree_Computations.sol](#merkletree_computations)

## Shield {#shield}
Ce contrat permet à un utilisateur d'envoyer une transaction pour être traitée par un proposant. S'il s'agit d'une transaction de dépôt, elle acceptera le paiement.
Elle permet également à quiconque de demander la mise à jour de l'état du contrat Shield (listes root et nullificateur d'engagement).
Une fois l'état mis à jour, tous les retraits dans la mise à jour sont traités.

Il n'y a aucun besoin fondamental de poster une transaction de transfert ou de retrait dans la blockchain : il s'agit simplement d'agir comme un forum pour
que les proposants puissent récupérer la transaction et l'incorporer dans un bloc de couche 2.

Étant donné que Nightfall interagit avec de véritables contrats ERC, les contrôles suivants ne peuvent pas être rendus privés :

- Pendant le **dépôt/retrait**, l'adresse du jeton ERC est valide.
- Pendant le **dépôt**, l'utilisateur a un solde ou possède un jeton pour créer un engagement.

## Proposants {#proposers}
Le contrat inclut une fonctionnalité pour l'enregistrement, le désenregistrement, le paiement et la rotation des proposants, et la proposition d'un nouveau bloc de couche 2 à la blockchain.
La première version de Nightfall n'accepte qu'un seul proposant de démarrage exploité par Polygon. Dans les versions à venir, cette restriction sera levée là où plusieurs proposants seront autorisés.

## Challenges {#challenges}
La fonctionnalité permet à un bloc d'être contesté comme incorrect.

## MerkleTree_Stateless {#merkletree_stateless}
Une version sans état (fonction pure) du `MerkleTree.sol` original, utilisée par `Challenges.sol` pour aider à calculer les challenges de bloc sur la chaîne.

## Autres contrats {#other-contracts}
- `Utils.sol` - rassemble des fonctionnalités qui sont soit utilisées dans plusieurs contrats, soit, si elles sont laissées en ligne, affecteraient la lisibilité du code.
- `Config.sol` - contient des constantes, similaires à un fichier de configuration Node.js.
- `Structures.sol` - définit les structures globales, les énumérations, les événements, les mappages et les variables d'état. Cela facilite la recherche.

## Évolutivité {#upgradability}
Au moins dans un premier temps, Polygon conserve la possibilité de mettre à niveau les contrats Nightfall après le déploiement.
Pour ce faire, nous utilisons les [plugins de mise à niveau](https://docs.openzeppelin.com/upgrades-plugins/1.x/) Openzeppelin pour Truffle.

Polygon utilise un module de [déploiement](https://github.com/EYBlockchain/nightfall_3/tree/master/nightfall-deployer) pour mettre à niveau les contrats.
Le `deployer` a 4 migrations stockées dans son dossier de migration.
Les trois premières migrations effectuent un déploiement « normal » de la suite de contrats Polygon Nightfall. Elles
s'assurent cependant que tous les contrats (mais pas les bibliothèques) sont déployés avec un proxy pour leur permettre
d'être mis à niveau à une date ultérieure. La quatrième migration est utilisée pour améliorer les contrats.
