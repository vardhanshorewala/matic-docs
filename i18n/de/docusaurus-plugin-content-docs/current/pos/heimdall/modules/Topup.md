---
id: topup
title: Top-up
description: "Betrag, der für die Bezahlung von Gebühren auf der Heimdall-Chain verwendet werden wird."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
## Übersicht {#overview}

Das Heimdall-Top-up ist der Betrag, der für die Bezahlung von Gebühren auf der Heimdall-Chain verwendet werden wird.

Es gibt zwei Möglichkeiten, deinen Account aufzutoppen.

1. Wenn sich ein neuer Validator anschließt, kann dieser zusätzlich zu dem gestakten Betrag einen `topup`-Betrag als Top-up angeben, welcher als Saldo auf die Heimdall-Chain verschoben werden wird, um die Gebühren auf Heimdall zu bezahlen
2. Benutzer können die Top-up-Funktion direkt auf dem Staking-Smart Contract auf Ethereum abrufen, um ihr Top-up-Saldo auf Heimdall zu erhöhen

## Nachrichten {#messages}

### MsgTopup {#msgtopup}

Die `MsgTopup`-Transaktion ist dafür zuständig, das Saldo auf eine Adresse auf Heimdall zu minten, welche wiederum auf einem `TopUpEvent` auf der Ethereum-Chain, der auf dem Staking-Manager-Contract liegt, basiert.

Der Abwickler dieser Transaktion führt das Top-up aus und erhöht den Saldo nur einmal für jedes vorliegende `msg.TxHash` und `msg.LogIndex`. Beim Versuch, das Top-up mehr als einmal auszuführen, wird der Fehler `Older invalid tx found` angezeigt.

Hier siehst du die Struktur einer Top-Up-Transaktionsnachricht:

```go
type MsgTopup struct {
	FromAddress types.HeimdallAddress `json:"from_address"`
	ID          types.ValidatorID     `json:"id"`
	TxHash      types.HeimdallHash    `json:"tx_hash"`
	LogIndex    uint64                `json:"log_index"`
}
```

### MsgWithdrawFee {#msgwithdrawfee}

`MsgWithdrawFee`Die -Transaktion ist dafür zuständig, Auszahlungen vom Saldo der Heimdall- auf die Ethereum-Chain auszuführen. Ein Validator kann einen beliebigen Betrag von Heimdall abheben.

Der Abwickler verarbeitet die Auszahlung, indem er den Saldo vom jeweiligen Validators abzieht und den Status vorbereitet, um ihn an den nächsten Checkpoint zu senden. Der nächstmögliche Checkpoint wird den mit der Abhebung verbundenen Status für den bestimmten Validator enthalten.

Der Abwickler erhält die Information über den Validator basierend auf `ValidatorAddress` und verarbeitet die Abhebung.

```go
// MsgWithdrawFee - high-level transaction of the fee coin withdrawal module
type MsgWithdrawFee struct {
	ValidatorAddress types.HeimdallAddress `json:"from_address"`
	Amount           types.Int             `json:"amount"`
}
```

## CLI-Befehle {#cli-commands}

### Top-up-Gebühr {#topup-fee}

```bash
heimdallcli tx topup fee
	--log-index <log-index>
	--tx-hash <transaction-hash>
	--validator-id <validator ID here>
	--chain-id <heimdall-chain-id>
```

### Abhebungsgebühr {#withdraw-fee}

```bash
heimdallcli tx topup withdraw --chain-id <heimdall-chain-id>
```

Zur Kontrolle des auf dem Account reflektierten Top-ups führe folgenden Befehl aus

```bash
heimdallcli query auth account <validator-address> --trust-node
```

## REST APIs {#rest-apis}

| Name | Methode | URL | Body-Parameter |
|----------------------|------|------------------|-------------------------------------------------------------------------------------------------------------------------------------------------|
| Top-up-Gebühren | POST | /topup/fee | `id`Validator-ID, `tx_hash` Transaktions-Hash eines erfolgreichen Top-up-Ereignisses auf der Ethereum-Chain, `log_index` Log-Index eines auf der Ethereum-Chain ausgestellten Top-up-Ereignisses |
| Abhebunggebühr | POST | /topup/withdraw | `amount` Betrag abheben |
