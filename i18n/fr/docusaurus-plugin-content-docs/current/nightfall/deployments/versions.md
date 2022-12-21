---
id: versions
title: Historique
sidebar_label: History of changes
description: "Versions déployées"
keywords:
  - docs
  - polygon
  - nightfall
  - changelog
image: https://matic.network/banners/matic-network-16x9.png
---


## Beta 1.0 {#beta-1-0}
La version Beta 1.0 a été publiée le 17 mai 2022. Elle comprenait le mécanisme de base pour déployer la preuve de concept Nightfall.
Elle a pris en charge un `Proposer` unique et une première mise en œuvre `coarse` des transactions. Elle a également fourni une première
version d'un portefeuille utilisateur.
La version déployée peut être trouvée [ici](https://github.com/EYBlockchain/nightfall_3/commit/bc3e475de3e2877f14430f9599e5b38ea960765b)

## Beta 2.0 {#beta-2-0}
La version déployée peut être trouvée [ici](https://github.com/EYBlockchain/nightfall_3/commit/4c2af01ac95af5ea6f5b40071d73a1624f06ba46)
Plusieurs améliorations ont été apportées :
- **Collecter des frais**

Possibilité pour les proposants de collecter des frais de transactions. Cette fonctionnalité sera incitative pour plusieurs proposants.
- **Déploiement du challenger**

Le réseau comprend désormais un challenger qui surveille les blocs du proposant.
- **Transactions de circuits**

Plus de flexibilité et de meilleures performances lors de la génération du ZKP de toutes les transactions.  Aussi bien `transfer` que `withdrawal` acceptent jusqu'à deux engagements et la monnaie de retour.
En ce qui concerne les performances, les transactions sont maintenant optimisées de sorte qu'il faut moins de temps pour les prouver.

| Opérations | Contraintes avant | Contraintes après |
|-----------|--------------------|------------------|
| Déposer | 84 766 | 1277 |
| Transférer | 499 119 | 67 694 |
| Retirer | 168 883 | 53 348 |

Une partie de l'optimisation a été possible en passant à Poseidon

- **Chiffrement des secrets**

Nous sommes passés d'El-Gamal à un processus de chiffrement [KEM-DEM](../protocol/secrets) qui a apporté plusieurs avantages :
- Simplification du processus de chiffrement / déchiffrement
- Réduction des contraintes et des coûts de gaz sur la chaîne.

- **Déploiement du challenger**

