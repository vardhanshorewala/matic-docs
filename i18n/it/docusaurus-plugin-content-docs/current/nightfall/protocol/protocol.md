---
id: protocol
title: Protocollo Nightfall
sidebar_label: Nightfall Protocol
description: "Il processo Nightfall."
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

Presumiamo che almeno un proponente sia registrato nel sistema e abbia pubblicato uno stake minimo.

## Pubblicazione delle transazioni {#transaction-posting}
Per pubblicare le nuove transazioni, esistono due meccanismi:

- [on-chain;](#on-chain)
- [off-chain.](#off-chain)

### on-chain; {#on-chain}
Per prima cosa, un operatore crea una transazione chiamando `submitTransaction` su `Shield.sol`. L'operatore paga una commissione al contratto Shield per la transazione, a sua completa discrezione. Questa verrà corrisposta al proponente, che incorpora la transazione in un blocco. Al momento, è probabile che per questa operazione il proponente e l'istanza Optimist sottostante scelgano le commissioni più elevate, un po' come farebbe un miner.
La chiamata Transazione fa sì che sia pubblicato un evento blockchain contenente i relativi dettagli. Se la transazione corrisponde a un deposito, il contratto Shield incassa il pagamento del token ERC L1 in questione.

### off-chain. {#off-chain}
Le transazioni di trasferimento e prelievo possono essere inviate, anziché tramite il processo on-chain visto precedentemente, direttamente ai proponenti in ascolto.
Le transazioni off-chain consentono agli operatori di risparmiare sui costi di invio di un deposito (circa 45.000 di gas), ma richiedono un maggior grado di fiducia tra gli operatori stessi e i proponenti a cui scelgono di affidarsi. Le transazioni ricevute off-chain possono essere più facilmente censurate dai proponenti in mala fede, poiché, a differenza delle transazioni on-chain, queste non sono trasmesse a tutti i proponenti in ascolto. In questo caso, gli operatori dovrebbero considerare una transazione affidabile solo quando è trascorso il periodo di pausa (una settimana).

## Accettazione delle transazioni {#transaction-acceptance}
Quando i proponenti ricevono una transazione, effettuano una serie di controlli per confermare che la transazione sia stata eseguita correttamente e che la prova corrisponda all'hash di input pubblico.
Se la transazione supera tutti i controlli, viene aggiunta al mempool del proponente, affinché ne sia valutato l'inserimento in un blocco.

## Creazione e invio del blocco {#block-assembly-and-submission}
I proponenti attendono che il contratto Shield assegni loro come proponente corrente.
Il proponente attuale riceve, dalla sua stessa istanza Optimist interna, un nuovo blocco contenente le transazioni che provengono dal suo mempool. Per ogni transazione, calcolerà il nuovo albero di Merkle degli impegni che verrebbe a crearsi qualora la transazione venisse aggiunta al contratto Shield.

Il blocco conterrà quindi gli hash delle transazioni incluse nel blocco stesso e la root dell'albero di Merkle degli impegni che si creerebbe dopo aver elaborato tutte le transazioni nel blocco (root degli impegni). Successivamente, il proponente invia il blocco allo State smart contract.

Quando viene proposto un blocco, vengono registrate on-chain le informazioni seguenti:

- struttura dei dati del blocco;
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
- transazioni nel blocco.
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

## Challenge {#challenges}
I blocchi resteranno in coda per una settimana: durante tale periodo, la loro correttezza potrà essere rimessa in discussione chiamando una delle funzioni di challenge. Le possibili challenge sono le seguenti:

- **INVALID_PROOF**: la prova fornita in una transazione non si rivela vera;
- **INVALID_PUBLIC_INPUT_HASH**: l'hash di input pubblico di una transazione non è l'hash degli input pubblici corretto;
- **HISTORIC_ROOT_EXISTS**: la root dell'albero di Merkle degli impegni utilizzata per creare la prova della transazione non è mai esistito;
- **DUPLICATE_NULLIFIER**: un nullifier fornito nell'ambito della transazione è presente nell'elenco dei nullifier già utilizzati;
- **HISTORIC_ROOT_INVALID**: la root degli impegni aggiornata che deriva dall'elaborazione delle transazioni nel blocco non è corretta;
- **DUPLICATE_TRANSACTION**: una transazione identica inclusa nel blocco in questione è già stata inclusa in un blocco precedente;
- **TRANSACTION_TYPE_INVALID**: la transazione non ha la forma corretta in base al tipo di transazione (ad es. deposito, trasferimento, prelievo).

Se la challenge si conclude correttamente, ossia se il calcolo on-chain dimostra che è valida, vengono intraprese le azioni seguenti:

- l'hash del blocco in questione e di tutti i blocchi successivi vengono rimossi dalla coda;
- lo stake del blocco, inviato dal proponente, è pagato al challenger;
- all'operatore con una transazione nel blocco vengono rimborsati la commissione che avrebbe pagato al proponente e gli eventuali fondi trattenuti dal contratto Shield nel caso delle transazioni di deposito.

