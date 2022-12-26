---
id: encoder
title: Encoder (Pulp)
description: "RLP-Kodierung zur Erzeugung spezieller Transaktionen, wie Checkpoint."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
## Pulp {#pulp}

Quelle: [https://github.com/maticnetwork/heimdall/blob/master/auth/types/pulp.go](https://github.com/maticnetwork/heimdall/blob/master/auth/types/pulp.go)

Heimdall muss die Transaktionen von Heimdall in der Ethereum Chain verifizieren. Dazu verwendet es RLP-Kodierung, um spezielle Transaktionen wie Checkpoint zu erzeugen.

Diese spezielle Transaktion verwendet die Kodierung durch `pulp` (RLP-basiert) anstelle der Standard-Aminokodierung.

Pulp verwendet einen präfixbasierten einfachen Kodierungsmechanismus, um die Schnittstellendekodierung zu lösen. Methode `GetPulpHash` überprüfen.

```go
const (
	// PulpHashLength pulp hash length
	PulpHashLength int = 4
)

// GetPulpHash returns string hash
func GetPulpHash(name string) []byte {
	return crypto.Keccak256([]byte(name))[:PulpHashLength]
}
```

Die folgende Funktion liefert Präfix-Bytes für eine gegebene `msg`.  Hier ein Beispiel für die Registrierung eines Objekts für die Pulp-Kodierung.

```go
RegisterConcrete(name, obj) {
	rtype := reflect.TypeOf(obj)
	// set record for name => type of the object
	p.typeInfos[hex.EncodeToString(GetPulpHash(name))] = rtype
}

// register "A"
pulp.RegisterConcrete("A", A{})
```

Kodierung ist nur RLP-Kodierung und vorangestellter Hash von `GetPulpHash` der `name`

```go
// EncodeToBytes encodes msg to bytes
txBytes, err := rlp.EncodeToBytes(obj)
if err != nil {
	return nil, err
}

result := append(GetPulpHash("A"), txBytes[:]...), nil
```

Dekodieren funktioniert wie folgt:

```go
// retrieve type of objet based on prefix
rtype := typeInfos[hex.EncodeToString(incomingData[:PulpHashLength])]

// create new object
newMsg := reflect.New(rtype).Interface()

// decode without prefix and inject into newly created object
if err := rlp.DecodeBytes(incomingData[PulpHashLength:], newMsg); err != nil {
	return nil, err
}

// result => newMsg
```

Weitere Informationen:

Das Cosmos SDK verwendet zwei Binärdraht-Kodierungsprotokolle, [Amino](https://github.com/tendermint/go-amino/) und [Protokollpuffer](https://developers.google.com/protocol-buffers), wobei Amino eine Objektkodierungsspezifikation ist. Es handelt sich um eine Untermenge von Proto3 mit einer Erweiterung für die Unterstützung von Schnittstellen. Weitere Informationen zu den [Spezifikationen von Proto3](https://developers.google.com/protocol-buffers/docs/proto3), mit denen Amino weitgehend kompatibel ist (aber nicht mit Proto2), finden Sie in den Spezifikationen für Proto3.

Mehr hier: [https://docs.cosmos.network/master/core/encoding.html](https://docs.cosmos.network/master/core/encoding.html)
