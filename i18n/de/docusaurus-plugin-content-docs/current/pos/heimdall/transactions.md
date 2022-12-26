---
id: transactions
title: Transactions
description: Was sind Transaktionen und wann werden sie verwendet?
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Transaktionen bestehen aus Metadaten, die in [Kontexten](https://docs.cosmos.network/master/core/context.html) und [Nachrichten](https://docs.cosmos.network/master/building-modules/messages-and-queries.html) gespeichert sind und über den [Handler](https://docs.cosmos.network/master/building-modules/handler.html) des Moduls Zustandsänderungen innerhalb des Moduls auslösen.

Wenn Benutzer mit einer Anwendung interagieren und Zustandsänderungen vornehmen wollen (z. B. das Senden von Coins), erstellen sie Transaktionen. Jede `message` einer Transaktion muss mit dem Privatschlüssel des entsprechenden Kontos signiert werden, bevor die Transaktion an das Netzwerk übermittelt wird. Eine Transaktion muss dann in einen Block aufgenommen, validiert und anschließend vom Netzwerk durch den Konsensprozess genehmigt werden. Um mehr über den Lebenszyklus einer Transaktion zu erfahren, klicken Sie [hier](https://docs.cosmos.network/master/basics/tx-lifecycle.html).

## **Typdefinition**

Transaktionsobjekte sind SDK-Typen, die die Schnittstelle `Tx` implementieren.

```go
type Tx interface {
	// Gets all the transaction's messages.
	GetMsgs() []Msg

	// ValidateBasic does a simple and lightweight validation check that doesn't
	// require access to any other information.
	ValidateBasic() Error
}
```

Weitere Informationen zu Transaktionen: [https://docs.cosmos.network/master/core/transactions.html](https://docs.cosmos.network/master/core/transactions.html)