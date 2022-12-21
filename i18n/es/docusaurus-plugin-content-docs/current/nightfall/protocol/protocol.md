---
id: protocol
title: Protocolo Nightfall
sidebar_label: Nightfall Protocol
description: "El proceso Nightfall."
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

Suponemos que al menos 1 proponente se ha registrado con el sistema, y se ha publicado un stake mínimo.

## Publicación de transacción {#transaction-posting}
Existen dos mecanismos para publicar nuevas transacciones:

- [En la cadena](#on-chain)
- [Fuera de la cadena](#off-chain)

### En la cadena {#on-chain}
El proceso comienza con un Transactor que crea una transacción llamando a `submitTransaction` en`Shield.sol`. El transactor paga una comisión al contrato de Escudo para la transacción, la cual puede ser cualquier cosa que el transactor decida. Esto se pagará al proponente que incorpora la transacción en un bloque. Actualmente, el proponente y la instancia de Optimist subyacente probablemente elegirá las tarifas más altas para incorporar en un bloque, casi como haría un minero.
La llamada para una transacción causa un evento de cadena de bloques para ser publicado, con sus detalles. Si se trata de depositar el contrato de Escudo se paga el token de la capa 1 ERC en cuestión.

### Fuera de la cadena {#off-chain}
Las transacciones de transferir y retirar tienen la opción de ser enviadas directamente a los proponentes de escucha en lugar de ser enviadas en cadena mediante el proceso anterior.
Estas transacciones fuera de la cadena ahorrarán a los transactores el costo de envío en cadena de un depósito (~ 45k gas), pero ellos requieren un mayor grado de confianza entre los transactores y los proponentes que eligieron conectar. Es más fácil para los proponentes de mala actuación censurar las transacciones que se reciben fuera de cadena que las que se reciben en cadena, ya que estas transacciones no son transmitidas a todos los proponentes de escucha. En este caso, los transactores solo deberían considerar que una transacción es confiable cuando haya pasado el periodo de reflexión (1 semana).

## Aceptación de transacción {#transaction-acceptance}
Cuando los proponentes reciben cualquier transacción, realizan una gama de verificaciones para validar que la transacción está bien formada y que la prueba verifica contra el hash de entrada público.
Si todas las verificaciones pasan, la transacción se agrega al mempool de Proponente para ser considerada en un bloque.

## Montaje de bloque y envío {#block-assembly-and-submission}
Los proponentes esperar hasta que el contrato de Escudo los asigne como el proponente actual.
El proponente actual recibe, desde su propia instancia interna de Optimist, un nuevo bloque que contiene las transacciones de su mempool. Para cada transacción, calculará el nuevo compromiso de Árbol Merkle que entraría en ser si esta transacción se agregara al contrato de Escudo.

El bloque contiene, por lo tanto, los hashes incluidos de las transacciones en bloque y el compromiso de raíz de Merkle Tree como este existiría después de procesar todas las transacciones en bloque (raíz de compromiso). Luego, el proponente envía este bloque a la declaración del contrato inteligente.

Cuando un bloque es propuesto, se registra la siguiente información en cadena:

- Estructura de datos de bloque
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
- Transacciones en bloque
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
Los bloques serán desafiados en la cola durante una semana, durante la cual su corrección puede ser desafiada llamando a una de las funciones desafiadoras. Los desafíos que se pueden plantear son:

- **INVALID_PROOF**: la prueba dada en una transacción no se verifica como verdadera;
- **INVALID_PUBLIC_INPUT_HASH**: el hash de entrada pública de una transacción no es el hash correcto de las entradas públicas;
- **HISTORIC_ROOT_EXISTS**: la raíz del compromiso que el árbol de Merkle usó para crear la prueba de transacción que nunca ha existido;
- **DUPLICATE_NULLIFIER**: un nulificador, dado como parte de una Transacción, está presente en la lista de nulificadores gastados;
- **HISTORIC_ROOT_INVALID**: la raíz de compromiso actualizada que resulta del procesamiento de las transacciones en el bloque no es correcta;
- **DUPLICATE_TRANSACTION**: una transacción idéntica incluida en este bloque ya ha sido incluida en un bloque anterior;
- **TRANSACTION_TYPE_INVALID**: la transacción no está bien formada según el tipo de transacción (por ejemplo, Depósito, Transferencia, Retiro).

Debería el desafío tener éxito, es decir, el cálculo en cadena demuestra que es un desafío válido, entonces se toman las siguientes acciones:

- El hash del bloque en cuestión y todos los bloques subsecuentes se eliminan de la cola.
- El bloque stake presentado por el proponente, se paga al desafiador.
- Los transactores con una transacción en el bloque son reembolsados con la comisión que hubiera pagado al proponente y cualquiera de los fondos en garantía que el contrato de Escudo se guarda en el caso de una transacción de depósito.

