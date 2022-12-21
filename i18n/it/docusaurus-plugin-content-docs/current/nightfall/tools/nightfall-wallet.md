---
id: nightfall-wallet
title: Wallet Nightfall
sidebar: Nightfall Wallet
description: "Guida al wallet Polygon Nightfall."
keywords:
  - docs
  - matic
  - polygon
  - nightfall
  - wallet
image: https://matic.network/banners/matic-network-16x9.png

---

Il wallet Polygon Nightfall è un wallet browser in grado di interagire con la
versione beta della mainnet Nightfall.

:::info Utilizza il wallet Nightfall per effettuare depositi, trasferimenti e prelievi

### Limitazioni {#restrictions}

Finché Nightfall non avrà raggiunto la maturità, si applicheranno le seguenti limitazioni:


| Token ERC20 | Deposito massimo | Prelievo massimo |
|-------------|-------------|--------------|
| MATIC | 250 MATIC | 1.000 MATIC |
| WETH | 0,25 WETH | 1 WETH |
| DAI | 250 DAI | 1.000 DAI |
| USDT | 250 USDT | 1.000 USDT |
| USDC | 250 USDC | 1.000 USDC |

:::

:::caution Misure di sicurezza

Il wallet Nightfall è testato su un browser Chrome. Durante la fase Beta, la resa sugli altri browser
può variare.

**Consigliamo vivamente di utilizzare Nightfall su Chrome**.

:::



## Per iniziare {#getting-started}

Visita il [wallet mainnet](https://wallet-beta.polygon.technology) web di Polygon oppure
[il wallet testnet](https://wallet.testnet.polygon-nightfall.technology/), connetti il tuo account MetaMask
e seleziona il wallet Polygon a sinistra. Per assistenza con Metamask, consulta la
[documentazione Polygon su Metamask](../../develop/metamask/tutorial-metamask.md)

![](../imgs/tools-wallet/polygon-wallet-click-nf.png)

A questo punto, il wallet richiederà di passare alla rete di Polygon; si aprirà una finestra pop-up di Metamask,
in cui verrà richiesto di confermare l'operazione.

![](../imgs/tools-wallet/polygon-network.png)

Successivamente, nella sezione superiore del wallet, fai clic sul menu a discesa e seleziona `Polygon Nightfall`: comparirà
una nuova richiesta di passare all'Ethereum mainnet. Accetta di passare all'Ethereum mainnet
per poter operare con Polygon Nightfall.

![](../imgs/tools-wallet/polygon-network-dropdown-nf.png)

Se operi su testnet, l'URL del wallet ti indirizza immediatamente alla landing page del wallet Polygon Nightfall.

![](../imgs/tools-wallet/wallet-main-screen.png)

Alla tua prima visita, sarà necessario creare il tuo wallet Nightfall. Dovrebbe apparire un pop-up per la generazione di un mnemonico e la creazione del wallet. Fai clic su `Generate Mnemonic`, quindi su `Create Wallet`. **Ricorda che puoi usare il wallet soltanto sul tuo dispositivo corrente**.

![](../imgs/tools-wallet/generate-mnemonic-create-wallet.png)

:::caution Backup di impegni e mnemonici

Le chiavi e le transazioni del wallet sono memorizzate nel browser (IndexedDb). Lo stesso vale per il mnemonico che hai configurato al primo accesso al wallet Nightfall.

Assicurati di conservare il mnemonico in un luogo sicuro. È l'unico modo per poter produrre prove compatibili con i tuoi fondi su L2. Lo stesso accade con i tuoi impegni: assicurati di memorizzarli in modo sicuro toccando `export commitments` ogni volta che usi un altro browser o un'altra macchina.

:::

**Se perdi i tuoi impegni, i fondi andranno persi per sempre**


A questo punto dovresti essere in grado di vedere gli indirizzi sia Metamask che Nightfall (in alto a destra).

**Prima di iniziare a eseguire transazioni, attendi qualche altro minuto affinché la configurazione del wallet sia completa**.

Nell'angolo in basso a sinistra del wallet, lo stato del wallet sarà mostrato come `Syncing Nightfall`. In questo stato, il wallet sta recuperando
i circuiti ZK e lo stato della rete necessari per eseguire le transazioni.

![](../imgs/tools-wallet/wallet-state-syncing.png)

Attendi finché lo stato del wallet passerà a `Nightfall Synced`

![](../imgs/tools-wallet/wallet-state-synced.png)


## Come connettere un hardware wallet Ledger a Nightfall {#how-to-connect-a-ledger-hardware-wallet-to-nightfall}
Una guida alla connessione degli hardware wallet Ledger con Metamask è disponibile sul sito ufficiale di Metamask ([qui](https://support.ledger.com/hc/en-us/articles/4404366864657-How-to-access-your-Ledger-Ethereum-ETH-account-via-Metamask?docs=true)).

Assicurati di connettere l'app Ethereum nel wallet e attivare la funzione di "blind signing" nelle impostazioni dell'app.


### Indirizzo del wallet {#your-wallet-address}
Puoi ottenere l'indirizzo del wallet Nightfall dalla pagina degli Asset Nightfall, facendo clic su `Receive`.

![](../imgs/tools-wallet/nightfall-wallet-address.png)

## Come effettuare depositi {#how-to-make-deposits}
Dalla pagina degli Asset Nightfall, fai clic sul pulsante `Deposit` a destra della risorsa prescelta o vai alla pagina del Bridge L2.

1. Verifica che la modalità di Trasferimento sia impostata su `Deposit`
2. Verifica che sia selezionato il token desiderato (WETH, MATIC, ecc.)
3. Inserisci il valore da depositare nel wallet Nightfall e fai clic su `Transfer`
4. Ricontrolla la transazione nella finestra pop-up
5. Fai clic su `Create Transaction`

![](../imgs/tools-wallet/deposit-click-transfer.png)

Verrà avviata una procedura per calcolare la ZKP e preparare la transazione: concedi a Metamask l'accesso al saldo del tuo conto. Terminata la procedura, fai clic su `Send Transaction`: concedi a Metamask ulteriori permessi per l'interazione con i contratti.

![](../imgs/tools-wallet/deposit-tx-created-and-ready-to-be-sent.png)

Per [visualizzare il deposito](#view-transactions), vai alla pagina delle Transazioni.

### Informazioni importanti sui depositi {#important-information-about-deposits}
- Durante la fase Beta, [gli importi dei depositi sono soggetti a limitazioni](#note-the-following-deposit-and-withdrawal-restrictions)

## Come effettuare trasferimenti {#how-to-make-transfers}
Dalla pagina degli Asset Nightfall, fai clic sul pulsante `Send` a destra della risorsa prescelta.

1. Inserisci un indirizzo valido esistente sull'L2 di Polygon Nightfall
2. Verifica che sia selezionato il token desiderato (WETH, MATIC, ecc.)
3. Inserisci il valore da trasferire dal wallet Nightfall e fai clic su `Continue`

![](../imgs/tools-wallet/send-nf.png)

Verrà avviata una procedura per calcolare la ZKP e preparare la transazione. Terminata la procedura, fai clic su `Send Transaction`.

Per [visualizzare il trasferimento](#view-transactions), vai alla pagina delle Transazioni.

### Informazioni importanti sui trasferimenti {#important-information-about-transfers}
I circuiti di trasferimento ZKP attualmente utilizzati in Nightfall limitano l'importo dei trasferimenti al valore esatto di uno degli
impegni esistenti o a qualsiasi combinazione lineare di due impegni esistenti.

Per illustrare le limitazioni ai trasferimenti con un esempio, osserviamo i seguenti insiemi di impegni:

- Insieme A: [1, 1, 1, 1, 1, 1]
- Insieme B: [2, 2, 2]
- Insieme C: [2, 4]

Tutti e tre gli insiemi hanno un totale equivalente a 6, ma solo i seguenti trasferimenti sono disponibili:

- Insieme A: qualsiasi trasferimento tra 0 e 2 (esclusi 0 e 2)
- Insieme B: qualsiasi trasferimento tra 0 e 4 (esclusi 0 e 4)
- Insieme C: qualsiasi trasferimento tra 0 e 6 (esclusi 0 e 6)

Per continuare con l'esempio, se Alex possiede l'Insieme di impegni C, i trasferimenti disponibili sono quelli di importo compreso fra 0 e 6, esclusi 0 e 6. Se Alex decide di trasferire 3,5 a Bob, una volta proposto il blocco, Alex si ritrova con un unico impegno di 2,5 e Bob riceve un impegno di 3,5.

Se invece Alex decidesse di trasferire a Bob un importo di 6, la prova ZK non andrebbe a buon fine, poiché non ci sarebbe una combinazione di impegni valida.

**È importante notare che questi valori rappresentano gli impegni detenuti**, e non ad esempio dei depositi. Per ulteriori informazioni, consulta la sezione dedicata agli [impegni](../protocol/commitments.md) di questi docs.

## Come effettuare prelievi {#how-to-make-withdrawals}
Dalla pagina degli Asset Nightfall, fai clic sul pulsante `Withdraw` a destra della risorsa prescelta o vai alla pagina del Bridge L2.

1. Verifica che la modalità di Trasferimento sia impostata su `Withdraw`
2. Verifica che sia selezionato il token desiderato (WETH, MATIC, ecc.)
3. Inserisci il valore da prelevare dal wallet Nightfall e fai clic su `Transfer`
4. Ricontrolla la transazione nella finestra pop-up
5. Fai clic su `Create Transaction`

Verrà avviata una procedura per calcolare la ZKP e preparare la transazione. Terminata la procedura, fai clic su `Send Transaction`.

Per [visualizzare il prelievo](#view-transactions), vai alla pagina delle Transazioni. Una volta trascorso il periodo di finalizzazione di una settimana, l'utente
potrà finalizzare e riscattare l'importo del prelievo.

### Informazioni importanti sui prelievi {#important-information-about-withdrawals}
- Il valore dei prelievi deve corrispondere esattamente all'importo di uno degli impegni detenuti (ulteriori informazioni [sugli impegni](#learn-about-commitments))
- I prelievi sono soggetti a un periodo di finalizzazione di **una settimana**, a partire dal momento in cui viene creato il blocco che comprende la transazione del prelievo. Una volta trascorso tale periodo, puoi finalizzare il prelievo affinché i fondi siano inviati al tuo account Ethereum.
- Durante la fase Beta, [gli importi dei prelievi sono soggetti a limitazioni](#note-the-following-deposit-and-withdrawal-restrictions)
- I prelievi sono transazioni on-chain e richiedono il pagamento di gas fee sia durante la richiesta della transazione che alla finalizzazione del prelievo.

![](../imgs/tools-wallet/cooling-off-vs-ready.png)

## Visualizza le transazioni {#view-transactions}
Verifica lo stato di depositi, trasferimenti e prelievi alla pagina delle Transazioni. Ogni transazione viene elaborata non appena vi è un numero di transazioni sufficiente a produrre un blocco, oppure dopo 6 ore.

![](../imgs/tools-wallet/transactions.png)
