---
id: state-sync
title: State-Sync-Mechanismus
description: "Mechanismus, um Ethereum-Daten von der Matic-EVM-Chain auszulesen."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
`State Sync` ist der ursprüngliche Mechanismus, um Ethereum-Daten von der Matic-EVM-Chain auszulesen.

Validatoren auf der Heimdall-Layer greifen das [StateSynced](https://github.com/maticnetwork/contracts/blob/a4c26d59ca6e842af2b8d2265be1da15189e29a4/contracts/root/stateSyncer/StateSender.sol#L24)-Ereignis auf und geben es an die Bor-Layer weiter (lies mehr über die Architektur [hier](/docs/pos/bor/overview).

Der Empfänger-Contract erbt [IStateReceiver](https://github.com/maticnetwork/genesis-contracts/blob/master/contracts/IStateReceiver.sol) und die benutzerdefinierte Logik befindet sich in der Funktion [onStateReceive](https://github.com/maticnetwork/genesis-contracts/blob/05556cfd91a6879a8190a6828428f50e4912ee1a/contracts/IStateReceiver.sol#L5).


Dies ist der Flow, der für Dapps/Benutzer erforderlich ist, um mit State-Sync zu arbeiten:

1. Rufe die Smart Contract-Funktion hier auf: [https://github.com/maticnetwork/Contracts/blob/19163ddecf91db17333859ae72dd73c91bee6191/Contracts/root/stateSyncer/StateSender.sol#L33](https://github.com/maticnetwork/contracts/blob/19163ddecf91db17333859ae72dd73c91bee6191/contracts/root/stateSyncer/StateSender.sol#L33)
2. Welche ein Ereignis ausgibt, das sich `StateSynced(uint256 indexed id, address indexed contractAddress, bytes data);` nennt
3. Alle Validatoren auf der Heimdall-Chain erhalten dieses Ereignis und einer von ihnen, wer auch immer es wünscht, die tx-Gebühren für State-Sync zu erhalten, sendet diese Transaktion an Heimdall
4. Sobald die `state-sync`-Transaktion auf Heimdall in einem Block eingeschlossen wurde, wird sie der ausstehenden State-Sync-Liste hinzugefügt.
5. Nach jedem Sprint auf  greift `bor`der `bor`-Knoten die ausstehenden State-Sync-Ereignisse von Heimdall über einen API-Aufruf auf.
6. Der Empfänger-Contract erbt die `IStateReceiver` -Schnittstelle, und die benutzerdefinierte Logik zum Dekodieren der Datenbytes und zum Ausführen von Aktionen befindet sich in der `onStateReceive` -Funktion: [https://github.com/maticnetwork/genesis-contracts/blob/master/contracts/IStateReceiver.sol](https://github.com/maticnetwork/genesis-contracts/blob/master/contracts/IStateReceiver.sol)
