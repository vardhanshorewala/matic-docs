---
id: governance
title: Governance
sidebar_label: Governance
description: "System auf Grundlage von 1 Token - 1 Stimme"
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
## Übersicht {#overview}

Die Heimdall-Governance funktioniert genauso wie das Cosmos-SDK `x/gov`-Modul. [https://docs.cosmos.network/master/modules/gov/](https://docs.cosmos.network/master/modules/gov/)

In diesem System können Inhaber, die den nativen Staking-Token auf der Chain halten, über Vorschläge auf einer `1 token = 1 vote`-Basis abstimmen. Es folgt eine Liste der Funktionen, die das Modul derzeit unterstützt:

- **Einreichen eines Vorschlags:** Validatoren können Vorschläge mit einer Einzahlung einreichen. Sobald die Mindesteinzahlung erreicht ist, tritt der Vorschlag in die Abstimmungsperiode ein. Validatoren, die auf Vorschläge Einzahlungen hinterlegten, können ihre Einlagen wieder zurückgewinnen, sobald der Vorschlag abgelehnt oder angenommen wurde.
- **Abstimmen:** Validatoren können über Vorschläge abstimmen, die MinDeposit erreicht haben

Es gibt die Einzahlungsperiode und die Abstimmungsperiode als Parameter im `gov`-Modul. Die Mindesteinzahlung wurde erreicht, bevor die Einzahlungsperiode endet, andernfalls wird der Vorschlag automatisch abgelehnt werden.

Sobald die Mindesteinzahlung innerhalb der Einzahlungsperiode erreicht wurde, startet die Abstimmungsperiode. In der Abstimmungsperiode sollten alle Validatoren ihre Stimme zum Vorschlag abgeben. `threshold`Nach Ablauf der Abstimmungsperiode führt `gov/Endblocker.go`  die `tally`-Funktion aus und nimmt den Vorschlag an oder lehnt in ab, basierend auf  — `quorum`, `tally_params`und `veto`.

Quelle: [https://github.com/maticnetwork/heimdall/blob/develop/gov/endblocker.go](https://github.com/maticnetwork/heimdall/blob/develop/gov/endblocker.go)

Es gibt verschiedene Arten von Vorschlägen, die auf Heimdall umgesetzt werden können, doch derzeit wird nur eine Vorschlagsart unterstützt:

- Vorschlag zur Änderung von Parametern

### **Vorschlag zur Änderung von Parametern**

Mithilfe dieser Art von Vorschlag können Validatoren jedweden `params`in einen beliebigen Heimdall-`module` einwechseln. Beispiel: Wechseln des Minimum-`tx_fees` für eine Transaktion in ein `auth`-Modul. Wenn der Vorschlag angenommen wird, wechselt er das `params` automatisch in den Heimdall-Status. Es werden keine zusätzlichen TX benötigt.

## CLI-Befehle {#cli-commands}

### Abfrage von Governance-Parametern {#query-gov-params}

```go
heimdallcli query gov params --trust-node
```

Dies zeigt alle Parameter für das Governance-Modul an.

```go
voting_params:
  voting_period: 48h0m0s
tally_params:
  quorum: "334000000000000000"
  threshold: "500000000000000000"
  veto: "334000000000000000"
deposit_parmas:
  min_deposit:
  - denom: matic
    amount:
      i: "10000000000000000000"
  max_deposit_period: 48h0m0s
```

### Einreichung des Vorschlags {#submit-proposal}

```bash
heimdallcli tx gov submit-proposal \
	--validator-id 1 param-change proposal.json \
	--chain-id <heimdall-chain-id>
```

`proposal.json` ist eine Datei, welche den Vorschlag im json-Format enthält.

```go
{
  "title": "Auth Param Change",
  "description": "Update max tx gas",
  "changes": [
    {
      "subspace": "auth",
      "key": "MaxTxGas",
      "value": "2000000"
    }
  ],
  "deposit": [
    {
      "denom": "matic",
      "amount": "1000000000000000000"
    }
  ]
}
```

### Abfrage des Vorschlags {#query-proposal}

Abfrage aller Vorschläge

```go
heimdallcli query gov proposals --trust-node
```

Abfrage eines bestimmten Vorschlags

```go
heimdallcli query gov proposals 1 --trust-node
```

### Abstimmen über einen Vorschlag {#vote-on-proposal}

Wie man über einen bestimmten Vorschlag abstimmen kann

```bash
heimdallcli tx gov vote 1 "Yes" --validator-id 1  --chain-id <heimdal-chain-id>
```

Der Vorschlag wird nach Ablauf der Abstimmungsperiode automatisch abgehakt.

## REST APIs {#rest-apis}

| Name | Methode | Endpunkt |
|----------------------|------|------------------|
| Hole dir alle Vorschläge | HOLEN | /gov/proposals |
| Hole dir die Details des Vorschlags. | HOLEN | /gov/proposals/`proposal-id` |
| Hole dir alle Stimmen für den Vorschlag. | HOLEN | /gov/proposals/`proposal-id`/votes |
