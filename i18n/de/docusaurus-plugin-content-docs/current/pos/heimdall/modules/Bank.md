---
id: bank
title: Bank
description: "Modul für Kontostandsübertragungen für Heimdall."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
## Übersicht {#overview}

Mit dem Modul `bank` werden die Kontostandsübertragungen für Heimdall abgewickelt. Dieses Modul entspricht dem Modul `bank` von cosmos-sdk.

## Nachrichten {#messages}

### MsgSend {#msgsend}

`MsgSend` wickelt übertragen zwischen Konten in Heimdall ab. Hier ist eine Struktur für Transaktionsmitteilungen:

```go
// MsgSend - high-level transaction of the coin module
type MsgSend struct {
	FromAddress types.HeimdallAddress `json:"from_address"`
	ToAddress   types.HeimdallAddress `json:"to_address"`
	Amount      types.Coins           `json:"amount"`
}
```

### MsgMultiSend {#msgmultisend}

`MsgMultiSend` wickelt mehrere Übertragungen zwischen Konten für Heimdall ab.

```go
// MsgMultiSend - high-level transaction of the coin module
type MsgMultiSend struct {
	Inputs  []Input  `json:"inputs"`
	Outputs []Output `json:"outputs"`
}
```

## **Parameter**

Das Bankmodul enthält die folgenden Parameter:

| Key | Typ | Standardwert |
|----------------------|--------|------------------|
| `sendenabled` | bool | true |

## CLI-Befehle {#cli-commands}

### Saldo senden {#send-balance}

Der folgende Befehl sendet 1000 Matic-Token an die genannte `address`.

```bash
heimdallcli tx bank send <address> 1000matic --chain-id <chain-id>
```
