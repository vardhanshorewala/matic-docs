---
id: consensus
title: Consenso
description: Explicación para el módulo consenso de Polygon Edge.
keywords:
  - docs
  - polygon
  - edge
  - architecture
  - module
  - consensus
  - ibft
---

## Resumen {#overview}

El **módulo consenso** proporciona una interfaz para los mecanismos de consenso.

Actualmente, los siguientes motores de consenso están disponibles:
* **IBFT PoA**
* **IBFT PoS**

El Polygon Edge quiere mantener una declaración de modularidad y conectabilidad. <br />
 Esto es por qué la lógica de consenso central ha sido abstractada fuera, por lo que nuevos mecanismos de consenso se pueden construir en la cima, sin comprometer la usabilidad y la facilidad de uso.

## Interfaz de Consenso  {#consensus-interface}

````go title="consensus/consensus.go"
// Consensus is the interface for consensus
type Consensus interface {
	// VerifyHeader verifies the header is correct
	VerifyHeader(parent, header *types.Header) error

	// Start starts the consensus
	Start() error

	// Close closes the connection
	Close() error
}
````

La ***interfaz de consenso*** es el núcleo de la abstracción mencionada. <br />
* El método **VerifyHeader** representa una función auxiliar que la capa de consenso expone a la **capa de la cadena de bloques**
 Está allí para manejar la verificación de los encabezados
* El método **Start** simplemente inicia el proceso de consenso, y todo lo relacionado con él. Esto incluye la sincronización,
 sellando todo lo que necesita hacerse
* El método **Close** cierra la conexión de consenso

## Configuración de Consenso {#consensus-configuration}

````go title="consensus/consensus.go"
// Config is the configuration for the consensus
type Config struct {
	// Logger to be used by the backend
	Logger *log.Logger

	// Params are the params of the chain and the consensus
	Params *chain.Params

	// Specific configuration parameters for the backend
	Config map[string]interface{}

	// Path for the consensus protocol to store information
	Path string
}
````

Puede haber momentos en los que quizás quieras pasar en una ubicación personalizada para el protocolo de consenso para el almacenamiento de datos, o tal vez para un mapa de valor clave personalizado que quieres que el mecanismo de consenso use. Esto se puede lograr a través de ***la estructura de configuración***,
 la cual se lee cuando una nueva instancia de consenso es creada.

## IBFT {#ibft}

### ExtraData {#extradata}

El objeto de encabezado de la cadena de bloques, entre otros campos, tiene un campo llamado **ExtraData**.

IBFT utiliza este campo extra para almacenar información operativa sobre el bloque, respondiendo a preguntas como:
* "¿Quién firmó este bloque?"
* "¿Quiénes son los validadores para este bloque?"

Estos campos adicionales para IBFT se definen de la siguiente manera:
````go title="consensus/ibft/extra.go"
type IstanbulExtra struct {
	Validators    []types.Address
	Seal          []byte
	CommittedSeal [][]byte
}
````

### Firmando Datos {#signing-data}

Para que el nodo firme información en IBFT, aprovecha el método *signHash*:
````go title="consensus/ibft/sign.go"
func signHash(h *types.Header) ([]byte, error) {
	//hash := istambulHeaderHash(h)
	//return hash.Bytes(), nil

	h = h.Copy() // make a copy since we update the extra field

	arena := fastrlp.DefaultArenaPool.Get()
	defer fastrlp.DefaultArenaPool.Put(arena)

	// when hashign the block for signing we have to remove from
	// the extra field the seal and commitedseal items
	extra, err := getIbftExtra(h)
	if err != nil {
		return nil, err
	}
	putIbftExtraValidators(h, extra.Validators)

	vv := arena.NewArray()
	vv.Set(arena.NewBytes(h.ParentHash.Bytes()))
	vv.Set(arena.NewBytes(h.Sha3Uncles.Bytes()))
	vv.Set(arena.NewBytes(h.Miner.Bytes()))
	vv.Set(arena.NewBytes(h.StateRoot.Bytes()))
	vv.Set(arena.NewBytes(h.TxRoot.Bytes()))
	vv.Set(arena.NewBytes(h.ReceiptsRoot.Bytes()))
	vv.Set(arena.NewBytes(h.LogsBloom[:]))
	vv.Set(arena.NewUint(h.Difficulty))
	vv.Set(arena.NewUint(h.Number))
	vv.Set(arena.NewUint(h.GasLimit))
	vv.Set(arena.NewUint(h.GasUsed))
	vv.Set(arena.NewUint(h.Timestamp))
	vv.Set(arena.NewCopyBytes(h.ExtraData))

	buf := keccak.Keccak256Rlp(nil, vv)
	return buf, nil
}
````
Otro método notable es el método *VerifyCommittedFields* el que verifica que los sellos comprometidos son de validadores vigentes:
````go title="consensus/ibft/sign.go
func verifyCommitedFields(snap *Snapshot, header *types.Header) error {
	extra, err := getIbftExtra(header)
	if err != nil {
		return err
	}
	if len(extra.CommittedSeal) == 0 {
		return fmt.Errorf("empty committed seals")
	}

	// get the message that needs to be signed
	signMsg, err := signHash(header)
	if err != nil {
		return err
	}
	signMsg = commitMsg(signMsg)

	visited := map[types.Address]struct{}{}
	for _, seal := range extra.CommittedSeal {
		addr, err := ecrecoverImpl(seal, signMsg)
		if err != nil {
			return err
		}

		if _, ok := visited[addr]; ok {
			return fmt.Errorf("repeated seal")
		} else {
			if !snap.Set.Includes(addr) {
				return fmt.Errorf("signed by non validator")
			}
			visited[addr] = struct{}{}
		}
	}

	validSeals := len(visited)
	if validSeals <= 2*snap.Set.MinFaultyNodes() {
		return fmt.Errorf("not enough seals to seal block")
	}
	return nil
}
````

### Instantáneas {#snapshots}

Las instantáneas, como su nombre lo indica, están allí para proporcionar una *instantánea*, o la *declaración*de un sistema a cualquier altura de bloque (número).

Las instantáneas contienen un conjunto de nodos que son validadores, así como la información de votación (los validadores pueden votar por otros validadores). Los validadores incluyen información de votación en la **encabezado minero** archivado y cambie el valor de **mientras tanto**:
* Nuncio es **todos 1** si el nodo quiere remover a un validador
* Nuncio es **todos 0** si el nodo quiere añadir un validador

Las instantáneas son calculadas usando el método ***processHeaders***:

````go title="consensus/ibft/snapshot.go"
func (i *Ibft) processHeaders(headers []*types.Header) error {
	if len(headers) == 0 {
		return nil
	}

	parentSnap, err := i.getSnapshot(headers[0].Number - 1)
	if err != nil {
		return err
	}
	snap := parentSnap.Copy()

	saveSnap := func(h *types.Header) error {
		if snap.Equal(parentSnap) {
			return nil
		}

		snap.Number = h.Number
		snap.Hash = h.Hash.String()

		i.store.add(snap)

		parentSnap = snap
		snap = parentSnap.Copy()
		return nil
	}

	for _, h := range headers {
		number := h.Number

		validator, err := ecrecoverFromHeader(h)
		if err != nil {
			return err
		}
		if !snap.Set.Includes(validator) {
			return fmt.Errorf("unauthroized validator")
		}

		if number%i.epochSize == 0 {
			// during a checkpoint block, we reset the voles
			// and there cannot be any proposals
			snap.Votes = nil
			if err := saveSnap(h); err != nil {
				return err
			}

			// remove in-memory snaphots from two epochs before this one
			epoch := int(number/i.epochSize) - 2
			if epoch > 0 {
				purgeBlock := uint64(epoch) * i.epochSize
				i.store.deleteLower(purgeBlock)
			}
			continue
		}

		// if we have a miner address, this might be a vote
		if h.Miner == types.ZeroAddress {
			continue
		}

		// the nonce selects the action
		var authorize bool
		if h.Nonce == nonceAuthVote {
			authorize = true
		} else if h.Nonce == nonceDropVote {
			authorize = false
		} else {
			return fmt.Errorf("incorrect vote nonce")
		}

		// validate the vote
		if authorize {
			// we can only authorize if they are not on the validators list
			if snap.Set.Includes(h.Miner) {
				continue
			}
		} else {
			// we can only remove if they are part of the validators list
			if !snap.Set.Includes(h.Miner) {
				continue
			}
		}

		count := snap.Count(func(v *Vote) bool {
			return v.Validator == validator && v.Address == h.Miner
		})
		if count > 1 {
			// there can only be one vote per validator per address
			return fmt.Errorf("more than one proposal per validator per address found")
		}
		if count == 0 {
			// cast the new vote since there is no one yet
			snap.Votes = append(snap.Votes, &Vote{
				Validator: validator,
				Address:   h.Miner,
				Authorize: authorize,
			})
		}

		// check the tally for the proposed validator
		tally := snap.Count(func(v *Vote) bool {
			return v.Address == h.Miner
		})

		if tally > snap.Set.Len()/2 {
			if authorize {
				// add the proposal to the validator list
				snap.Set.Add(h.Miner)
			} else {
				// remove the proposal from the validators list
				snap.Set.Del(h.Miner)

				// remove any votes casted by the removed validator
				snap.RemoveVotes(func(v *Vote) bool {
					return v.Validator == h.Miner
				})
			}

			// remove all the votes that promoted this validator
			snap.RemoveVotes(func(v *Vote) bool {
				return v.Address == h.Miner
			})
		}

		if err := saveSnap(h); err != nil {
			return nil
		}
	}

	// update the metadata
	i.store.updateLastBlock(headers[len(headers)-1].Number)
	return nil
}
````

Este método generalmente se llama con 1 encabezado, pero el flujo es el mismo incluso con múltiples encabezados. <br />
 Para cada encabezado pasado, el IBFT necesita verificar que el proponente del encabezado sea el validador. Esto se puede hacer fácilmente al agarrar la última instantánea, y verificar si el nodo está en el conjunto de validadores.

A continuación, el nuncio es verificado El voto está incluido, y se cuenta - y si hay suficientes votos nodo es añadido/eliminado desde el conjunto de validadores, siguiendo el cual de las nuevas instantáneas son guardadas.

#### Almacenamiento de Instantáneas {#snapshot-store}

El servicio de instantáneas administra y actualiza una entidad denominada **snapshot Store**, que almacena la lista de todas las instantáneas disponibles.
 Usándolo este servicio es capaz de averiguar rápidamente cuales instantáneas están asociadas con una altura de bloque.
````go title="consensus/ibft/snapshot.go"
type snapshotStore struct {
	lastNumber uint64
	lock       sync.Mutex
	list       snapshotSortedList
}
````

### Inicio de IBFT {#ibft-startup}

Para iniciar el IBFT, el Polygon Edge en primer lugar necesita configurar el transporte IBFT:
````go title="consensus/ibft/ibft.go"
func (i *Ibft) setupTransport() error {
	// use a gossip protocol
	topic, err := i.network.NewTopic(ibftProto, &proto.MessageReq{})
	if err != nil {
		return err
	}

	err = topic.Subscribe(func(obj interface{}) {
		msg := obj.(*proto.MessageReq)

		if !i.isSealing() {
			// if we are not sealing we do not care about the messages
			// but we need to subscribe to propagate the messages
			return
		}

		// decode sender
		if err := validateMsg(msg); err != nil {
			i.logger.Error("failed to validate msg", "err", err)
			return
		}

		if msg.From == i.validatorKeyAddr.String() {
			// we are the sender, skip this message since we already
			// relay our own messages internally.
			return
		}
		i.pushMessage(msg)
	})
	if err != nil {
		return err
	}

	i.transport = &gossipTransport{topic: topic}
	return nil
}
````

Esencialmente, crea un nuevo tema con IBFT proto, con un nuevo mensaje de beneficio de proto.<br />
 Los mensajes están destinados a ser utilizados por los validadores. El Polygon Edge entonces se suscribe al tema y maneja los mensajes en consecuencia.

#### Mensaje Requerido {#messagereq}

El mensaje intercambiado por los validadores:
````go title="consensus/ibft/proto/ibft.proto"
message MessageReq {
    // type is the type of the message
    Type type = 1;

    // from is the address of the sender
    string from = 2;

    // seal is the committed seal if message is commit
    string seal = 3;

    // signature is the crypto signature of the message
    string signature = 4;

    // view is the view assigned to the message
    View view = 5;

    // hash of the locked block
    string digest = 6;

    // proposal is the rlp encoded block in preprepare messages
    google.protobuf.Any proposal = 7;

    enum Type {
        Preprepare = 0;
        Prepare = 1;
        Commit = 2;
        RoundChange = 3;
    }
}

message View {
    uint64 round = 1;
    uint64 sequence = 2;
}
````

El **campo de vista** en el **mensaje requerido** representa la posición actual del nodo dentro de la cadena.
 Tiene una *cualidad redonda* y una*cualidad en* secuencia.
* **la redonda** representa al proponente que ronda por la altura
* **secuencia** representa la altura de la cadena de bloques

El *msgQueue* archivado en la implementación del IBFT tiene el propósito de almacenar las solicitudes de mensajes. Ordena los mensajes por La *vista* (primero por secuencia, luego por ronda). La implementación de IBFT también posee diferentes colas para diferentes declaraciones del sistema

### Declaraciones IBFT {#ibft-states}

Después de que el mecanismo de consenso se inicia utilizando el método **Start**se ejecuta en un bucle infinito que simula una máquina de estado:
````go title="consensus/ibft/ibft.go"
func (i *Ibft) start() {
	// consensus always starts in SyncState mode in case it needs
	// to sync with other nodes.
	i.setState(SyncState)

	header := i.blockchain.Header()
	i.logger.Debug("current sequence", "sequence", header.Number+1)

	for {
		select {
		case <-i.closeCh:
			return
		default:
		}

		i.runCycle()
	}
}

func (i *Ibft) runCycle() {
	if i.state.view != nil {
		i.logger.Debug(
		    "cycle",
		    "state",
		    i.getState(),
		    "sequence",
		    i.state.view.Sequence,
		    "round",
		    i.state.view.Round,
	    )
	}

	switch i.getState() {
	case AcceptState:
		i.runAcceptState()

	case ValidateState:
		i.runValidateState()

	case RoundChangeState:
		i.runRoundChangeState()

	case SyncState:
		i.runSyncState()
	}
}
````

#### Declaración de Sincronización {#syncstate}

Todos los nodos inicialmente en la **sincronización de declaración**.

Esto es porque los datos nuevos necesitan ser obtenidos de la cadena de bloques. El cliente necesita saber si es el validador, encontrar la instantánea actual. Esta declaración resuelve cualquier bloque pendiente.

Una vez que finaliza la sincronización y el cliente determina que, de hecho, es un validador, debe transferirse a una **Declaración aceptada**.
 Si el cliente no **es** un validador, continuará sincronizándose y permanecerá en **una declaración sincronizada**

#### Declaración Aceptada {#acceptstate}

La **declaración** aceptada, siempre comprobar la instantánea y el conjunto de validadores. Si el nodo actual no está en el conjunto de validadores,
 vuelven al estado **de declaración** aceptada.

En cambio, si el nodo **es** un validador, calcula el proponente. Si resulta que el nodo actual es el proponente que construye un bloque y envía la preparación previamente y luego prepara los mensajes.

* Previamente prepara mensajes - los mensajes enviados por los proponentes a los validadores, para permitirles saber acerca de la propuesta
* Prepara los mensajes - mensajes en los que los validadores están de acuerdo en una propuesta. Todos los nodos reciben todos los mensajes de preparación
* Los mensajes de compromiso mensajes que contienen información de compromisos para la propuesta

Si el nodo actual **no es** de un validador, utiliza el método *getNextMessage* para leer un mensaje de la cola mostrada anteriormente. <br />
 Espera los mensajes preparados previamente. Una vez que se confirma que todo es correcto, el nodo se mueve a la **declaración** validada.

#### Declaración de Validación {#validatestate}

La **declaración** de validación es bastante simple: todo lo que hacen los nodos en esta declaración es leer mensajes y agregarlos a su instantánea local de declaración.
