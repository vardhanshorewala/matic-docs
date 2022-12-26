---
id: auth
title: Auth
description: "Module zur Angabe der Basis-Transaktionen und Account-Typen."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
## Übersicht {#overview}

Dieses Dokument legt das `auth`-Modul für Heimdall fest.

Das `auth`-Modul ist dafür zuständig, die Basis-Transaktionen und Account-Typen für eine Anwendung zu spezifizieren. Es enthält den Vorabwickler, über welchen sämtliche Basis-Transaktions-Validitätsprüfungen (Signaturen, Noncen, Hilfsfelder) ausgeführt werden, und legt den Account-Hüter offen, was es anderen Modulen ermöglicht, Accounts zu lesen, zu überschreiben oder zu verändern.

## Gas und Gebühren {#gas-and-fees}

Gebühren dienen einem Netzwerkbetreiber in zweierlei Hinsicht.

Gebühren begrenzen das Wachstum des Status, der von jeder Full Node gepeichert wird und ermöglichen eine allgemeine Transaktionszensur mit nur geringem finanziellen Aufwand. Gebühren eignen sich bestens als Anti-Spam-Mechanismus, wodurch Validatoren das Interesse daran verlieren, das Netzwerk und die Benutzeridentitäten zu veruntreuen.

**Da Heimdall weder Kundensupport-Contracts noch -Codes für die Transaktionen nutzt, setzt es festgelegte kostenpflichtige Transaktionen ein.**

Für diese kostenpflichtigen Transaktionen können Validatoren ihre Accounts auf der Ethereum-Chain auftoppen und auf Heimdall Token über das [Top-up](topup)-Modul empfangen.

## Typen {#types}

Neben Accounts (im Status spezifizierte) sind es folgende Typen, die mittels des Auth-Moduls offengelegt werden: StdSignature, die Kombination eines Public Keys und einer kryptografischen Signatur als Byte-Array, StdTx, ein Konstrukt, das die -`sdk.Tx`Schnittstelle einsetzt, um ,`StdSignature` ,`StdSignDoc` zu nutzen, eine Struktur zur Wiederholungsvermeidung für ,`StdTx` welche die Transaktionsaussteller unterzeichnen müssen.

### StdSignature {#stdsignature}

Eine `StdSignature`ist ein Ausprägung eines Byte-Arrays.

```go
// StdSignature represents a sig
type StdSignature []byte
```

### **StdTx**

Ein `StdTx` ist ein Konstrukt, das die  `sdk.Tx` -Schnittstelle einsetzt; es besteht die Wahrscheinlichkeit, dass dieses ausreichend exemplarisch ist, um für eine Vielzahl von Transaktionstypen zu fungieren.

```go
type StdTx struct {
		Msg       sdk.Msg      `json:"msg" yaml:"msg"`
		Signature StdSignature `json:"signature" yaml:"signature"`
		Memo      string       `json:"memo" yaml:"memo"`
}
```

### StdSignDoc

Eine `StdSignDoc` ist eine Struktur zur Wiederholungsvermeidung, die unterzeichnet werden muss; sie stellt sicher, dass sämtliche übersendete Transaktionen (welche lediglich eine Signatur über einen bestimmten Byte-Strang darstellen) nur einmal auf Heimdall durchführbar sind.

```go
// StdSignDoc is replay-prevention structure.
// It includes the result of msg.GetSignBytes(),
// as well as the ChainID (prevent cross chain replay)
// and the Sequence numbers for each signature (prevent
// inchain replay and enforce tx ordering per account).
type StdSignDoc struct {
	ChainID       string          `json:"chain_id" yaml:"chain_id"`
	AccountNumber uint64          `json:"account_number" yaml:"account_number"`
	Sequence      uint64          `json:"sequence" yaml:"sequence"`
	Msg           json.RawMessage `json:"msg" yaml:"msg"`
	Memo          string          `json:"memo" yaml:"memo"`
}
```

### Account {#account}

Dieser verwaltet die Adressen, Coins und Noncen für die Transaktionen. Außerdem unterzeichnet und validiert er Transaktionen.

Quelle: [https://github.com/maticnetwork/heimdall/blob/master/auth/types/account.go#L32-L54](https://github.com/maticnetwork/heimdall/blob/master/auth/types/account.go#L32-L54)

```go
type BaseAccount struct {
		Address types.HeimdallAddress `json:"address" yaml:"address"`
		Coins types.Coins `json:"coins" yaml:"coins"`
		PubKey crypto.PubKey `json:"public_key" yaml:"public_key"`
		AccountNumber uint64 `json:"account_number" yaml:"account_number"`
		Sequence uint64 `json:"sequence" yaml:"sequence"`
}
```

## **Parameter**

Das Auth-Modul enthält folgende Parameter:

| Key | Typ | Standardwert |
|----------------------|------|------------------|
| MaxMemoCharacters | uint64 | 256 |
| TxSigLimit | uint64 | 7 |
| TxSizeCostPerByte | uint64 | 10 |
| SigVerifyCostED25519 | uint64 | 590 |
| SigVerifyCostSecp256k1 | uint64 | 1000 |
| DefaultMaxTxGas | uint64 | 1000000 |
| DefaultTxFees | string | "1000000000000000" |


## CLI-Befehle {#cli-commands}

### **Account ansehen**

Wie man Account-Daten nach Heimdall kopiert

```bash
heimdalld show-account
```

**Voraussichtliches Ergebnis:**

```json
{
	"address": "0x68243159a498cf20d945cf3E4250918278BA538E",
	"pub_key": "0x040a9f6879c7cdab7ecc67e157cda15e8b2ddbde107a04bc22d02f50032e393f6360a05e85c7c1ecd201ad30dfb886af12dd02b47e4463f6f0f6f94159dc9f10b8"
}
```

### **Details zu Account und Coins**

Wie lassen sich Account-Details, Coins, Sequenz- und Account-Nummer anzeigen:

```bash
heimdallcli query auth account 0x68243159a498cf20d945cf3E4250918278BA538E --trust-node
```

**Voraussichtliches Ergebnis**:

```json
address: 0x68243159a498cf20d945cf3e4250918278ba538e
coins:
- denom: matic
    amount:
    i: "1000000000000000000000"
pubkey: ""
accountnumber: 0
sequence: 0
```

### Parameter {#params}

Alle Parameter kopieren

```go
heimdallcli query auth params
```

**Voraussichtliches Ergebnis:**

```go
max_memo_characters: 256
tx_sig_limit: 7
tx_size_cost_per_byte: 10
sig_verify_cost_ed25519: 590
sig_verify_cost_secp256k1: 1000
max_tx_gas: 1000000
tx_fees: "1000000000000000"
```

## REST APIs {#rest-apis}

| Name | Endpunkt | Beschreibung |
|----------------------|--------|------------------|
| Account-Details | /auth/accounts/{address} | Gibt alle Details für eine Adresse zurück |
| Details zu Accountsequenzen | /auth/accounts/{address}/sequenz | Gibt nur für die Unterzeichnung notwendige Details zurück |
| Auth-Parameter | /auth/params | Gibt alle Parameter zurück, die das Auth-Modul verwendet |
