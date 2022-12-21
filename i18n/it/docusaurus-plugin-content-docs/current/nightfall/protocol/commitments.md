---
id: commitments
title: Impegni e Nullifier
sidebar_label: Commitment and Nullifiers
description: "Trasferimenti singoli e doppi."
keywords:
  - docs
  - polygon
  - nightfall
  - commitment
  - nullifier
image: https://matic.network/banners/matic-network-16x9.png
---


## Cosa sono gli impegni? {#what-are-commitments}
Un impegno è una primitiva crittografica che consente a un utente di impegnarsi su un valore prescelto
e tenerlo nascosto agli altri, con la possibilità di rivelare il valore impegnato in un secondo momento.
In questo modo si ottiene la riservatezza del valore e del destinatario.

Ogni volta che un utente esegue una transazione con Nightfall, il wallet browser calcola una Zero
Knowledge Proof (ZKP) e crea (o annulla) un impegno.
Ad esempio, crei un impegno quando effettui un deposito o un bonifico e annulli un impegno quando
effettui un trasferimento o un prelievo.

Il calcolo ZKP si basa su [circuiti](../protocol/circuits.md) che definiscono le regole che una
transazione deve seguire per essere corretta.

L'impegno viene utilizzato per nascondere le seguenti proprietà:
- **Indirizzo ERC del token**
- **ID del token**
- **Valore**
- **Proprietario**

Gli impegni sono memorizzati in una struttura ad *albero di Merkle*. La root di questo *albero di Merkle* è memorizzata on-chain.

![](../imgs/commitment.png)

### UTXO {#utxo}
Gli impegni vengono creati durante i depositi e trasferimenti, e vengono spesi durante le operazioni di trasferimento e prelievo. **Gli impegni non vengono aggregati**. Quando si spende un impegno, il valore dell'impegno speso è limitato al valore di un massimo di due impegni posseduti.

Gli attuali circuiti di trasferimento e prelievo ZKP utilizzati in Nightfall sono limitati a 2 ingressi e 2 uscite (impegno di trasferimento/prelievo e modifica), esclusi i pagamenti.
Se l'insieme degli impegni di un transattore contiene principalmente impegni di basso valore (polvere), potrebbe avere difficoltà a effettuare trasferimenti futuri.

Osserva il seguente set di valori

- **Set A**: [1, 1, 1, 1, 1, 1]
- **Set B**: [2, 2, 2]
- **Set C**: [2, 4]

Sebbene tutti e tre i set abbiano somme totali equivalenti, il trasferimento massimo di valore che può essere operato dai set *A*, *B* e *C* è 2, 4 e 6 rispettivamente. Questo è uno dei motivi per cui si preferiscono valori di impegno elevati. La strategia di selezione degli impegni utilizzata attenua questo rischio dando priorità all'utilizzo di impegni di valore ridotto e riducendo al minimo la creazione di impegni di polvere.


## Cosa sono i Nullifier? {#what-are-nullifiers}
Un **Nullifier** è il risultato della combinazione di un impegno e della chiave di annullamento. Una volta che il Nullifier viene trasmesso on-chain, l'impegno viene considerato esaurito.
I Nullifier sono memorizzati on-chain come parte dei dati della chiamata durante la proposta del blocco.

![](../imgs/nullifier.png)



