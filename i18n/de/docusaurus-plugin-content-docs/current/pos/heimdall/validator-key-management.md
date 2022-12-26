---
id: validator-key-management
title: Validator-Schlüsselverwaltung
description: "Validator-Management von Signier- und Eigentümerschlüssel."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
Jeder Validator verwendet zwei Schlüssel, um validatorbezogene Aktivitäten auf Polygon zu verwalten:

1. **Signierschlüssel**

    Der Signierschlüssel ist die Adresse, die für das Signieren der Heimdall-Blöcke, Checkpoints und anderer Signier-Aktivitäten verwendet wird. Der private Schlüssel dieses Schlüssels wird auf dem Prüfknoten zu Signierzwecken gespeichert. Er kann nicht Stake, Prämien oder Delegationen verwalten.

    Der Validator muss zwei Arten von Salden auf dieser Adresse behalten:

    - Matic-Token auf Heimdall (durch Top-up-Transaktionen), um Validierungsaufgaben auf Heimdall wahrzunehmen
    - ETH auf der Ethereum-Chain zum Senden von Checkpoints auf Ethereum
2. **Eigentümerschlüssel**

    Der Eigentümerschlüssel ist eine Adresse, die für das Staking, Re-Stake, das Ändern des Signerschlüssels, das Einlösen von Prämien und die Verwaltung von delegationsbezogenen Parametern auf der Ethereum-Chain verwendet wird. Der Privatschlüssel für diesen Schlüssel muss um jeden Preis sicher sein.

Alle Transaktionen durch diesen Schlüssel werden auf der Ethereum-Chain durchgeführt.

Der Signierschlüssel wird auf Knoten gehalten und wird im Allgemeinen als `hot`-Wallet betrachtet, während der Eigentümerschlüssel sehr sicher gehalten wird, selten verwendet wird und allgemein als `cold`-Wallet gilt. Das eingesetzte Geld wird durch den Eigentümerschlüssel kontrolliert.

Diese Trennung von Zuständigkeiten wurde durchgeführt, um einen effizienten Tradeoff zwischen Sicherheit und Benutzerfreundlichkeit zu gewährleisten.

Beide Schlüssel sind Ethereum-kompatible Adressen und arbeiten exakt auf die gleiche Weise.

Es ist möglich, dieselben Eigentümer- und Signierschlüssel zu haben.

**Signiererwechsel**

Das folgende Ereignis wird im Falle eines Signiererwechsels auf der Ethereum-Chain `StakingInfo.sol`erzeugt: [https://github.com/maticnetwork/contracts/blob/develop/contracts/staking/StakingInfo.sol](https://github.com/maticnetwork/contracts/blob/develop/contracts/staking/StakingInfo.sol)

```go
// Signer change
event SignerChange(
  uint256 indexed validatorId,
  address indexed oldSigner,
  address indexed newSigner,
  bytes signerPubkey
);
```

Die Heimdall-Bridge verarbeitet diese Ereignisse und sendet Transaktionen an Heimdall, um den Status auf der Grundlage der Ereignisse zu ändern.