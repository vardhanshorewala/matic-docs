---
id: polygon-architecture
title: Übersicht
description: Polygons Architektur
keywords:
  - architecture
  - layers
  - polygon
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## Polygon {#polygon}

Polygon ist eine Blockchain-Anwendungsplattform, die hybride Proof-of-Stake- und Plasma-fähige Sidechains anbietet.

Die Schönheit von Polygon liegt in seiner Architektur, also im eleganten Design, das eine generische Validation-Layer bietet, die von unterschiedlichen Ausführungsumgebungen wie Plasma-fähigen Chains sowie vollwertigen EVM-Sidechains und künftig auch von anderen Layer-2-Ansätzen wie Optimistic-Rollups getrennt ist.

Das Polygon PoS-Netzwerk verfügt über eine dreischichtige Architektur:

* Ethereum-Layer – eine Reihe von Contracts auf dem Ethereum Mainnet.
* Heimdall-Layer – eine Reihe von Proof-of-Stake-Heimdall-Knoten, die parallel zum Ethereum Mainnet laufen; diese überwachen die eingesetzten Staking-Contracts im Ethereum Mainnet und sie übermitteln die Polygon Netzwerk.-Checkpoints an das Ethereum Mainnet. Heimdall basiert auf Tendermint.
* Bor-Layer– eine Reihe von blockproduzierenden Bor-Knoten gemischt mit Heimdall-Knoten. Bor basiert auf Go Ethereum.

<img src={useBaseUrl("img/staking/architecture.png")} />

Derzeit können Entwickler **Plasma** für bestimmte Statusübergänge für welche Plasma-Prädikate
geschrieben wurden, darunter ERC20, ERC721, Asset Swaps oder andere benutzerdefinierte Prädikate, verwenden. Für beliebige Statusübergänge
kann PoS verwendet werden. Oder beide! Dies wird durch Polygons hybride Bauweise ermöglicht.

Um den PoS-Mechanismus auf unserer Plattform zu aktivieren, werden eine Reihe von **Staking**-Management-Contracts auf
Ethereum bereitgestellt sowie eine Auswahl an anreizbasierten Validatoren, die **Heimdall**- und **Bor**-Knoten betreiben. Ethereum ist
die erste Basechain, die Polygon unterstützt. Polygon hat aber außerdem vor, auf der Grundlage von Vorschlägen und Konsens der Community, Support für weitere Basechains anzubieten,
um eine interoperable dezentrale Layer-2-Blockchain-Plattform zu ermöglichen.

<img src={useBaseUrl("img/matic/Architecture.png")} />;

## Staking-Contracts {#staking-contracts}

Um den [Proof of Stake/PoS-](docs/home/polygon-basics/what-is-proof-of-stake)Mechanismus auf Polygon zu ermöglichen,
wendet das System eine Reihe von [Staking](/docs/maintain/glossary#staking)-Management-Contracts im Ethereum Mainnet an.

Die Staking-Verträge implementieren die folgenden Funktionen:

* Jeder kann Matic-Token auf den [Staking-Contracts](/docs/maintain/glossary#validator) im Ethereum Mainnet staken und dem System als Validator beitreten.
* Verdiene Staking-Prämien für die Validierung von Statusübergängen auf dem Polygon-Netzwerk.
* Strafen/Slashing für Aktivitäten wie Double-Signing, Validatoren-Ausfallzeit usw. aktivieren
* [Checkpoints](/docs/maintain/glossary#checkpoint-transaction) im Ethereum Mainnet abspeichern.

Der PoS-Mechanismus dient auch dazu, das Problem der Nichtverfügbarkeit von Daten für die Polygon-Sidechains zu mildern.

## Heimdall {#heimdall}

Heimdall ist die Proof-of-Stake/PoS-Validierungslayer, die sich darum kümmert,
von [Bor](/docs/maintain/glossary#bor) produzierte Blöcke in einen Merkle-Baum zu aggregieren; außerdem veröffentlicht es die Merkle-Wurzel in regelmäßigen Abständen an die
Root-Chain. Die regelmäßige Veröffentlichung von Snapshots der Bor-Sidechain werden [Checkpoints](/docs/maintain/glossary#checkpoint-transaction) genannt.

1. Überprüft alle Blöcke seit dem letzten Checkpoint.
2. Erstellt einen Merkle-Baum des Block-Hashes.
3. Veröffentlicht den Merkle-Root-Hash im Ethereum Mainnet.

Checkpoints sind aus zwei Gründen wichtig:

1. Bereitstellung von Finalität auf der Root Chain.
2. Gewährleistung des Proof-of-Burn bei der Abhebung von Assets.

Eine Übersicht des Prozesses:

* Eine Untermenge von aktiven Validatoren aus dem Pool wird ausgewählt, um für eine [Spanne](/docs/maintain/glossary#span) als [Blockproduzenten](/docs/maintain/glossary#block-producer) zu fungieren. Diese Blockproduzenten sind für die Erstellung von Blöcken und die Verbreitung der erstellten Blöcke im Netzwerk verantwortlich.
* Ein Checkpoint enthält die Merkle-Root-Hash aller Blöcke, die während eines bestimmten Intervalls erstellt wurden. Alle Knoten prüfen dieselbe Merkle-Root-Hash und fügen ihr ihre Signatur hinzu.
* Ein ausgewählter [Proposer](/docs/maintain/glossary#proposer) aus der Validatoren-Gruppe ist dafür verantwortlich, alle Signaturen für einen bestimmten Checkpoint zu sammeln und in das Ehtereum Mainnet zu übertragen.
* Die Zuständigkeit für die Erstellung von Blöcken und das Vorschlagen von Checkpoints hängt von dem Stake eines Validators am Gesamtpool ab.

Mehr Details zu [Heimdall](/docs/pos/heimdall/overview) sind im Leitfaden zur Heimdall-Architektur zu finden.

### Bor {#bor}

Bor ist Polygons Sidechain-Blockproduzent – die Entität, die für die Zusammenfassung von Transaktionen zu Blöcken verantwortlich ist.

Bor-Blockproduzenten sind eine Untermenge der Validatoren und werden regelmäßig von den Validatoren von [Heimdall](/docs/maintain/glossary#heimdall) durchgemischt.

Siehe auch [Bor-Architektur](/docs/pos/bor/overview).

Bor ist Polygons Block-Producer-Layer – die für die Aggregation von Transaktionen zu Blöcken zuständige Einheit.  Derzeit handelt es sich um eine grundlegende Geth-Implementierung mit benutzerdefinierten Änderungen am Konsensalgorithmus.

Block-Produzenten werden regelmäßig über die Komitee-Selektion auf Heimdall in Zeitabständen,
die auf Polygon `span` genannt werden, durchgemischt. Blöcke werden am **Bor**-Knoten produziert, und die VM-Sidechain ist EVM-kompatibel. Blöcke, die auf Bor produziert wurden, werden ebenfalls regelmäßig von Heimdall-Knoten validiert und ein Checkpoint, der
aus einem Merkle-Baum-Hash aus einer Reihe von Blöcken auf Bor besteht, wird in regelmäßigen Abständen zu Ethereum übermittelt.

Weitere Details sind im Leitfaden für die [Bor-Architektur](/docs/pos/bor/overview) zu finden.

### Ressourcen {#resources}

* [Bor-Architektur](https://forum.polygon.technology/t/matic-system-overview-bor/9123)
* [Heimdall-Architektur](https://forum.polygon.technology/t/matic-system-overview-heimdall/8323)
* [Checkpoint-Mechanismus](https://forum.polygon.technology/t/checkpoint-mechanism-on-heimdall/7160)
