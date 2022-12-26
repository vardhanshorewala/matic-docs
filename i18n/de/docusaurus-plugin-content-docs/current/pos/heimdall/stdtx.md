---
id: stdtx
title: StdTx
description: "Eine Standardlösung, um ein Msg mit einer Gebühr und Signaturen zu versehen."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
Quelle: [https://github.com/maticnetwork/heimdall/blob/master/auth/types/stdtx.go](https://github.com/maticnetwork/heimdall/blob/master/auth/types/stdtx.go)

Heimdalls `StdTx` verwendet `Fee` nicht für jede Transaktion. Wie verfügen über eine begrenzte Anzahl von Transaktionsarten und da die Endbenutzer keinerlei Contracts auf Heimdall anwenden werden, wird ein festgelegtes Gebührenmodell für die Transaktion angewendet.

Sieh hier nach: [https://github.com/maticnetwork/heimdall/blob/master/auth/ante.go#L32](https://github.com/maticnetwork/heimdall/blob/master/auth/ante.go#L32)

    // StdTx ist eine Standardlösung, um ein Msg mit einer Gebühr und Signaturen zu versehen. type StdTx struct {
    	Msg       sdk.Msg      `json:"msg" yaml:"msg"`
    	Signature StdSignature `json:"signature" yaml:"signature"`
    	Memo      string       `json:"memo" yaml:"memo"`
    }