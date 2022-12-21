---
id: faq
title: DOMANDE FREQUENTI
sidebar_label: FAQ
description: Domande frequenti su Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip

Se non trovi la tua domanda in questo elenco, invia la tua domanda al <ins>**[server discord Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR)**</ins>.

:::

## Dove posso trovare gli smart contract? {#where-can-i-find-the-smart-contracts}

I contratti Polygon Nightfall sono stati distribuiti nella [testnet Goerli](../deployments/testnet.md) e nella [mainnet](../deployments/mainnet.md).

## Qual è lo stato dell'audit di sicurezza di Polygon Nightfall? {#what-s-the-state-of-polygon-nightfall-s-security-audit}
Polygon Nightfall è attualmente sottoposto a un audit di sicurezza che dovrebbe concludersi nel terzo trimestre. Nel frattempo, sono state aggiunte diverse restrizioni al protocollo:

- Singolo proponente in funzione e gestito da Polygon
- [Importi di deposito e prelievo limitati](../tools/nightfall-wallet.md#deposit-and-withdraw-restrictions)

## Come faccio a configurare il mio wallet Nightfall? {#how-do-i-set-up-my-nightfall-wallet}
[Qui](../tools/nightfall-wallet.md) è possibile consultare un tutorial completo sul wallet con tutti i dettagli su come iniziare a usare il wallet Polygon Nightfall.

## Come faccio a collegare un wallet hardware ledger al wallet Nightfall? {#how-do-i-connect-a-ledger-hardware-wallet-to-nightfall-wallet}
Nel tutorial del wallet è presente una sezione che spiega [come collegare un wallet ledger hardware con Metamask](../tools/nightfall-wallet.md#how-to-connect-a-ledger-hardware-wallet-to-nightfall).

## Quanto tempo impiegano i trasferimenti sulla rete Nightfall di Polygon dall'inizio alla fine? {#how-long-do-transfers-take-on-polygon-nightfall-network-from-start-to-finish}
L'attuale proponente riceve le transazioni dagli utenti e crea blocchi fino a 32 transazioni. Non appena viene raccolto un numero sufficiente di transazioni per costruire un blocco, la transazione viene elaborata.

Inoltre, c'è un limite massimo al periodo di generazione dei blocchi in modo che venga proposto almeno un blocco ogni 6 ore (indipendentemente dal numero di transazioni raccolte dal proponente).

## Con chi posso fare transazioni? {#who-can-i-transact-with}
Per trasferire gli asset all'interno di Polygon Nightfall è sufficiente il `Destination Wallet Address`. Leggi il tutorial sul wallet per capire [come condividere l'indirizzo del tuo wallet](../tools/nightfall-wallet.md#your-wallet-address) per ricevere fondi.

## Dove vengono effettuati i backup degli impegni? {#where-are-commitments-backed-up}

Le Zero Knowledge Proof vengono calcolate nel browser, in modo che le tue chiavi segrete rimangano con te, mentre il wallet tiene traccia di tutti gli impegni che possiedi, nel suo IndexedDb. Chiunque abbia accesso a questi dati può scoprire quali impegni possiedi, anche se non può rubarli senza le tue chiavi. Le chiavi vengono decifrate solo quando si inserisce il mnemonico. Pertanto, dovresti utilizzare il wallet solo su un computer di cui ti fidi.

Per ora, questi dati non vengono esportati da alcuna parte. Pertanto, se utilizzi un browser su un altro computer, non avrai accesso ai tuoi impegni a meno che tu trasferisca i contenuti dell'IndexedDB. Forniamo un meccanismo per esportare e importare impegni attraverso il wallet.

## Privacy delle transazioni {#privacy-of-transactions}
È importante capire che le transazioni di deposito e prelievo non sono private. Questo perché interagiscono con il Layer 1, e il Layer 1 non è privato. Questo significa che tutti sanno se crei un impegno il Layer 2 e quanto contiene. Allo stesso modo, se si restituisce un token al Layer 1 distruggendo un impegno nel Layer 2, tutti ne conoscono il valore e il destinatario.

La privacy deriva interamente dai trasferimenti all'interno del Layer 2. Dal punto di vista della blockchain di Ethereum, questi sono completamente privati. L'unico dato che trapela è il tuo indirizzo IP quando invii una transazione di trasferimento a un proponente di blocco. Per la Beta iniziale, Polygon gestisce gli unici proponenti.


## Come si prelevano i fondi? {#how-to-withdraw-funds}
I fondi possono essere prelevati mediante il wallet Nightfall di Polygon. I prelievi sono soggetti a un periodo di finalizzazione di **una settimana**, a partire dal momento in cui viene creato il blocco che comprende la transazione del prelievo. Una volta trascorso tale periodo, puoi finalizzare il prelievo affinché i fondi siano inviati al tuo account Ethereum.

## Quanto costano le transazioni su Nightfall? {#how-much-will-transactions-cost-on-nightfall}
Esistono due tipi di transazioni che comportano costi diversi:

- Transazioni on-chain: vengono inviate allo smart contract e richiedono il pagamento di gas su Ethereum per il mining. Qualsiasi proponente può prendere questa transazione e inserirla in un blocco. Attualmente, `deposit` e `finalize withdrawal` sono transazioni on-chain.
- Transazioni off-chain: vengono inviate direttamente al proponente. Attualmente, tutte le transazioni `transfer`e `withdrawals` sono configurate come off-chain.

## Quali token posso utilizzare sulla rete Nightfall? {#which-tokens-can-i-use-on-nightfall-network}
Su Nightfall sono operativi i seguenti token:

- MATIC
- WETH
- DAI
- USDC

## Occorrono token MATIC per usare Nightfall? {#do-i-need-matic-tokens-to-use-nightfall}
Sì. Dovrai depositare dei token MATIC su Nightfall per poter pagare `transfers` e `withdrawals`.

## Dove posso inviare una segnalazione di bug o contattare Nightfall per ricevere ulteriore assistenza? {#where-can-i-submit-a-bug-report-or-contact-nightfall-for-additional-help}
Il modo migliore è unirsi al nostro [server discord Polygon Nightfall](https://discord.com/invite/pZkC3JV2bR) e inviare la tua domanda.
