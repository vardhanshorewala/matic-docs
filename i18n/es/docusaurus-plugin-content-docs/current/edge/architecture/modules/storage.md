---
id: storage
title: Almacenamiento
description: Explicación para el módulo de almacenamiento de JSON RPC de Polygon Edge.
keywords:
  - docs
  - polygon
  - edge
  - architecture
  - module
  - storage
  - LevelDB
---

## Resumen {#overview}

El Polygon Edge actualmente utiliza **LevelDB** para almacenar datos, así como una **in-memory** almacenadora de datos.

A lo largo de Polygon Edge, cuando los módulos necesitan interactuar con el almacenamiento subyacente, de datos, no necesitan saber de cuál motor o servicio DB están hablando.

La capa DB se abstrae entre un módulo llamado **Storage**, el cual exporta interfaces que consultan los módulos.

Cada capa de base de datos, solo por ahora **LevelDB**, implementa estos métodos por separado, asegurándose de que encajen con su implementación.

````go title="blockchain/storage/storage.go"
// Storage is a generic blockchain storage
type Storage interface {
	ReadCanonicalHash(n uint64) (types.Hash, bool)
	WriteCanonicalHash(n uint64, hash types.Hash) error

	ReadHeadHash() (types.Hash, bool)
	ReadHeadNumber() (uint64, bool)
	WriteHeadHash(h types.Hash) error
	WriteHeadNumber(uint64) error

	WriteForks(forks []types.Hash) error
	ReadForks() ([]types.Hash, error)

	WriteDiff(hash types.Hash, diff *big.Int) error
	ReadDiff(hash types.Hash) (*big.Int, bool)

	WriteHeader(h *types.Header) error
	ReadHeader(hash types.Hash) (*types.Header, error)

	WriteCanonicalHeader(h *types.Header, diff *big.Int) error

	WriteBody(hash types.Hash, body *types.Body) error
	ReadBody(hash types.Hash) (*types.Body, error)

	WriteSnapshot(hash types.Hash, blob []byte) error
	ReadSnapshot(hash types.Hash) ([]byte, bool)

	WriteReceipts(hash types.Hash, receipts []*types.Receipt) error
	ReadReceipts(hash types.Hash) ([]*types.Receipt, error)

	WriteTxLookup(hash types.Hash, blockHash types.Hash) error
	ReadTxLookup(hash types.Hash) (types.Hash, bool)

	Close() error
}
````

## LevelDB {#leveldb}

### Prefijos {#prefixes}

Para realizar consultas del almacenamiento de LevelDB que sea determinista y para evitar conflictos de almacenamiento de claves, Polygon Edge aprovecha prefijos y sub-prefijos cuando se almacenan datos

````go title="blockchain/storage/keyvalue.go"
// Prefixes for the key-value store
var (
	// DIFFICULTY is the difficulty prefix
	DIFFICULTY = []byte("d")

	// HEADER is the header prefix
	HEADER = []byte("h")

	// HEAD is the chain head prefix
	HEAD = []byte("o")

	// FORK is the entry to store forks
	FORK = []byte("f")

	// CANONICAL is the prefix for the canonical chain numbers
	CANONICAL = []byte("c")

	// BODY is the prefix for bodies
	BODY = []byte("b")

	// RECEIPTS is the prefix for receipts
	RECEIPTS = []byte("r")

	// SNAPSHOTS is the prefix for snapshots
	SNAPSHOTS = []byte("s")

	// TX_LOOKUP_PREFIX is the prefix for transaction lookups
	TX_LOOKUP_PREFIX = []byte("l")
)

// Sub-prefixes
var (
	HASH   = []byte("hash")
	NUMBER = []byte("number")
	EMPTY  = []byte("empty")
)
````

## Planes Futuros {#future-plans}

Los planes para un futuro cercano incluyen agregar algunas de las soluciones de DB más populares, tales como:
* PostgreSQL
* MySQL


## 📜 Recursos {#resources}
* **[LevelDB](https://github.com/google/leveldb)**