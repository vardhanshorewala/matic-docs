---
id: actors
title: Partecipanti
sidebar_label: Actors
description: "Tipi di partecipanti in Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - transactor
  - proposer
  - challenger
  - liquidity
  - provider
image: https://matic.network/banners/matic-network-16x9.png
---

I partecipanti coinvolti nella rete sono quattro:

- [Transattori](#transactor)
- [Proponenti](#proposer)
- [Challenger](#challenger)

## Transattore {#transactor}
Un Transattore è un cliente abituale del servizio. Desidera effettuare transazioni, cioè depositare, trasferire e prelevare privatamente. Questi clienti in genere utilizzano un wallet web o un server dedicato (Client) per eseguire le prove ZK necessarie a generare le transazioni.

## Proponente {#proposer}
Un proponente raccoglie le transazioni dei clienti e propone nuovi aggiornamenti allo stato del contratto Shield. Per stato intendiamo in particolare le variabili di archiviazione associate a una transazione ZKP:
nullifier e root di impegno.
Le proposte di aggiornamento contengono diverse transazioni, raggruppate in un blocco Layer 2. Solo un hash
dello stato finale che esisterebbe dopo l'elaborazione di tutte le transazioni del blocco
è memorizzato on-chain. Le transazioni diventano definitive dopo un periodo di una settimana.

Chiunque può diventare un proponente, ma deve vincolare dello stake. Lo stake ha lo scopo di incentivare il buon comportamento.
I proponenti guadagnano fornendo blocchi corretti e riscuotendo le commissioni dai transattori. Sono in qualche modo analoghi ai miner di una blockchain convenzionale.

## Challenger {#challenger}
Un Challenger controlla la correttezza dei blocchi proposti entro una settimana dall'invio del blocco. Tutti possono rivestire il ruolo di Challenger. I Challenger accettano lo stake posto dai proponenti per la costruzione dei loro blocchi quando inviano con successo una sfida.


## Note {#notes}
Nell'implementazione di riferimento di Polygon, sia il proponente che il Challenger scaricano alcune funzionalità su un modulo comune chiamato Optimist.
Questo modulo Optimist fornisce alcuni servizi a un certo numero di Proponenti e Challenger, come la generazione e la contestazione di blocchi
(il proponente e i challenger dovranno firmare queste transazioni), la sincronizzazione con gli eventi della blockchain, ecc.

Oltre ai partecipanti descritti in precedenza, ne esiste un altro chiamato Client. Un Client funge da servizio fidato che raccoglie le transazioni degli utenti, esegue le ZK Proof per loro conto, invia le transazioni al Proponente, ascolta gli eventi della Blockchain ecc. In sintesi, il Client agisce come relayer di fiducia per un insieme di utenti che vogliono scaricare il calcolo di prove pesanti e che si fidano l'uno dell'altro.

L'alternativa al client è l'utilizzo del wallet browser, un servizio serverless fornito da Polygon. Questo wallet gestisce tutte le attività di transazione per un singolo utente mantenendo la privacy.
