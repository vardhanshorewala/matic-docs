---
id: definitions
title: Definicios generales
description: Definiciones generales para términos que se utilizan en ChainBridge
keywords:
  - docs
  - polygon
  - edge
  - Bridge
---


## Repetidor {#relayer}
ChainBridge es un repetidor tipo puente. La función de un repetidor es votar para le ejecución de una solicitud (cuántos token para quemar o liberar, por ejemplo).
 `Deposit`Hace un seguimiento de eventos desde cada cadena y vota para una propuesta en el contrato puente de la cadena de destino cuando recibe un evento  desde una cadena. Un repetidor llama a un método en el contrato puente para ejecutar la propuesta, luego de que se haya enviado el número de votos solicitado. El puente delega la ejecución al contrato de manejador.


## Tipos de contratos {#types-of-contracts}
En ChainBridge, hay tres tipos de contratos en cada cadena: puente/manejador/objetivo

| **Tipo** | **Descripción** |
|----------|-------------------------------------------------------------------------------------------------------------------------------|
| Contrato puente | Un contrato puente que maneja solicitudes, votos, ejecutiones se necesita desplegar en cada cadena. Los usuarios llamarán Una vez que el contrato manejador llamó al contrato objetivo de forma satisfactoria, el contrato puente emite evento de `Deposit` para notificar a los repetidores. |
| Contrato de manejador | Este contrato interactúa con el contrato objetivo para ejecutar un depósito o propuesta. Valida la solicitud del usuario, llama al contrato objetivo y ayuda con algunos ajustes del contrato ojetivo. Hay ciertos contratos de manejador para llamar a cada contrato objetivo que tiene una interfaz diferente. Las llamadas indirectas del contrato de manejador hacen que el puente habilita la transferencia de cualquier clase de activos o datos. Actualmente, hay tres tipos de contratos de manejador que implementa ChainBridge: ERD-20, ERC-721 y manejador genérico. |
| Contrato objetivo | Un contrato que maneja los activos para intercambiar o los mensajes que se transfieren entre cadenas. La interacción con este contrato se realizará desde cada lateral del punete. |

<div style={{textAlign: 'center'}}>

![Arquitectura ChainBridge](/img/edge/chainbridge/architecture.svg)
 *Arquitectura ChaindBridge*

</div>

<div style={{textAlign: 'center'}}>

![Flujo de trabajo de transferencia del token ERC-20](/img/edge/chainbridge/erc20-workflow.svg)
 *Ejemplo: flujo de trabajo de una transferencia de token *ERC-20

</div>

## Tipos de cuentas {#types-of-accounts}

Asegúrese de que las cuentas tengan suficientes tokens nativos para crear transacciones antes de comenzar. En Polygon Edge, puedes asignar saldos preminados a cuentas cuando se genera el bloque genesis.

| **Tipo** | **Descripción** |
|----------|-------------------------------------------------------------------------------------------------------------------------------|
| Administrador | A esta cuente se le dará el rol de administrador por defecto. |
| Usuario | La cuenta remitente/receptora que envía o recibe activos. La cuenta remitente paga las tarifas de gas al aprobar las transferencias de token y al llamar depósitos en el contrato puente para comenzar a transferir. |

:::info El rol de administrador

Determinadas acciones solo se pueden realizar a través de la cuenta con rol de administrador.
 Por defecto, el administrador del contrato puente tiene el rol de aministrador. A continuación, encontrará como concederle el rol de administrador a otra cuenta o cómo quitárselo.

### Agregar rol de aministrador {#add-admin-role}

Añade un administrador

```bash
# Grant admin role
$ cb-sol-cli admin add-admin \
  --url [JSON_RPC_URL] \
  --privateKey [PRIVATE_KEY] \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --admin "[NEW_ACCOUNT_ADDRESS]"
```
### Revocar el rol de administrador {#revoke-admin-role}

Eliminar un administrador

```bash
# Revoke admin role
$ cb-sol-cli admin remove-admin \
  --url [JSON_RPC_URL] \
  --privateKey [PRIVATE_KEY] \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --admin "[NEW_ACCOUNT_ADDRESS]"
```

## Las operaciones que permite la cuenta `admin` son las que se muestran a continuación. {#account-are-as-below}

### Configurar recurso {#set-resource}

Registrar una identificación de recurso con una dirección de contrato para un manejador.

```bash
# Register new resource
$ cb-sol-cli bridge register-resource \
  --url [JSON_RPC_URL] \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --resourceId "[RESOURCE_ID]" \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --handler "[HANDLER_CONTRACT_ADDRESS]" \
  --targetContract "[TARGET_CONTRACT_ADDRESS]"
```

### Hacer que el contrato se pueda quemar/acuñar. {#make-contract-burnable-mintable}

Configurar un contrato token para que se pueda acuñar o quemar en un manejador.

```bash
# Let contract burnable/mintable
$ cb-sol-cli bridge set-burn \
  --url [JSON_RPC_URL] \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --handler "[HANDLER_CONTRACT_ADDRESS]" \
  --tokenContract "[TARGET_CONTRACT_ADDRESS]"
```

### Cancelar la propuesta {#cancel-proposal}

Cancelar la propuesta para la ejecución

```bash
# Cancel ongoing proposal
$ cb-sol-cli bridge cancel-proposal \
  --url [JSON_RPC_URL] \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --resourceId "[RESOURCE_ID]" \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --chainId "[CHAIN_ID_OF_SOURCE_CHAIN]" \
  --depositNonce "[NONCE]"
```

### Pausar/quitar pausa {#pause-unpause}

Pausar depósitos, la creación de propuestas, el vito y ejecuciones de  depósitos de forma temporaria.

```bash
# Pause
$ cb-sol-cli admin pause \
  --url [JSON_RPC_URL] \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]"

# Unpause
$ cb-sol-cli admin unpause \
  --url [JSON_RPC_URL] \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]"
```

### Cambiar la comisión {#change-fee}

Cambiar la comisión que se pagará al contrato puente

```bash
# Change fee for execution
$ cb-sol-cli admin set-fee \
  --url [JSON_RPC_URL] \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --fee [FEE_IN_WEI]
```

### Agregar/quitar un repetidor {#add-remove-a-relayer}

Agregar una cuenta como un nuevo repetidor o quitar una cuenta desde repetidores

```bash
# Add relayer
$ cb-sol-cli admin add-relayer \
  --url [JSON_RPC_URL] \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --relayer "[NEW_RELAYER_ADDRESS]"

# Remove relayer
$ cb-sol-cli admin remove-relayer \
  --url [JSON_RPC_URL] \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --relayer "[RELAYER_ADDRESS]"
```

### Cambiar el umbral del repetidor {#change-relayer-threshold}

Cambiar el número de votos que se necesitan para la ejecución de una propuesta

```bash
# Remove relayer
$ cb-sol-cli admin set-threshold \
  --url [JSON_RPC_URL] \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --threshold [THRESHOLD]
```
:::

## Identificación de la cadena {#chain-id}

El ChainBridge  `chainId`es un valor arbitrario que se usa en el puente para diferenciar entre las redes de cadenas de bloques, y tiene que estar en el rango de uint8. Para no confundirse con el ID de la cadena de la red, no son la misma cosa. Es necesario que este valor sea único, pero no tiene que ser el mismo de la ID de la red.

En este ejemplo, configuramos

##  {#resource-id}





##  {#json-rpc-url-for-polygon-pos}



##  {#ways-of-processing-the-transfer-of-tokens}


###  {#lock-release-mode}


###  {#burn-mint-mode}







