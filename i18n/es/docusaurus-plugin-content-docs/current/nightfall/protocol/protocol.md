---
id: protocol
title: Protocolo Nightfall
sidebar_label: Nightfall Protocol
description: "El proceso Nightfall"
keywords:
  - docs
  - polygon
  - nightfall
  - protocol
  - chain
  - block
  - structure
  - layer
image: https://matic.network/banners/matic-network-16x9.png
---

Asumimos que al menos 1 proponente se ha registrado con el sistema y ha publicado una participación mínima.

## Publicación de la transacción {#transaction-posting}
Existen dos mecanismos para publicar transacciones nuevas:

- [En cadena](#on-chain)
- [Fuera de la cadena](#off-chain)

### En cadena {#on-chain}
EL proceso comienza con un transactor creando una transacción al llamar `submitTransaction`en `Shield.sol`. El transactor paga una tarifa al contrato de escudo por la transacción, la cual puede ser cualquiera que decida el transactor. Esto se pagará al proponente que incorpora la transacción en un bloque. Actualmente, el proponente y la instancia de Optimist subyacente probablemente elegirán las tarifas más altas para incorporarlas en un bloque, prácticamente como lo haría un minero. La llamada de transacción hace que un evento de cadena de bloques se publique, conteniendo sus detalles. Si se trata de un depósito, el contrato de escudo toma el pago del token ERC de la capa 1 en cuestión.

### Fuera de la cadena {#off-chain}
Las transacciones de transferencias y retiros tienen la opción de ser enviadas directamente a los proponentes que están escuchando en lugar de ser enviadas en cadena a través del proceso anterior.
Estas transacciones fuera de la cadena ahorrarán a los transactores el costo de envío en cadena de un depósito (aproximadamente 45k de gas), pero requieren un mayor grado de confianza entre los transactores y los proponentes a los cuales elijan conectarse. Es más fácil para los proponentes que actúan mal censurar las transacciones recibidas fuera de la cadena que las recibidas en cadena, ya que estas transacciones no se transmiten a todos los proponentes que están escuchando. En este caso, los transactores solo deben considerar una transacción como confiable cuando ha transcurrido el período de enfriamiento (1 semana).

## Aceptación de la transacción {#transaction-acceptance}
Cuando los proponentes reciben cualquier transacción, realizan una serie de revisiones para validar que la transacción está bien formada y que la prueba verifica con el hash de entrada público.
Si todas las revisiones pasan, la transacción se agrega al mempool del proponente para ser considerado en un bloque.

## Montaje y envío de bloques {#block-assembly-and-submission}
Los proponentes esperan hasta que el contrato de escudo los asigna como el proponente actual.
El proponente actual recibe, desde su propia instancia interna de Optimist, un bloque nuevo que contiene transacciones desde su mempool. Para cada transacción, calculará el nuevo compromiso del árbol de Merkle en el que se convertiría si la transacción fuera agregada al contrato del escudo.

El bloque contiene, por lo tanto, los hashes de las transacciones incluidas en un bloque y la raíz de compromiso del árbol de Merkle como existiría después de procesar todas las transacciones en el bloque (raíz de compromiso). Después, el proponente envía este bloque al estado del contrato inteligente.

Cuando un bloque es propuesto, la información siguiente se registra en cadena:

- Estructura de datos del bloque
```
  struct Block {
    uint48 leafCount; // note this is defined to be the number of leaves BEFORE the commitments in this block are added
    address proposer;
    bytes32 root; // the 'output' commitment root after adding all commitments
    uint256 blockNumberL2;
    bytes32 previousBlockHash;
    bytes32 transactionHashesRoot;
  }
```
- Transacciones en el bloque
```
    struct Transaction {
        uint112 value;
        uint112 fee;
        TransactionTypes transactionType;
        TokenType tokenType;
        uint64[2] historicRootBlockNumberL2; // number of L2 block containing historic root
        uint64[2] historicRootBlockNumberL2Fee; //number of L2 block containing historic root fee
        bytes32 tokenId;
        bytes32 ercAddress;
        bytes32 recipientAddress;
        bytes32[2] commitments;
        bytes32[2] nullifiers;
        bytes32[1] commitmentFee;
        bytes32[2] nullifiersFee;
        bytes32[2] compressedSecrets;
        uint256[4] proof;
    }
```

## Desafíos {#challenges}
Se podrá desafiar los bloques en espera durante una semana, tiempo durante el cual su corrección puede ser desafiada al llamar a una de las funciones para desafiar. Los desafíos que se pueden hacer son:

- **INVALID_PROOF** - la prueba dada en una transacción no la verifica como verdadera;
- **INVALID_PUBLIC_INPUT_HASH** - el hash de entrada público de una transacción no es el hash correcto de las entradas públicas;
- **HISTORIC_ROOT_EXISTS** - la raíz, del árbol de Merkle del compromiso utilizado para crear la prueba de la transacción nunca ha existido;
- **DUPLICATE_NULLIFIER** - un anulador, dado como parte de una transacción, está presente en la lista de anuladores usados;
- **HISTORIC_ROOT_INVALID** - la raíz del compromiso actualizada que resulta de procesar las transacciones en el bloque no es correcta;
- **DUPLICATE_TRANSACTION** - una transacción idéntica incluida en este bloque ya ha sido incluida en un bloque anterior;
- **TRANSACTION_TYPE_INVALID** - la transacción no está bien formada basándose en el tipo de transacción (por ejemplo, el depósito, la transferencia, el retiro).

Si el desafío tiene éxito, es decir, el cálculo en cadena muestra que es un desafío válido, entonces se toman las siguientes acciones:

- El hash del bloque en cuestión y todos los bloques posteriores se eliminan de la fila de espera.
- La participación del bloque, presentada por el proponente se paga al desafiante.
- Los transactores con una transacción en el bloque son reembolsados con la tarifa que habrían pagado al proponente y cualquier fondo en garantía mantenido por el contrato del escudo en el caso de una transacción de depósito.

