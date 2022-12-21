---
id: circuits
title: Circuits et transactions
sidebar_label: Circuits and Transactions
description: "Types de circuits sur Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - circuits
  - deposit
  - transfer
image: https://matic.network/banners/matic-network-16x9.png
---

Les circuits sont utilisés pour définir les règles qu'une transaction doit suivre pour être considérée comme correcte. Il existe globalement trois types de circuits, un pour chaque type de transaction :

- [Dépôt](#deposit)
- [Transfert](#transfer)
- [Retrait](#withdraw)

Chaque transaction comprend une preuve à divulgation nulle de connaissance suivant les contraintes spécifiées dans ces circuits. Les utilisateurs construisent cette preuve à l'aide d'un portefeuille,
ou via un serveur client.
Une preuve n'est générée que si tous les cas suivants sont vrais :

- Le nouvel [engagement](./commitments#what-are-commitments) est valide
- L'ancien [engagement](./commitments#what-are-commitments) est valide et appartient à l'expéditeur
- Le [nullificateur] (./commitments#what-are-nullifiers) est valide
- Le chemin/root de l'arbre de Merkle est valide
- L'engagement contenant le texte chiffré est valide


## Dépôt {#deposit}
Les dépôts convertissent les jetons ERC visibles publiquement en un engagement de jeton qui contient la même valeur ou l'identifiant de jeton que celui du jeton d'origine,
et la clé publique Nightfall du propriétaire de l'engagement prévu.

Une preuve à divulgation nulle de connaissance du dépôt prouve que le prouveur a créé un engagement $Z_A$ with a public key $pk_A$ valide.

Le circuit vérifie ensuite que $Z_A$ == H(@ | ɑ | $pk_A$ | σ)
Les informations divulguées sur une transaction de dépôt comprennent l'adresse qui a marqué le nouvel engagement ainsi que l'adresse et la valeur du jeton ERC utilisé.

![](../imgs/deposit.png)

## Transfert {#transfer}
Les transferts permettent de transmettre jusqu'à deux engagements d'un même actif entre deux parties en annulant les engagements antérieurs et en créant jusqu'à deux nouveaux engagements :
- L'un sera envoyé au destinataire, contenant la valeur du montant transféré
- Un autre sera créé avec la valeur de la monnaie (différence entre la somme des valeurs des engagements utilisés moins la valeur transférée) et appartenant à l'émetteur.

Une preuve à divulgation nulle de connaissance du transfert prouve que le prouveur a annulé jusqu'à deux anciens engagements qui existaient dans l'arbre de Merkle, en a créé un nouveau et a chiffré ses informations pour le destinataire.

Dans les deux cas, l'information divulguée sera qu'une adresse Ethereum a annulé des engagements
parmi le pool d'engagements détenu par l'émetteur, et que de nouveaux engagements ont été créés.
Les informations sur le nouveau propriétaire, les engagements qui ont été dépensés ou le montant transféré restent privés.

Le premier diagramme passe en revue les étapes consistant à annuler un engagement (ou des engagements) existant(s) et à ajouter les informations à la structure des données de`transaction`.

![](../imgs/transfer_a.png)

Le deuxième diagramme passe en revue les étapes requises pour générer et chiffrer l'engagement nouvellement créé.

![](../imgs/transfer_b.png)

## Retrait {#withdraw}
Le retrait est l'opération consistant à annuler un engagement Nightfall existant et à le convertir en jetons ERC visibles publiquement avec la même valeur et le même identifiant de jeton que l'engagement brûlé. Le retrait est l'opération opposée au dépôt. À l'instar des transferts, les retraits acceptent comme entrée jusqu'à deux engagements.

Une preuve à divulgation nulle de connaissance du retrait prouve que le prouveur a annulé jusqu'à deux anciens engagements qui existaient dans l'arbre de Merkle.

Les informations divulguées lors d'un retrait comprennent l'adresse de l'adresse qui a retiré l'engagement, la valeur / l'identifiant du jeton et l'adresse du jeton retiré.

![](../imgs/withdraw.png)

### Période de réflexion {#cooling-off-period}

Les retraits nécessitent une période de `COOLING OFF` d'une semaine pour être finalisés. Cela est dû à la nature optimiste de Nightfall, car un nouveau bloc est supposé correct jusqu'à ce que certains challengers soumettent une preuve de fraude. Les fonds sont retenus jusqu'à ce qu'une semaine se soit écoulée. Ensuite, ils peuvent être retirés à L1.

# Frais {#fees}

Le proposant prend la transaction entrante et l'intègre dans un bloc L2 en échange de frais. Il existe deux types de frais payés à la proposition en fonction de la transaction :
- Les dépôts paient les frais ETH directement dans L1.
- Les transferts et retraits paient des frais en MATIC dans L2.
