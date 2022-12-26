---
id: types
title: Arten
description: "Beschreibung der HeimdallAddress, des Pubkeys & des HeimdallHash."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
## HeimdallAddress {#heimdalladdress}

`HeimdallAddress` steht für Adresse auf Heimdall. Sie greift für die Adresse auf Ethereums gemeinsame Bibliothek zurück. Die Adressenlänge beträgt 20 Bytes.

```go
// HeimdallAddress represents Heimdall address
type HeimdallAddress common.Address
```

## PubKey {#pubkey}

Dies steht für den in Heimdall verwendeten Public Key und `ecdsa`bezeichnet einen kompatiblen, unkomprimierten Public Key:

```go
// PubKey pubkey
type PubKey [65]byte
```

## HeimdallHash {#heimdallhash}

Dies steht für einen Hash auf Heimdall. Er wird wie der Ethereum-Hash verwendet.

```go
// HeimdallHash represents heimdall address
type HeimdallHash common.Hash
```
