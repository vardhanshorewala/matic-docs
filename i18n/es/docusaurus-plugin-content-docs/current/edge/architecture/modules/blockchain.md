---
id: blockchain
title: Cadena de bloques
description: Explicación para la cadena de bloques y declarar módulos de Polygon Edge.
keywords:
  - docs
  - polygon
  - edge
  - architecture
  - module
  - blockchain
  - state
---

## Resumen {#overview}

Uno de los principales módulos del Polygon Edge son **cadena de bloques** y **Declaración**. <br />

**Cadena de bloques** es la potencia que se ocupa con las reorganizaciones de bloques. Esto significa que se ocupa de toda la lógica que ocurre cuando un nuevo bloque es incluido en una cadena de bloques

**Declaración** representa el*objetivo de la transición de la declaración*. Se trata de cómo cambia la declaración cuando se incluye un nuevo bloque. <br /> Entre otras cosas, **la declaración** se encarga de:
* Ejecutar transacciones
* Ejecutar la EVM
* Cambiar los intentos de Merkle
* Mucho más, que está cubierto en la correspondiente **sección de declaración** 🙂

La conclusión clave es que estas 2 partes están muy conectadas y trabajan en estrecha colaboración para que el cliente funcione. <br /> Por ejemplo, cuando la **capa de cadena de bloques** recibe un nuevo bloque (y no ocurre una reorganización), llama a la **declaración** para realizar una transición de declaración.

**cadena de bloques**también tiene que lidiar con algunas partes relacionadas con el consenso (ejemplo*¿Es correcta esta ethHash?*, *¿es correcta esta PoW?*). <br /> En una oración, **es el núcleo principal de la lógica a través de la cual se incluyen todos los bloques**.

## *Write Blocks*

Una de las partes más importantes relacionadas con **la capa de cadena de bloques** es el *método Write Blocks*:

````go title="blockchain/blockchain.go"
// WriteBlocks writes a batch of blocks
func (b *Blockchain) WriteBlocks(blocks []*types.Block) error {
	if len(blocks) == 0 {
		return fmt.Errorf("no headers found to insert")
	}

	parent, ok := b.readHeader(blocks[0].ParentHash())
	if !ok {
		return fmt.Errorf("parent of %s (%d) not found: %s", blocks[0].Hash().String(), blocks[0].Number(), blocks[0].ParentHash())
	}

	// validate chain
	for i := 0; i < len(blocks); i++ {
		block := blocks[i]

		if block.Number()-1 != parent.Number {
			return fmt.Errorf("number sequence not correct at %d, %d and %d", i, block.Number(), parent.Number)
		}
		if block.ParentHash() != parent.Hash {
			return fmt.Errorf("parent hash not correct")
		}
		if err := b.consensus.VerifyHeader(parent, block.Header, false, true); err != nil {
			return fmt.Errorf("failed to verify the header: %v", err)
		}

		// verify body data
		if hash := buildroot.CalculateUncleRoot(block.Uncles); hash != block.Header.Sha3Uncles {
			return fmt.Errorf("uncle root hash mismatch: have %s, want %s", hash, block.Header.Sha3Uncles)
		}
		
		if hash := buildroot.CalculateTransactionsRoot(block.Transactions); hash != block.Header.TxRoot {
			return fmt.Errorf("transaction root hash mismatch: have %s, want %s", hash, block.Header.TxRoot)
		}
		parent = block.Header
	}

	// Write chain
	for indx, block := range blocks {
		header := block.Header

		body := block.Body()
		if err := b.db.WriteBody(header.Hash, block.Body()); err != nil {
			return err
		}
		b.bodiesCache.Add(header.Hash, body)

		// Verify uncles. It requires to have the bodies on memory
		if err := b.VerifyUncles(block); err != nil {
			return err
		}
		// Process and validate the block
		if err := b.processBlock(blocks[indx]); err != nil {
			return err
		}

		// Write the header to the chain
		evnt := &Event{}
		if err := b.writeHeaderImpl(evnt, header); err != nil {
			return err
		}
		b.dispatchEvent(evnt)

		// Update the average gas price
		b.UpdateGasPriceAvg(new(big.Int).SetUint64(header.GasUsed))
	}

	return nil
}
````
El *método Write Blocks* es el punto de entrada para escribir bloques en la cadena de bloques. Como un parámetro, toma en una gama de bloques.<br /> En primer lugar, los bloques son validados. Después de eso, están escritos en la cadena.

la actual *transición de la declaración* se realiza llamando al método*processBlock* entro de *Write Blocks*.

Vale la pena mencionar que, dado que es el punto de entrada para escribir bloques en la cadena de bloques, otros módulos (como el **Sealer**) utiliza este método.

## Suscripciones Cadena de bloques {#blockchain-subscriptions}

Necesita haber una forma de monitorear los cambios relacionados con la cadena de bloques. <br />
 Aquí es donde **las subscripciones** entran.

Las suscripciones son una forma de aprovechar los flujos de eventos de la cadena de bloques y recibir datos significativos al instante.

````go title="blockchain/subscription.go"
type Subscription interface {
    // Returns a Blockchain Event channel
	GetEventCh() chan *Event
	
	// Returns the latest event (blocking)
	GetEvent() *Event
	
	// Closes the subscription
	Close()
}
````

Los **eventos de la cadena de bloques** contienen información sobre cualquier cambio realizado en la cadena actual. Esto incluye las reorganizaciones, así como nuevos bloques:

````go title="blockchain/subscription.go"
type Event struct {
	// Old chain removed if there was a reorg
	OldChain []*types.Header

	// New part of the chain (or a fork)
	NewChain []*types.Header

	// Difficulty is the new difficulty created with this event
	Difficulty *big.Int

	// Type is the type of event
	Type EventType

	// Source is the source that generated the blocks for the event
	// right now it can be either the Sealer or the Syncer. TODO
	Source string
}
````

:::tip Actualizar

¿Recuerdas cuando mencionamos el ***comando del monitor*** en los comandos dentro de los [comandos CLI](/docs/edge/get-started/cli-commands)?

Los eventos de la cadena de bloques son los eventos originales que ocurren dentro de Polygon Edge y luego se asignan a un formato de mensaje de Protocol Buffers para facilitar la transferencia.
:::