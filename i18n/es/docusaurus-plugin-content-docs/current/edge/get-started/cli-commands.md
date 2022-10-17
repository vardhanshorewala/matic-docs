---
id: cli-commands
title: Comandos CLI
description: "Lista de comandos CLI y banderas de comando para Polygon Edge."
keywords:
  - docs
  - polygon
  - edge
  - cli
  - commands
  - flags
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';


Esta sección detalla los comandos actuales, banderas de comando en el Polygon Edge, y cómo se utilizan.

:::tip Soporte de salida JSON

La bandera `--json`es compatible con algunos comandos. Esta bandera instruye al comando para imprimir la salida en formato JSON

:::

## Comandos de Inicio {#startup-commands}

| **Comando** | **Descripción** |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| servidor | El comando por defecto que inicia al cliente de la cadena de bloques, mediante el arranque de todos los módulos  |
| génesis juntos | Genera un archivo *genesis.json* que se utiliza para establecer un estado de cadena predefinido antes de iniciar el cliente. La estructura del archivo de génesis se describe abajo |

### banderas del servidor {#server-flags}

<h4><i>sello</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--sello DEBERÍA_SELLAR]
</TabItem>
  <TabItem value="example" label="Example">

    Sellar servidor
</TabItem>
</Tabs>

Establece la bandera que indica que el cliente debería sellar los bloques. Por defecto:`true`.

---

<h4><i>directorio de datos</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--data-dir DIRECTORIO_DE_DATOS]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --directorio de datos ./example-dir
</TabItem>
</Tabs>

Se utiliza para especificar el directorio de datos utilizado para almacenar los datos del cliente de Polygon Edge por defecto:`./test-chain`.

---


<h4><i>jsonrpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--jsonrpc DIRECCIÓN JSONRPC]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --jsonrpc 127.0.0.1:10000
</TabItem>
</Tabs>

Establece la dirección y el puerto para el servicio JSON-RPC   .   
 Si solo se define el puerto    se vinculará a todas las interfaces.
 Si se omite el servicio este se vinculará por defecto`address:port`.
 Dirección por defecto:`0.0.0.0:8545`.

---

<h4><i>límite de rango de bloques de json-rpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--json-rpc-block-range-limit RANGO_DE_BLOQUES]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --json-rpc-block-range-limit 1500
</TabItem>
</Tabs>

Establece el rango máximo de bloques a considerar al ejecutar las solicitudes de json-rpc que incluyen valores de bloque / a bloque (por ejemplo, eth_getLogs). Por defecto:`1000`.

---

<h4><i>json-rpc-batch-request-limit</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--json-rpc-batch-request-limit MAX_LENGTH]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --json-rpc-batch-request-limit 50
</TabItem>
</Tabs>

Establece la longitud máxima a considerar al manejar las solicitudes de lotes de json-rpc. Por defecto:`20`.

---

<h4><i>grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --grpc-address 127.0.0.1:10001
</TabItem>
</Tabs>

Establece la dirección y el puerto para el servicio de gRPC. `address:port`Dirección por defecto:`127.0.0.1:9632`.

---

<h4><i>libp2p</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--libp2p LIBP2P_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --libp2p 127.0.0.1:10002
</TabItem>
</Tabs>

Establece la dirección y el puerto para el servicio de libp2p. `address:port` Dirección por defecto:`127.0.0.1:1478`.

---

<h4><i>prometheus</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--prometheus PROMETHEUS_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --prometheus 127.0.0.1:10004
</TabItem>
</Tabs>

Establece la dirección y el puerto para el servidor de prometheus.       
 Si solo se define el puerto del el servicio se vinculará a todas las interfaces. `0.0.0.0:5001`
 Si se omite el servicio no se iniciará.

---

<h4><i>objetivo de bloques de gas</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--block-gas-target BLOCK_GAS_TARGET]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --block-gas-target 10000000
</TabItem>
</Tabs>

Establece el límite del bloque de gas para la cadena por defecto (no se aplica):`0`.

Una explicación más detallada sobre el objetivo del bloque de gas se puede encontrar en la [sección de Txpool](/docs/edge/architecture/modules/txpool#block-gas-target).

---

<h4><i>max-peers</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--max-peers PEER_COUNT]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --max-peers 40
</TabItem>
</Tabs>

Establece el número máximo de pares del cliente. Por defecto:`40`.

El límite de pares debe especificarse ya sea utilizando`max-peers` o la bandera`max-inbound/outbound-peers`

---

<h4><i>max-inbound-peers</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--max-inbound-peers PEER_COUNT]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --max-inbound-peers 32
</TabItem>
</Tabs>

Establece el número máximo entrante de pares del cliente. Si`max-peers` se establece, el límite máximo de entrada de pares se calcula utilizando las siguientes fórmulas.

`max-inbound-peer = InboundRatio * max-peers` donde`InboundRatio` está `0.8`

---

<h4><i>max-outbound-peers</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--max-outbound-peers PEER_COUNT]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --max-outbound-peers 8
</TabItem>
</Tabs>

Establece el número máximo de pares saliente del cliente. Si `max-peers`se establece, el número máximo de pares de salida se calcula utilizando las siguientes fórmulas.

`max-outbound-peer = OutboundRatio * max-peers` donde`OutboundRatio` está `0.2`

---

<h4><i>max-enqueued</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--max-enqueued ENQUEUED_TRANSACTIONS]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --max-enqueued 210
</TabItem>
</Tabs>

Establece el número máximo de transacciones en cola por cuenta. Por defecto:`128`.

---

<h4><i>nivel de inicio</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--log-level LOG_LEVEL]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --log-level DEBUG
</TabItem>
</Tabs>

Establece el nivel de registro para la salida de la consola. Por defecto:`INFO`.

---

<h4><i>inicia en</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--log-to LOG_FILE]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --log-to node.log
</TabItem>
</Tabs>

Define el nombre de archivo de inicio que mantendrá toda la salida de inicio del comando del servidor. Por defecto todos los inicios de los servidores se producirán a la consola (stdout), pero si la bandera está establecida, no habrá salida a la consola cuando se ejecuta el comando del servidor.

---

<h4><i>cadena</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--chain GENESIS_FILE]
</TabItem>
  <TabItem value="example" label="Example">

    servidor cadena /home/ubuntu/genesis.json
</TabItem>
</Tabs>

Especifica el archivo de génesis utilizado para iniciar la cadena. Por defecto:`./genesis.json`.

---

<h4><i>únete</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--join JOIN_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --únete /ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
</TabItem>
</Tabs>

Especifica la dirección del par que debería unirse

---

<h4><i>nat</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--nat NAT_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --nat 192.0.2.1
</TabItem>
</Tabs>

Establece la dirección externa IP sin el puerto, ya que puede ser visto por los pares.

---

<h4><i>dns</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--dns DNS_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --dns dns4/example.io
</TabItem>
</Tabs>

Establece la dirección DNS del huésped. Esto se puede utilizar para publicitar un DNS externo. Soportes`dns``dns4``dns6`

---

<h4>
  <i>límite de precios</i>
</h4>


<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--price-limit PRICE_LIMIT]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --price-limit 10000
</TabItem>
</Tabs>

Establece el límite mínimo del precio de gas para hacer cumplir su aceptación en el grupo. Por defecto:`1`.

---

<h4>
  <i>espacios máximos</i>
</h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--max-slots MAX_SLOTS]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --max-slots 1024
</TabItem>
</Tabs>

Establece los espacios máximos en el grupo. Por defecto:`4096`.

---

<h4><i>config</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--config CLI_CONFIG_PATH]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --config ./myConfig.json
</TabItem>
</Tabs>

Especifica la ruta hacia la configuración de CLI. Soportes`.json`.

---

<h4><i>config secretos</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--secrets-config SECRETS_CONFIG]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --secrets-config ./secretsManagerConfig.json
</TabItem>
</Tabs>

Establece la ruta hacia el archivo de configuración del administrador de secretos Usado para Hashicorp Vault, AWS SSM y el administrador de secretos GCP. Si se omite, se utiliza el administrador local de secretos FS.

---

<h4><i>dev</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--dev DEV_MODE]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --dev
</TabItem>
</Tabs>

Establece al cliente en el modo desarrollador. Por defecto:`false`.

---

<h4><i>dev-interval</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--dev-interval DEV_INTERVAL]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --dev-interval 20
</TabItem>
</Tabs>

Establece el intervalo de notificación de desarrollador del cliente en segundos. Por defecto:`0`.

---

<h4><i>no-descubras</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--no-discover NO_DISCOVER]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --no-discover
</TabItem>
</Tabs>

Evita que el cliente descubra otros pares. Por defecto:`false`.

---

<h4><i>restaurar</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--restore RESTORE]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --restore backup.dat
</TabItem>
</Tabs>

Restaurar los bloques del archivo especificado

---

<h4><i>block-time</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--block-time BLOCK_TIME]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --block-time 1000
</TabItem>
</Tabs>

Establece el tiempo (u hora) de producción en segundos. Por defecto: `2`

---

<h4><i>access-control-allow-origins</i></h4>
<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    servidor [--access-control-allow-origins ACCESS_CONTROL_ALLOW_ORIGINS]
</TabItem>
  <TabItem value="example" label="Example">

    servidor --access-control-allow-origins "https://edge-docs.polygon.technology"
</TabItem>
</Tabs>

Establece los dominios autorizados para poder compartir las respuestas de las solicitudes JSON-RPC.   
 Añade banderas múltiples    para autorizar dominios múltiples.
 Si se omite, el encabezado Acceso-Control-Permitir-Orígenes se establecerá en `*`y todos los dominios serán autorizados.

---

### banderas de genesis {#genesis-flags}

<h4><i>dir</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--dir DIRECTORY]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --dir ./genesis.json

</TabItem>
</Tabs>

Establece el directorio para los datos de génesis del Polygon Edge por defecto:`./genesis.json`.

---

<h4><i>nombre</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--name NAME]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --name test-chain
</TabItem>
</Tabs>

Establece el nombre para la cadena. Por defecto:`polyton-edge`.

---

<h4><i>pos</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--pos IS_POS]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --pos
</TabItem>
</Tabs>

Establece la bandera que indica que el cliente debería usar la prueba de participación IBFT. Por defecto para la prueba de autoridad si no se proporciona la bandera o`false`.

---

<h4><i>tamaño de epoch</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--epoch-size EPOCH_SIZE]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --epoch-size 50
</TabItem>
</Tabs>

Establece el tamaño de epoch para la cadena. Por defecto`100000`.

---

<h4><i>preminar</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--premine ADDRESS:VALUE]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --preminar 0x3956E90e632AEbBF34DEB49b71c28A83Bc029862:1000000000000000000000
</TabItem>
</Tabs>

Establece las cuentas y los saldos preminados en el formato`address:amount`.
 La cantidad puede ser ya sea en decimal o en hex. Saldo preminado por defecto:`0x3635C9ADC5DEA00000`.

---

<h4><i>Id de cadena</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--chain-id CHAIN_ID]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --chain-id 200
</TabItem>
</Tabs>

Establece la identificación de la cadena. Por defecto:`100`.

---

<h4><i>ibft-validator-type</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--ibft-validator-type IBFT_VALIDATOR_TYPE]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --ibft-validator-type ecdsa
</TabItem>
</Tabs>

Especifica el modo de validación de los encabezados de los bloques Valores posibles:`[ecdsa, bls]`. Por defecto:`bls`.

---

<h4><i>ibft-validators-prefix-path</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--ibft-validators-prefix-path IBFT_VALIDATORS_PREFIX_PATH]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --ibft-validators-prefix-path test-chain-
</TabItem>
</Tabs>

Ruta de prefijo para el directorio de carpeta de validador. Debe estar presente si la bandera`ibft-validator` es omitida.

---

<h4><i>validador-ibft</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--ibft-validator IBFT_VALIDATOR_LIST]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --ibft-validator 0xC12bB5d97A35c6919aC77C709d55F6aa60436900
</TabItem>
</Tabs>

Establece las direcciones aprobadas como validadores de IBFT. Debe estar presente si la bandera`ibft-validators-prefix-path` es omitida.
1. Si la red se ejecuta con ECDSA, el formato es. `--ibft-validator [ADDRESS]`
2. Si la red se ejecuta con BLS, el formato es. `--ibft-validator [ADDRESS]:[BLS_PUBLIC_KEY]`

---

<h4><i>límite de gas del bloque</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--block-gas-limit BLOCK_GAS_LIMIT]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --block-gas-limit 5000000
</TabItem>
</Tabs>

Se refiere a la cantidad máxima de gas utilizada por todas las operaciones en un bloque. Por defecto:`5242880`.

---

<h4><i>consensus</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--consensus CONSENSUS_PROTOCOL]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --consensus ibft
</TabItem>
</Tabs>

Establece protocolo consensus. Por defecto:`pow`.

---

<h4><i>nodo de arranque</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--bootnode BOOTNODE_URL]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --bootnode /ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
</TabItem>
</Tabs>

URL de multiaddr para el bootstrap de descubrimiento de p2p. Esta bandera puede ser usada múltiples veces. En lugar de una dirección IP, la dirección DNS del nodo de inicio puede ser proporcionada.

---

<h4><i>recuento máximo de validadores</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--max-validator-count MAX_VALIDATOR_COUNT]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --max-validator-count 42
</TabItem>
</Tabs>

El número máximo de participantes capaces de unirse al validador establecido en PoS (prueba de participación) consensus. Este número no puede superar el valor de MAX_SAFE_INTEGER (2^53 - 2).

---

<h4><i>recuento-min-de validadores</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    genesis [--min-validator-count MIN_VALIDATOR_COUNT]
</TabItem>
  <TabItem value="example" label="Example">

    genesis --min-validator-count 4
</TabItem>
</Tabs>

El número mínimo de participantes necesarios para unirse al grupo de validadores en PoS (prueba de participación) consensus. Este número no puede superar el valor de recuento de validadores máximos. Por defecto para 1.

---

## Comandos de Operador {#operator-commands}

### Comandos de Pares {#peer-commands}

| **Comando** | **Descripción** |
|------------------------|-------------------------------------------------------------------------------------|
| agregar pares | Añade un nuevo par usando su dirección de libp2p |
| Lista de pares | Enumera todos los pares el cliente está conectado a través de libp2p |
| Estatus de pares | Regresa el estatus de un par específico de la lista de pares, utilizando la dirección de libp2p |

<h3>Pares agregar banderas</h3>

<h4><i>Dirección</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    agregar pares --addr PEER_ADDRESS
</TabItem>
  <TabItem value="example" label="Example">

    agregar pares --addr /ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
</TabItem>
</Tabs>

Dirección de pares libp2p en el formato de multiaddr.

---

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    agregar pares [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    agregar pares --grpc-address 127.0.0.1:10003
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

<h3>banderas de la lista de pares</h3>

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    Lista de pares [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    Lista de pares --grpc-address 127.0.0.1:10003
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

<h3>banderas de estatus de pares</h3>

<h4><i>id-de-pares</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    estatus de pares --peer-id PEER_ID
</TabItem>
  <TabItem value="example" label="Example">

    estatus de pares --peer-id 16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
</TabItem>
</Tabs>

Identificación de nodo Libp2p de un par específico dentro de la red de p2p.

---

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    estatus de pares [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    estatus de pares --grpc-address 127.0.0.1:10003
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

### Comandos IBFT {#ibft-commands}

| **Comando** | **Descripción** |
|------------------------|-------------------------------------------------------------------------------------|
| instantánea de ibft | Regresa la instantánea de IBFT |
| candidatos ibft | Consulta el conjunto actual de candidatos propuestos, así como de candidatos que aún no se han incluido |
| propón ibft | Propón un nuevo candidato para ser agregado/eliminado del conjunto de validadores |
| estatus de ibft | Regresa el estatus general del cliente de IBFT |
| Interruptor de ibft | agregar configuraciones de bifurcación en archivo de genesis.json para cambiar el tipo de IBFT |
| quórum de ibft | Especifica el número de bloque después de lo cual el método óptimo de tamaño de quórum se utilizará para consensus |


<h3>banderas de instantáneas de ibft</h3>

<h4><i>número</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    instantánea de ibft [--number BLOCK_NUMBER]
</TabItem>
  <TabItem value="example" label="Example">

    instantánea de ibft --número 100
</TabItem>
</Tabs>

Altura de bloque (número) para la instantánea.

---

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    instantánea de ibft [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    instantánea de ibft --grpc-address 127.0.0.1:10003
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

<h3>banderas de candidatos de ibft</h3>

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    candidatos ibft [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    candidatos de ibft --grpc-address 127.0.0.1:10003
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

<h3>propón banderas de ibft</h3>

<h4><i>votar</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    propón ibft --votar VOTE
</TabItem>
  <TabItem value="example" label="Example">

    propón ibft --vote auth
</TabItem>
</Tabs>

Propón un cambio en el conjunto de validadores. Valores posibles:`[auth, drop]`.

---

<h4><i>Dirección</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    propón ibft --addr ETH_ADDRESS
</TabItem>
  <TabItem value="example" label="Example">

    propón ibft --addr 0x89205A3A3b2A69De6Dbf7f01ED13B2108B2c43e7
</TabItem>
</Tabs>

Dirección de la cuenta a votar.

---

<h4><i>bls</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    propón ibft --bls BLS_PUBLIC_KEY
</TabItem>
  <TabItem value="example" label="Example">

    propón ibft --bls 0x9952735ca14734955e114a62e4c26a90bce42b4627a393418372968fa36e73a0ef8db68bba11ea967ff883e429b3bfdf
</TabItem>
</Tabs>

Clave pública de BLS de la cuenta a votar, necesaria solo en modo BLS.

---

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    candidatos ibft [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    candidatos de ibft --grpc-address 127.0.0.1:10003
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

<h3>banderas de estatus de ibft</h3>

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    candidatos ibft [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    estatus de ibft --grpc-address 127.0.0.1:10003
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

<h3>banderas de interruptor ibft</h3>

<h4><i>cadena</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    interruptor de ibft [--chain GENESIS_FILE]
</TabItem>
  <TabItem value="example" label="Example">

    interruptor ibft --cadena genesis.json
</TabItem>
</Tabs>

Especifica el archivo de génesis para actualizar. Por defecto:`./genesis.json`.

---

<h4><i>tipo</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    interruptor de ibft [--type TYPE]
</TabItem>
  <TabItem value="example" label="Example">

    interruptor de ibft --tipo PoS
</TabItem>
</Tabs>

Especifica el tipo de IBFT para cambiar. Valores posibles:`[PoA, PoS]`.

---

<h4><i>despliegue</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    interruptor de ibft [--despliegue DEPLOYMENT]
</TabItem>
  <TabItem value="example" label="Example">

    interruptor de ibft --despliegue 100
</TabItem>
</Tabs>

Especifica la altura del contrato de despliegue. Solo disponible con PoS (prueba de participación)

---

<h4><i>desde</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    interruptor de ibft [--from FROM]
</TabItem>
  <TabItem value="example" label="Example">

    interruptor de ibft --from 200
</TabItem>
</Tabs>

---

<h4><i>ibft-validator-type</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    interruptor de ibft [--ibft-validator-type IBFT_VALIDATOR_TYPE]
</TabItem>
  <TabItem value="example" label="Example">

    interruptor de ibft --ibft-validator-type ecdsa
</TabItem>
</Tabs>

Especifica el modo de validación de los encabezados de los bloques Valores posibles:`[ecdsa, bls]`. Por defecto:`bls`.

---

<h4><i>ibft-validators-prefix-path</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    interruptor de ibft [--ibft-validators-prefix-path IBFT_VALIDATORS_PREFIX_PATH]
</TabItem>
  <TabItem value="example" label="Example">

    interruptor de ibft --ibft-validators-prefix-path test-chain-
</TabItem>
</Tabs>

Ruta de prefijo para los directorios de nuevos validadores. Debe estar presente si la bandera está omitida. `ibft-validator`Disponible solo cuando el modo de IBFT es PoA (bandera es omitida). `--pos`

---

<h4><i>validador-ibft</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    interruptor de ibft [--ibft-validator IBFT_VALIDATOR_LIST]
</TabItem>
  <TabItem value="example" label="Example">

    interruptor de ibft --ibft-validator 0xC12bB5d97A35c6919aC77C709d55F6aa60436900
</TabItem>
</Tabs>

Establece las direcciones aprobadas como validadores de IBFT utilizados después de la bifurcación. Debe estar presente si la bandera está omitida. `ibft-validators-prefix-path`Disponible solo en modo de PoA.
1. Si la red se ejecuta con ECDSA, el formato es. `--ibft-validator [ADDRESS]`
2. Si la red se ejecuta con BLS, el formato es. `--ibft-validator [ADDRESS][BLS_PUBLIC_KEY]`

---

<h4><i>recuento máximo de validadores</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    interruptor de ibft [--max-validator-count MAX_VALIDATOR_COUNT]
</TabItem>
  <TabItem value="example" label="Example">

    interruptor de ibft --max-validator-count 42
</TabItem>
</Tabs>

El número máximo de participantes capaces de unirse al validador establecido en PoS (prueba de participación) consensus. Este número no puede superar el valor de MAX_SAFE_INTEGER (2^53 - 2).

---

<h4><i>recuento-min-de validadores</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    interruptor de ibft [--min-validator-count MIN_VALIDATOR_COUNT]
</TabItem>
  <TabItem value="example" label="Example">

    interruptor de ibft --min-validator-count 4
</TabItem>
</Tabs>

El número mínimo de participantes necesarios para unirse al grupo de validadores en PoS (prueba de participación) consensus. Este número no puede superar el valor de recuento de validadores máximos. Por defecto para 1.

Especifica la altura de inicio de la bifurcación.

---

<h3>banderas de quórum de ibft</h3>

<h4><i>desde</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    quorum de ibft [--from your_quorum_switch_block_num]
</TabItem>
  <TabItem value="example" label="Example">

    quórum de ibft --from 350
</TabItem>
</Tabs>

La altura para cambiar el cálculo de quórum a Quórum óptimo, que utiliza la fórmula`(2/3 * N)`,`N` siendo el número de nodos de validación. Nota que esto es para compatibilidad de contrapartes, es decir, solo para cadenas que utilizaron un cálculo de quórum heredado hasta a una altura determinada de bloque.

---

<h4><i>cadena</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    interruptor de ibft [--chain GENESIS_FILE]
</TabItem>
  <TabItem value="example" label="Example">

    interruptor ibft --cadena genesis.json
</TabItem>
</Tabs>

Especifica el archivo de génesis para actualizar. Por defecto:`./genesis.json`.

### Comandos de Grupos de Transacción {#transaction-pool-commands}

| **Comando** | **Descripción** |
|------------------------|--------------------------------------------------------------------------------------|
| estatus de txpool | Regresa el número de transacciones en el grupo |
| suscribirse a txpool | Suscripción para eventos en el grupo de transacción |

<h3>banderas de estatus de txpool</h3>

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    candidatos ibft [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    estatus de txpool --grpc-address 127.0.0.1:10003
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

<h3>banderas de suscripción de txpool</h3>

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    suscribirte a txpool [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    suscribirte a txpool --grpc-address 127.0.0.1:10003
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

---

<h4><i>promovido</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    suscribirse a txpool [--promoted LISTEN_PROMOTED]
</TabItem>
  <TabItem value="example" label="Example">

    suscribirte a txpool --promoted
</TabItem>
</Tabs>

Suscripciones para eventos de tx promovidas en el TxPool.

---

<h4><i>abandonado</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    suscribirte a txpool [--dropped LISTEN_DROPPED]
</TabItem>
  <TabItem value="example" label="Example">

    suscribirte a txpool --dropped
</TabItem>
</Tabs>

Suscripciones para eventos de tx abandonados en el TxPool.

---

<h4><i>degradado</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    suscribirte a txpool [--demoted LISTEN_DEMOTED]
</TabItem>
  <TabItem value="example" label="Example">

    suscribirte a txpool --demoted
</TabItem>
</Tabs>

Suscripciones para eventos de tx degradados en el TxPool.

---

<h4><i>añadido</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    suscribirte a txpool [--added LISTEN_ADDED]
</TabItem>
  <TabItem value="example" label="Example">

    suscribirte a txpool --añadido
</TabItem>
</Tabs>

Suscripciones para eventos de tx añadidos al TxPool.

---

<h4><i>en cola</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    suscribirte a txpool [--enqueued LISTEN_ENQUEUED]
</TabItem>
  <TabItem value="example" label="Example">

    suscribirte a txpool --enqueued
</TabItem>
</Tabs>

Suscripciones para eventos de tx en cola de cuenta.

---

### comandos de cadena de bloques {#blockchain-commands}

| **Comando** | **Descripción** |
|------------------------|-------------------------------------------------------------------------------------|
| estatus | Regresa el estatus al cliente. La respuesta detallada se puede encontrar abajo |
| monitor | Suscripciones a una secuencia de evento de cadena de bloques. La respuesta detallada se puede encontrar abajo |
| versión | Regresa la versión actual del cliente |

<h3>banderas de estatus</h3>

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    estatus [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    estatus --grpc-address 127.0.0.1:10003
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

<h3>banderas de monitor</h3>

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    monitor [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    monitor --grpc-address 127.0.0.1:10003
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

---

## Comandos de Secretos {#secrets-commands}

| **Comando** | **Descripción** |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| secretos dentro de | Inicializa las claves privadas al gestor de secretos correspondiente |
| secretos generados | Genera un archivo de configuración de administrador de secretos que puede ser analizado por Polygon Edge |

### banderas de entrada de secretos {#secrets-init-flags}

<h4><i>config</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secretos dentro de [--config SECRETS_CONFIG]
</TabItem>
  <TabItem value="example" label="Example">

    secretos init --config ./secretsManagerConfig.json
</TabItem>
</Tabs>

Establece la ruta hacia el archivo de configuración del administrador de secretos Utilizado por Hashicorp Vault. Si se omite, se utiliza el administrador local de secretos FS.

---

<h4><i>directorio de datos</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secretos init [--data-dir DATA_DIRECTORY]
</TabItem>
  <TabItem value="example" label="Example">

    secretos init --data-dir ./example-dir
</TabItem>
</Tabs>

Establece el directorio para los datos de Polygon Edge si se utiliza la FS local.

---

<h4><i>ecdsa</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secretos init [--ecdsa FLAG]
</TabItem>
  <TabItem value="example" label="Example">

    secretos init --ecdsa=false
</TabItem>
</Tabs>

Establece la bandera que indica si quieres generar una clave de ECDSA. Por defecto:`true`.

---

<h4><i>red</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secretos init [--network FLAG]
</TabItem>
  <TabItem value="example" label="Example">

    secretos init --network=false
</TabItem>
</Tabs>

Establece la bandera que indica si quieres generar una clave de red de Libp2p. Por defecto:`true`.

---

<h4><i>bls</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    secretos init [--bls FLAG]
</TabItem>
  <TabItem value="example" label="Example">

    secretos init --bls
</TabItem>
</Tabs>

Establece la bandera que indica si quieres generar una clave de BLS. Por defecto:`true`.

### los secretos generan banderas {#secrets-generate-flags}

<h4><i>dir</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    los secretos generan [--dir DATA_DIRECTORY]
</TabItem>
  <TabItem value="example" label="Example">

    los secretos generan --dir ./example-dir
</TabItem>
</Tabs>

Establece el directorio para el archivo de configuración de administrador de secretos por defecto: `./secretsManagerConfig.json`

---

<h4><i>tipo</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    los secretos generan [--type TYPE]
</TabItem>
  <TabItem value="example" label="Example">

    los secretos generan --type hashicorp-vault
</TabItem>
</Tabs>

Especifica el tipo de administrador de secretos. [`hashicorp-vault`] Por defecto: `hashicorp-vault`

---

<h4><i>token</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    los secretos generan [--token TOKEN]
</TabItem>
  <TabItem value="example" label="Example">

    los secretos generan --token s.zNrXa9zF9mgrdnClM7PZ19cu
</TabItem>
</Tabs>

Especifica el acceso de token para el servicio

---

<h4><i>url-del servidor</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    los secretos generan [--server-url SERVER_URL]
</TabItem>
  <TabItem value="example" label="Example">

    los secretos generan --server-url http://127.0.0.1:8200
</TabItem>
</Tabs>

Especifica la URL del servidor para el servicio

---

<h4><i>nombre</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    los secretos generan [--name NODE_NAME]
</TabItem>
  <TabItem value="example" label="Example">

    los secretos generan --name node-1
</TabItem>
</Tabs>

Especifica el nombre del nodo para los registros de servicio de mantenimiento. Por defecto: `polygon-edge-node`

---

<h4><i>espacio para nombres</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    los secretos generan [--namespace NAMESPACE]
</TabItem>
  <TabItem value="example" label="Example">

    los secretos generan --namespace my-namespace
</TabItem>
</Tabs>

Especifica el espacio para nombres utilizado para el administrador de secretos de Hashicorp Vault. Por defecto: `admin`

---

## Respuestas {#responses}

### Respuesta de estatus {#status-response}

El objeto de la respuesta se define usando el Protocolo Buffers.
````go title="minimal/proto/system.proto"
message ServerStatus {
    int64 network = 1;

    string genesis = 2;

    Block current = 3;

    string p2pAddr = 4;

    message Block {
        int64 number = 1;
        string hash = 2;
    }
}
````

### Respuesta de monitor {#monitor-response}
````go title="minimal/proto/system.proto"
message BlockchainEvent {
    // The "repeated" keyword indicates an array
    repeated Header added = 1;
    repeated Header removed = 2;

    message Header {
        int64 number = 1;
        string hash = 2;
    }
}
````

## Utilidades {#utilities}

### comandos de whitelist {#whitelist-commands}

| **Comando** | **Descripción** |
|------------------------|-------------------------------------------------------------------------------------|
| mostrar whitelist | Muestra la información de whitelist |
| despliegue de whitelist | Actualiza la lista de implementación whitelist de los contratos Smart  |

<h3>mostrar la whitelist</h3>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    mostrar la whitelist
</TabItem>
</Tabs>

Muestra la información de la whitelist

---

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    mostrar la whitelist [--chain GENESIS_FILE]
</TabItem>
  <TabItem value="example" label="Example">

    mostrar la whitelist --chain genesis.json
</TabItem>
</Tabs>

Especifica el archivo de génesis para actualizar. Por defecto:`./genesis.json`.

---

<h3>despliegue de whitelist</h3>

<h4><i>cadena</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    despliegue de la whitelist [--chain GENESIS_FILE]
</TabItem>
  <TabItem value="example" label="Example">

    despliegue de whitelist --chain genesis.json
</TabItem>
</Tabs>

Especifica el archivo de génesis para actualizar. Por defecto:`./genesis.json`.

---

<h4><i>agregar</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    despliegue de whitelist [--add ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    despliegue de whitelist --add 0x5383Cb489FaCa92365Bb6f9f1FB40bD032E6365d
</TabItem>
</Tabs>

Añade una nueva dirección al despliegue del contrato whitelist. Solo las direcciones en el despliegue del contrato whitelist puede desplegar a los contratos. Si está vacía, la dirección puede ejecutar el despliegue del contrato

---

<h4><i>eliminar</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    despliegue de whitelist [--remove dirección]
</TabItem>
  <TabItem value="example" label="Example">

    despliegue de whitelist --remove 0x5383Cb489FaCa92365Bb6f9f1FB40bD032E6365d
</TabItem>
</Tabs>

Elimina una dirección desde el despliegue del contrato whitelist. Solo las direcciones en el despliegue del contrato whitelist puede desplegar a los contratos. Si está vacía, la dirección puede ejecutar el despliegue del contrato

---

### banderas del robot de carga {#loadbot-flags}

<h4><i>tps</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--tps NUMBER_OF_TXNS_PER_SECOND]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --tps 2000
</TabItem>
</Tabs>

El número de transacciones por segundo para enviar. Por defecto:`100`.

---

<h4><i>modo</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--mode MODE]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --mode transfer
</TabItem>
</Tabs>

Establece los modos de ejecutar el robot de carga[`transfer``deploy`] Por defecto:`transfer`.

---

<h4><i>id de la cadena</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--chain-id CHAIN_ID]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --chain-id 100
</TabItem>
</Tabs>

Establece la identificación de la cadena de red para las transacciones. Por defecto:`100`.

---

<h4><i>precio-de-gas</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--gas-price GAS_PRICE]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --gas-price 10000
</TabItem>
</Tabs>

El precio del gas que debería ser utilizado para las transacciones. Si se omite, el precio del gas promedio se obtiene de la red.

---

<h4><i>límite-de-gas</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--gas-limit GAS_LIMIT]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --gas-limit 10000
</TabItem>
</Tabs>

El límite del precio del gas que debería ser utilizado para las transacciones. Si se omite, el límite del gas se estima antes de comenzar el robot de carga.

---

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga --grpc-address GRPC_ADDRESS
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --grpc-address 127.0.0.1:9645
</TabItem>
</Tabs>

El punto final del GRPC utilizado para enviar las transacciones

---

<h4><i>detallado</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--detailed DETAILED]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --detailed
</TabItem>
</Tabs>

La bandera indica si el error en los registros debe ser mostrado. Por defecto:`false`.

---

<h4><i>contrato</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--contract CONTRACT_PATH]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --contract ./myContract.json
</TabItem>
</Tabs>

La ruta al artefacto JSON del contrato que contiene el código de bytes. Si se omite, se utiliza un contrato por defecto.

---

<h4><i>remitente</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--sender ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --remitente 0x1010101010101010101010101010101010101020
</TabItem>
</Tabs>

Dirección de la cuenta del remitente.

---

<h4><i>receptor</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--receiver ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --receiver 0x1010101010101010101010101010101010101000
</TabItem>
</Tabs>

Dirección del receptor de la cuenta.

---

<h4><i>jsonrpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--jsonrpc ENDPOINT]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --jsonrpc http://127.0.0.1:8545
</TabItem>
</Tabs>

Un punto final de RPC JSON utilizado para enviar las transacciones.

---

<h4><i>contar</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--count COUNT]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --count 100
</TabItem>
</Tabs>

El número total de transacciones para enviar. Por defecto:`1000`.

---

<h4><i>valor</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--value VALUE]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --value 10000000000000000
</TabItem>
</Tabs>

El valor para él envió en cada transacción.

---

<h4><i>max-conns</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    robot de carga [--max-conns MAX_CONNECTIONS_COUNT]
</TabItem>
  <TabItem value="example" label="Example">

    robot de carga --max-conns 1000
</TabItem>
</Tabs>

Establece el máximo de conexiones no.of permitido por el huésped. Por defecto:`2*tps`.

---

### banderas de respaldo {#backup-flags}

<h4><i>direcciones-grpc</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    respaldo [--grpc-address GRPC_ADDRESS]
</TabItem>
  <TabItem value="example" label="Example">

    respaldo --grpc-address 127.0.0.1:9632
</TabItem>
</Tabs>

Dirección de la API gRPC. Por defecto:`127.0.0.1:9632`.

---

<h4><i>afuera</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    respaldo [--out OUT]
</TabItem>
  <TabItem value="example" label="Example">

    respaldo --out backup.dat
</TabItem>
</Tabs>

Ruta del archivo de almacenamiento para guardar.

---

<h4><i>desde</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    desde [--from FROM]
</TabItem>
  <TabItem value="example" label="Example">

    respaldo --from 0x0
</TabItem>
</Tabs>

La altura inicial de los bloques en el archivo. por defecto 0.

---

<h4><i>para</i></h4>

<Tabs>
  <TabItem value="syntax" label="Syntax" default>

    para [--to TO]
</TabItem>
  <TabItem value="example" label="Example">

    respaldo --to 0x2710
</TabItem>
</Tabs>

La altura final de los bloques en el archivo.

---

## Plantilla de Génesis {#genesis-template}
El archivo de génesis debería ser utilizado para establecer la declaración inicial de la cadena de bloques (por ejemplo, si algunas cuentas debieran tener un saldo de inicio).

El siguiente archivo *./genesis.json* se genera:
````json
{
    "name": "example",
    "genesis": {
        "nonce": "0x0000000000000000",
        "gasLimit": "0x0000000000001388",
        "difficulty": "0x0000000000000001",
        "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "coinbase": "0x0000000000000000000000000000000000000000",
        "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000"
    },
    "params": {
        "forks": {},
        "chainID": 100,
        "engine": {
            "pow": {}
        }
    },
    "bootnodes": []
}
````

### Directorio de datos {#data-directory}

Cuando se genera una bandera *data-dir* a **una carpeta de prueba-de-cadena** es generado.
 La estructura de la carpeta consiste en las siguientes sub-carpetas:
* **cadena de bloques** - Almacena el LevelDB para los objetos de la cadena de bloques
* **trie** - Almacena el LevelDB para los intentos de Merkle
* **almacén de claves** - Almacena claves privadas para el cliente. Esto incluye la clave privada libp2p y la clave privada de sellado/validador
* **consensus** - Almacena cualquier información consensus que el cliente podría necesitar mientras trabaja

## Recursos {#resources}
* **[Reservas de Protocolo](https://developers.google.com/protocol-buffers)**
