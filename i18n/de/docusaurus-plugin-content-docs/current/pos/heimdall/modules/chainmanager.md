---
id: chainmanager
title: Chain-Manager
description: "Modul, das alle erforderlichen Abhängigkeiten bereitstellt."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
## Übersicht {#overview}

Dokument gibt einen Überblick über das Chain-Manager-Modul von Heimdall.

Dieses Modul stellt alle erforderlichen Abhängigkeiten wie `contract-addresses`, `bor_chain_id,` und `tx_confirmation_time` bereit. Weitere Parameter können später hinzugefügt werden.

Parameter werden über das Modul `gov` aktualisiert.

## Arten {#types}

Die Chainmanager-Struktur auf Heimdall sieht wie folgt aus:

```go
type ChainParams struct {
	// BorChainID is valid bor chainId
	BorChainID            string                  `json:"bor_chain_id" yaml:"bor_chain_id"`

	// MaticTokenAddress is valid matic token address
	MaticTokenAddress     hmTypes.HeimdallAddress `json:"matic_token_address" yaml:"matic_token_address"`

	// StakingManagerAddress is valid contract address
	StakingManagerAddress hmTypes.HeimdallAddress `json:"staking_manager_address" yaml:"staking_manager_address"`

	// RootChainAddress is valid contract address
	RootChainAddress      hmTypes.HeimdallAddress `json:"root_chain_address" yaml:"root_chain_address"`

	// StakingInfoAddress is valid contract address
	StakingInfoAddress    hmTypes.HeimdallAddress `json:"staking_info_address" yaml:"staking_info_address"`

	// StateSendedAddress is valid contract address
	StateSenderAddress    hmTypes.HeimdallAddress `json:"state_sender_address" yaml:"state_sender_address"`

	// Bor Chain Contracts
	// StateReceiveAddress is valid contract address
	StateReceiverAddress hmTypes.HeimdallAddress `json:"state_receiver_address" yaml:"state_receiver_address"`

	// ValidatorSetAddress is valid contract address
	ValidatorSetAddress  hmTypes.HeimdallAddress `json:"validator_set_address" yaml:"validator_set_address"`
}
```

## CLI Befehle {#cli-commands}

### Params {#params}

Alle Parameter kopieren

```go
heimdallcli query chainmanager params --trust-node
```

### Erwartetes Ergebnis {#expected-result}

```yaml
tx_confirmation_time: 12s
chain_params:
  bor_chain_id: "15001"
  matic_token_address: "0x0000000000000000000000000000000000000000"
  staking_manager_address: "0x0000000000000000000000000000000000000000"
  root_chain_address: "0x0000000000000000000000000000000000000000"
  staking_info_address: "0x0000000000000000000000000000000000000000"
  state_sender_address: "0x0000000000000000000000000000000000000000"
  state_receiver_address: "0x0000000000000000000000000000000000000000"
  validator_set_address: "0x0000000000000000000000000000000000000000"
```

### REST APIs {#rest-apis}

| Name | Methode | URL |
|----------------------|------|------------------|
| Parameter | HOLEN | chainmanager/params |


Alle Abfrage-APIs haben das folgende Format:

```json
{
	"height": "1",
	"result": {
		...	  
	}
}
```
