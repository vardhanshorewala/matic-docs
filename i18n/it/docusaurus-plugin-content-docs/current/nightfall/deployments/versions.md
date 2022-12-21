---
id: versions
title: Cronologia
sidebar_label: History of changes
description: "Versioni distribuite"
keywords:
  - docs
  - polygon
  - nightfall
  - changelog
image: https://matic.network/banners/matic-network-16x9.png
---


## Beta 1.0 {#beta-1-0}
La Beta 1.0 è stata pubblicata il 17 maggio 2022. Includeva il meccanismo di base per l'implementazione della proof-of-concept Nightfall. `Proposer`Supportava una prima `coarse`implementazione singola delle transazioni. Forniva anche una versione preliminare di un wallet per gli utenti. [Qui](https://github.com/EYBlockchain/nightfall_3/commit/bc3e475de3e2877f14430f9599e5b38ea960765b) è possibile trovare la versione distribuita

## Beta 2.0 {#beta-2-0}
[Qui](https://github.com/EYBlockchain/nightfall_3/commit/4c2af01ac95af5ea6f5b40071d73a1624f06ba46) è possibile trovare la versione distribuita Sono stati apportati diversi miglioramenti:
- **Raccolta delle commissioni**

Possibilità per i proponenti di raccogliere le commissioni per le transazioni. Questa funzionalità incentiverà la presenza di molteplici proponenti.
- **Implementazione del Challenger**

La rete adesso include uno challenger che monitora i blocchi del proponente.
- **Transazioni dei circuiti**

Maggiore flessibilità e prestazioni migliorate nella generazione dello ZKP di una qualsiasi transazione. Sia `transfer`che `withdrawal` accettano fino a due impegni e modifiche di rendimento. Per quanto riguarda le prestazioni, l'ottimizzazione permette di convalidare le transazioni in minor tempo.

| Operazioni | Vincoli prima dell'implementazione | Vincoli dopo l'implementazione |
|-----------|--------------------|------------------|
| Depositare | 84.766 | 1.277 |
| Metodo Transfer | 499.119 | 67.694 |
| Prelevare | 168.883 | 53.348 |

Parte dell'ottimizzazione è stata resa possibile dal passaggio a Poseidon

- **Crittografia delle chiavi segrete**

Ci siamo spostati da El-Gamal a un processo crittografico [KEM-DEM](../protocol/secrets), ottenendo così numerosi vantaggi:
- Semplificazione del processo di crittografia/decrittazione
- Riduzione dei vincoli e dei costi del gas on-chain.

- **Implementazione del Challenger**

