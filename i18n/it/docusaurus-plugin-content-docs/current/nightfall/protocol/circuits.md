---
id: circuits
title: Circuiti e transazioni
sidebar_label: Circuits and Transactions
description: "Tipi di circuiti su Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - circuits
  - deposit
  - transfer
image: https://matic.network/banners/matic-network-16x9.png
---

I circuiti vengono utilizzati per stabilire le regole che deve rispettare una transazione per essere considerata corretta. I circuiti possono essere sostanzialmente di tre tipi, uno per ogni tipo di transazione:

- [Deposito](#deposit)
- [Trasferimento](#transfer)
- [Prelievo](#withdraw)

Ogni transazione comprende una Zero-Knowledge Proof (ZKP) che segue i vincoli specificati in questi circuiti. Gli utenti costruiscono la prova utilizzando un wallet
oppure attraverso un client server.
Viene generata una prova solo se tutti i casi seguenti risultano veri:

- il nuovo [impegno](./commitments#what-are-commitments) è valido;
- il vecchio [impegno](./commitments#what-are-commitments) è valido e di proprietà del mittente;
- [Nullifier] (./commitments#what-are-nullifiers) è valido;
- il percorso/la root dell'albero di Merkle è valido(a);
- il testo criptato contenente l'impegno è valido.


## Deposito {#deposit}
I depositi convertono i token ERC visibili al pubblico in un impegno in token con lo stesso valore o lo stesso ID del token originale,
e la chiave pubblica Nightfall del proprietario dell'impegno previsto.

Una ZKP di deposito dimostra che il prover abbia creato un impegno valido $Z_A$ with a public key $pk_A$.

Il circuito quindi verifica che $Z_A$ == H(@ | ɑ | $pk_A$ | σ)
Per le transazioni di deposito, le informazioni divulgate comprendono l'indirizzo che ha creato il nuovo impegno, nonché l'indirizzo e il valore del token ERC utilizzato.

![](../imgs/deposit.png)

## Trasferimento {#transfer}
I trasferimenti consentono la trasmissione di un massimo di due impegni dello stesso asset tra due parti, annullando gli impegni precedenti e creando fino a due nuovi impegni:
- il primo, contenente il valore dell'importo trasferito, viene inviato al destinatario;
- il secondo, contenente il valore del cambio (somma dei valori degli impegni utilizzati, meno il valore trasferito), resta al mittente.

Una ZKP di trasferimento dimostra che il prover ha annullato un massimo di due impegni esistenti nell'albero di Merkle, creato un massimo di due nuovi impegni e crittografato le relative informazioni per il destinatario.

In ogni caso, l'informazione divulgata è che un indirizzo Ethereum ha annullato gli impegni
nella pool di impegni di proprietà del trasmettitore e che sono stati creati nuovi impegni.
Le informazioni sul nuovo proprietario, sugli impegni spesi o sull'importo trasferito restano private.

Il primo diagramma analizza i passaggi per l'annullamento di un impegno esistente (o di più impegni esistenti) e l'aggiunta delle informazioni alla struttura dei dati `transaction`.

![](../imgs/transfer_a.png)

Il secondo diagramma analizza i passaggi necessari per generare e crittografare l'impegno appena creato.

![](../imgs/transfer_b.png)

## Prelievo {#withdraw}
Il prelievo è un'operazione che consiste nell'annullare un impegno Nightfall esistente e convertirlo in token ERC visibili pubblicamente, con lo stesso valore e lo stesso token ID dell'impegno annullato. Il prelievo è l'operazione opposta al deposito. Analogamente ai trasferimenti, i prelievi accettano come input fino a due impegni.

Una ZKP di prelievo dimostra che il prover ha annullato fino a due impegni precedentemente esistenti nell'albero di Merkle.

Durante un prelievo, le informazioni divulgate includono l'indirizzo che ha prelevato l'impegno, nonché il valore/token ID e l'indirizzo del token prelevato.

![](../imgs/withdraw.png)

### Periodo di pausa {#cooling-off-period}

Per poter completare un prelievo, è necessario attendere un periodo di `COOLING OFF` di una settimana. Questo avviene a causa della natura optmistic di Nightfall, dato che un nuovo blocco viene considerato corretto finché un challenger non dimostri che sia avvenuta una truffa. I fondi vengono quindi trattenuti per una settimana, trascorsa la quale potranno essere prelevati e trasmessi in L1.

# Commissioni {#fees}

Il proponente prende in carico la transazione in entrata e la inserisce in un blocco L2, in cambio di una commissione. Le commissioni pagate al proponente possono essere di due tipi, a seconda della transazione:
- commissioni pagate in ETH direttamente in L1 per i depositi;
- commissioni in MATIC in L2 per i trasferimenti e i prelievi.
