---
id: protocol
title: Protocole Nightfall
sidebar_label: Nightfall Protocol
description: "Le processus Nightfall."
keywords:
  - docs
  - polygon
  - nightfall
  - protocol
  - chain
  - block
  - structure
  - layer
image: https://matic.network/banners/matic-network-16x9.png
---

Nous supposons qu'au moins 1 proposant s'est inscrit au système, enregistrant un stake minimal.

## Enregistrement des transactions {#transaction-posting}
Il existe deux mécanismes pour enregistrer de nouvelles transactions :

- [Sur chaîne](#on-chain)
- [Hors chaîne](#off-chain)

### Sur chaîne {#on-chain}
Le processus commence par la création d'une transaction par un transacteur en appelant `submitTransaction` sur `Shield.sol`. Le transacteur paie des frais au contrat Shield pour la transaction, en fonction de ce que le transacteur décide. Cela sera versé au proposant qui incorpore la transaction dans un bloc. Actuellement, le proposant et l'instance Optimist sous-jacente choisiront probablement les frais plus élevés à incorporer dans un bloc, à peu près comme le ferait un mineur.
L'appel de la transaction entraîne l'enregistrement d'un événement blockchain contenant ses détails. S'il s'agit d'un dépôt, le contrat Shield prend en charge le paiement du jeton ERC de couche 1 en question.

### Hors chaîne {#off-chain}
Les transactions de transfert et de retrait ont la possibilité d'être envoyées directement aux proposants d'écoute plutôt que d'être envoyées sur la chaîne via le processus ci-dessus.
Ces transactions hors chaîne permettront aux transacteurs d'économiser le coût d'envoi sur la chaîne d'un dépôt (environ 45 000 gaz), mais elles nécessitent un plus grand degré de confiance entre les transacteurs et les proposants auxquels ils choisissent de se connecter. Il est plus facile pour les proposants mal intentionnés de censurer les transactions reçues hors chaîne que celles reçues sur chaîne, car ces transactions ne sont pas diffusées à tous les proposants d'écoute. Dans ce cas, les opérateurs ne doivent considérer une transaction comme fiable que lorsque la période de réflexion (1 semaine) est écoulée.

## Acceptation de la transaction {#transaction-acceptance}
Lorsque les proposants reçoivent des transactions, ils effectuent une série de vérifications pour valider que la transaction est bien formée et que la preuve est vérifiée par rapport au hachage d'entrée public.
Si toutes les vérifications sont réussies, la transaction est ajoutée au mempool du proposant pour être considérée dans un bloc.

## Assemblage et envoi des blocs {#block-assembly-and-submission}
Les proposants attendent que le contrat Shield les affecte en tant que proposants actuels.
Le proposant actuel reçoit, à partir de sa propre instance Optimist interne, un nouveau bloc contenant des transactions de son mempool. Pour chaque transaction, il calculera le nouvel engagement de l'arbre de Merkle qui existerait si ces transactions étaient ajoutées au contrat Shield.

Le bloc contient donc les hachages des transactions incluses dans le bloc et le root de l'engagement de l'arbre de Merkle tel qu'il existerait après traitement de toutes les transactions dans le bloc (Root de l'engagement). Ensuite, le proposant envoie ce bloc au contrat intelligent de l'état.

Lorsqu'un bloc est proposé, les informations suivantes sont enregistrées sur la chaîne :

- Structure de données de bloc
```
  struct Block {
    uint48 leafCount; // note this is defined to be the number of leaves BEFORE the commitments in this block are added
    address proposer;
    bytes32 root; // the 'output' commitment root after adding all commitments
    uint256 blockNumberL2;
    bytes32 previousBlockHash;
    bytes32 transactionHashesRoot;
  }
```
- Transactions en bloc
```
    struct Transaction {
        uint112 value;
        uint112 fee;
        TransactionTypes transactionType;
        TokenType tokenType;
        uint64[2] historicRootBlockNumberL2; // number of L2 block containing historic root
        uint64[2] historicRootBlockNumberL2Fee; //number of L2 block containing historic root fee
        bytes32 tokenId;
        bytes32 ercAddress;
        bytes32 recipientAddress;
        bytes32[2] commitments;
        bytes32[2] nullifiers;
        bytes32[1] commitmentFee;
        bytes32[2] nullifiersFee;
        bytes32[2] compressedSecrets;
        uint256[4] proof;
    }
```

## Challenges {#challenges}
Les blocs sont contestables dans la file d'attente pendant une semaine, période au cours de laquelle leur exactitude peut être contestée en lançant l'une des fonctions de contestation. Les challenges sont les suivants :

- **INVALID_PROOF** - la preuve donnée dans une transaction ne vérifie pas comme vraie ;
- **INVALID_PUBLIC_INPUT_HASH** - le hachage des entrées publiques d'une transaction n'est pas le hachage correct des entrées publiques ;
- **HISTORIC_ROOT_EXISTS** - le root de l'engagement de l'arbre de Merkle utilisé pour créer la preuve de transaction n'a jamais existé ;
- **DUPLICATE_NULLIFIER** - un nullificateur, donné dans le cadre d'une transaction, est présent dans la liste des nullificateurs dépensés ;
- **HISTORIC_ROOT_INVALID** - le root d'engagement mis à jour qui résulte du traitement des transactions dans le bloc est incorrect ;
- **DUPLICATE_TRANSACTION** - une transaction identique incluse dans ce bloc a déjà été incluse dans un bloc précédent ;
- **TRANSACTION_TYPE_INVALID** - la transaction n'est pas bien formée en fonction du type de transaction (par exemple, dépôt, transfert, retrait).

Si le challenge réussit, c'est-à-dire que le calcul sur la chaîne montre qu'il s'agit d'un challenge valide, alors les mesures suivantes sont prises :

- Le hachage du bloc en question et de tous les blocs suivants sont supprimés de la file d'attente.
- Le stake de bloc, envoyé par le proposant, est payé au challenger.
- Les transacteurs ayant une transaction dans le bloc sont remboursés des frais qu'ils auraient payés au proposant et des fonds bloqués détenus par le contrat Shield dans le cas d'une transaction de dépôt.

