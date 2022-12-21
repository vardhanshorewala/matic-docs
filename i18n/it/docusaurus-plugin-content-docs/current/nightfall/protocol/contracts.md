---
id: contracts
title: Smart Contract
sidebar_label: Smart Contracts
description: "Shield, proponenti, challenge e computazioni con albero di Merkle."
keywords:
  - docs
  - polygon
  - nightfall
  - smart
  - contracts
  - shield
image: https://matic.network/banners/matic-network-16x9.png
---

I contratti definiscono le regole che ogni partecipante Nightfall deve seguire per poter operare sulla rete.
Tra gli Smart Contract sono compresi:

- [Shield.sol](#shield)
- [Proposers.sol](#proposers)
- [Challenges.sol](#challenges)
- [MerkleTree_Computations.sol](#merkletree_computations)

## Shield {#shield}
Questo contratto consente agli utenti di inviare una transazione a un proponente affinché venga elaborata. Nel caso si tratti di una transazione di deposito, richiederà un pagamento.
Consente inoltre a chiunque di richiedere un aggiornamento del contratto Shield (root impegni ed elenchi nullifier).
Quando lo stato è aggiornato, vengono elaborati gli eventuali prelievi nell'aggiornamento.

Pubblicare una transazione di trasferimento o prelievo sulla blockchain non è strettamente necessario, ma è una sorta di "messaggio in bacheca" che avvisa
i proponenti di aggiudicarsi la transazione e incorporarla in un blocco Layer 2.

Poiché Nightfall interagisce con contratti ERC reali, i seguenti controlli non possono essere privati:

- durante un **deposito/prelievo**, l'indirizzo del token ERC è valido;
- durante **un deposito**, l'utente dispone del saldo o possiede il token per creare un impegno.

## Proponenti {#proposers}
Il contratto include funzionalità per la registrazione, l'annullamento della registrazione, il pagamento e la rotazione dei proponenti, nonché per proporre nuovi blocchi L2 nella blockchain.
La prima versione di Nightfall accetta un solo proponente di avvio gestito da Polygon. Nelle versioni successive, questa restrizione verrà revocata e saranno consentiti più proponenti.

## Challenge {#challenges}
La funzionalità consente di contestare un blocco perché erroneo.

## MerkleTree_Stateless {#merkletree_stateless}
Una versione stateless (funzione pura) dell'originale `MerkleTree.sol`, utilizzata da `Challenges.sol` per contribuire a calcolare le challenge relative ai blocchi on-chain.

## Altri contratti {#other-contracts}
- `Utils.sol`: riunisce una funzionalità utilizzata in più contratti o che, se lasciata inline, influirebbe sulla leggibilità del codice.
- `Config.sol`: mantiene le costanti, analogamente a un file Node.js config.
- `Structures.sol` - definisce le variabili globali struct, enum, event, mapping e state, e le rende più facili da trovare.

## Aggiornabilità {#upgradability}
Almeno inizialmente, Polygon conserva la capacità di aggiornare i contratti Nightfall dopo l'implementazione.
A tal fine, utilizziamo i [Plugin di upgrade](https://docs.openzeppelin.com/upgrades-plugins/1.x/) per Truffle Openzeppelin.

Per aggiornare i contratti, Polygon utilizza un modulo [implementatore](https://github.com/EYBlockchain/nightfall_3/tree/master/nightfall-deployer).
Nelle cartelle di migrazione di `deployer`, sono memorizzate 4 migrazioni.
Le prime tre migrazioni effettuano un'implementazione "normale" della suite di contratti Polygon Nightfall, ma
assicurano comunque che tutti i contratti (ma non le librerie) siano implementati con un proxy che consentirà di
aggiornarli successivamente. La quarta migrazione viene utilizzata per aggiornare i contratti.
