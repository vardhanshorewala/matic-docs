---
id: overview
title: Panoramica
sidebar_label: Overview
description: Una panoramica di Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - privacy
  - rollup
  - zk
image: https://matic.network/banners/matic-network-16x9.png
---

Polygon crede nell'idea che nel prossimo futuro molte aziende interagiranno tra loro attraverso smart contract
per l'esecuzione di logiche commerciali e la gestione dello scambio di beni e servizi.

In collaborazione con [Ernst & Young](https://blockchain.ey.com/), Polygon offre una soluzione Layer 2 rollup pubblica e incentrata sulla privacy, chiamata Polygon Nightfall, per consentire l'accessibilità e la privacy alle aziende che desiderino
utilizzare Ethereum.

## Un protocollo ZK-Proof per le aziende {#a-zk-proof-protocol-for-enterprises}

Polygon Nightfall fa parte della suite di soluzioni di scalabilità di Polygon, che comprende
[Polygon Hermez](https://polygon.technology/solutions/polygon-hermez/),
[Polygon Miden](https://polygon.technology/solutions/polygon-miden/)
e [Polygon Zero](https://polygon.technology/solutions/polygon-zero/).
La differenza principale è che Nightfall è un rollup incentrato sulla privacy e progettato per i casi d'uso aziendali, combinando
i concetti di optimistic rollup e crittografia Zero-Knowledge (ZK) per offrire transazioni private e scalabili.

Se da un lato Nightfall consente la scalabilità, dall'altro è destinato a rimuovere una delle principali barriere che le aziende incontrano oggi
nell'utilizzo della blockchain: la mancanza di privacy delle transazioni. Nightfall aggiunge un livello di privacy in modo che i parametri chiave delle transazioni (ad esempio il valore e la destinazione) non possano essere rintracciati. Queste due caratteristiche hanno alimentato l'interesse delle imprese private che vedono in Nightfall un modo per eseguire la loro logica aziendale e coordinarsi con la loro catena di fornitura in una rete decentralizzata a un prezzo sostenibile, il tutto mantenendo la sicurezza e privacy.

## I pilastri di Nightfall {#nightfall-s-pillars}

La principale proposta di valore di Polygon Nightfall è quella di consentire trasferimenti di dati sicuri, privati e a basso costo
in una rete decentralizzata.

![](../imgs/overview.png)

## Privacy {#privacy}

Polygon Nightfall utilizza le ZK proof per inviare transazioni private. Un utente può generare una ZK proof della
transazione senza rivelare i parametri chiave della transazione, come la destinazione o il valore della
transazione. Maggiori dettagli sulla componente privacy di Nightfall sono disponibili nella
guida al [protocollo](../protocol/protocol.md).

## Sicurezza {#security}

> Al momento è in corso un audit sulla sicurezza di Nightfall che dovrebbe essere completato alla metà di giugno del 2022.
> Una volta completato il processo di verifica, i risultati saranno pubblicati qui.

> Essendo una nuova rete con un periodo di avvio, Nightfall dispone di misure di sicurezza transitorie per
> proteggere il sistema con l'obiettivo di rimuoverle e lasciarlo completamente decentralizzato.

Polygon Nightfall è una costruzione Layer 2 perché sfrutta Ethereum prendendo in prestito la sua sicurezza come solida
blockchain pubblica. Nightfall si basa su alcuni presupposti che garantiscono il recupero degli asset. Questi presupposti si
basano su diverse decisioni progettuali e architettoniche che ruotano attorno agli ZK-SNARK, che utilizzano
alcune primitive crittografiche, come gli hash e le firme.
Infine, Nightfall incorpora regole operative in diversi smart contract per garantire che gli operatori non blocchino
le transazioni degli utenti e che questi ultimi possano prelevare i loro asset in qualsiasi momento.

In sintesi, Nightfall adotta i seguenti presupposti di sicurezza:

1. Presupposti di sicurezza di Ethereum.
2. Ipotesi Groth16 (ipotesi di conoscenza dell'esponente).
3. Alcuni presupposti crittografici di primitive come hash (Poseidon) e firme.
4. Presupposti di sicurezza del software che si basano su una corretta progettazione e implementazione.

## Efficienza {#efficiency}

I proponenti dei blocchi raccolgono le transazioni di vari utenti e le raggruppano in un blocco L2.
Le dimensioni tipiche dei blocchi L2 contengono circa 32 transazioni.

Le gas fee stimate per un deposito, un trasferimento e un prelievo sono rispettivamente 9.000, 1.200 e 9,500. Questo costo è dovuto alla memorizzazione di 574 Byte di dati di chiamata per ogni transazione, più alcuni
dati di chiamata fissi e il calcolo per elaborare un blocco L2. I costi saranno fino all'80% più bassi dopo [EIP 4488](https://eips.ethereum.org/EIPS/eip-4488).

## Trasferimenti non negati {#non-deniable-transfers}

Come parte della ZK proof della transazione di trasferimento, Nightfall include la crittografia dei segreti (indirizzo,
valore, id e salt del token) necessari per elaborare l'impegno trasferito. Questo costringe l'utente a criptare i segreti
con una chiave nota al destinatario. Poiché la chiave fa parte della ZK proof, il destinatario si affida alla negazione plausibile
in quanto il mittente può dimostrare che è stata utilizzata la chiave crittografica corretta.

## Decentralizzazione {#decentralization}

Validatori e [Challenger](docs/nightfall/protocol/actors) sono parte integrante di Nightfall. Assicurano che
le transazioni e i blocchi L2 vengano prodotti in modo tempestivo e corretto. Un meccanismo di consenso basato su proof-of-stake (PoS) viene
utilizzato per selezionare il prossimo [proponente](docs/nightfall/protocol/actors) del network. D'altro canto, i Challenger controllano
il corretto funzionamento del network lanciando sfide quando viene rilevato un blocco non corretto e trattenendo
lo stake avanzato dal proponente.


## A prova di futuro {#future-proof}
Grazie alla flessibilità fornita dall'implementazione Optimistic rollup di Nightfall, è possibile includere nuove transazioni
in futuro senza compromettere quelle esistenti, semplicemente definendo e registrando un nuovo tipo di circuito che implementi
la transazione in ZK.

## Riferimenti {#references}

1. [Un approccio multilaterale alla scalatura ZK](https://messari.io/article/polygon-a-multi-sided-approach-to-zk-scaling)
2. [L'opinione di Paul Brody su Nightfall](https://www.linkedin.com/pulse/say-hello-nightfall-paul-brody-1f/)
