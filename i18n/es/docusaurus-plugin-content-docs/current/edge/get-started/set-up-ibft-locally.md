---
id: set-up-ibft-locally
title: Configuración Local

description: "Guía de configuración local paso a paso."
keywords:
  - docs
  - polygon
  - edge
  - local
  - setup
  - genesis
---

:::caution Esta guía es solo para probar propósitos

La guía de abajo te indicará cómo configurar una red de Polygon Edge en tu máquina local para probar y desarrollar propósitos.

El procedimiento difiere enormemente de la forma en que desearías configurar la red Polygon Edge para un escenario de uso real en un proveedor de nube: [Configuración de nube](/docs/edge/get-started/set-up-ibft-on-the-cloud)

:::


## Requisitos {#requirements}

Consulta el apartado [Instalación](/docs/edge/get-started/installation) para instalar Polygon Edge.

## Resumen {#overview}

![Configuración Local
](/img/edge/ibft-setup/local.svg)

A través de esta guía, nuestro objetivo es establecer una red de cadena de bloques `polygon-edge`que funcione a través de la utilización del [protocolo de consenso IBFT](https://github.com/ethereum/EIPs/issues/650).
 La red de cadena de bloques consistirá de 4 nodos, de los cuales la totalidad son nodos validadores y, por lo tanto, son elegibles tanto para proponer bloques como para validar bloques que provienen de otros proponentes.
 Todos los 4 nodos se ejecutarán en la misma máquina, ya que la idea de esta guía es de darte un grupo IBFT completamente funcional en la cantidad mínima de tiempo.

Para lograrlo, te guiaremos a través de estos 4 pasos sencillos:

1. Inicializar los datos de los directorios generará ambas claves de validador para cada uno de los 4 nodos e inicializará los directorios de datos de cadena de bloques vacíos. Las claves de validador son importantes, ya que necesitamos arrancar el bloque genesis con el grupo inicial de validadores que utilizan estas claves.
2. Preparar la cadena de conexión para el arranque será la información vital para conectar cada nodo que vamos a ejecutar en cuanto a cuál nodo conectar cuando se inicia por primera vez.
3. La generación del archivo `genesis.json`requerirá como entrada tanto las claves de validación generadas en el **paso 1** utilizadas para configurar los validadores iniciales de la red en el bloque de génesis y la cadena de conexión del nodo de arranque del **paso 2**.
4. Ejecutar todos los nodos es el objetivo final de esta guía y será el último paso que daremos, indicaremos a los nodos qué directorio de datos usar y dónde encontrar el`genesis.json`que arranca el estado inicial de la red.

Como todos los cuatro nodos se estarán ejecutando en el huésped local durante el proceso de instalación, se espera que todos los datos de los directorios para cada uno de los nodos están en el mismo directorio principal.

:::info Cantidad de validadores

No existe un límite mínimo para la cantidad de nodos en un clúster, lo que implica que pueden existir clústeres con solo 1 nodo validador.
 Ten en cuenta que con un _único_ grupo de nodos, no existe **tolerancia a fallas** y **no hay garantía de BFT**.

La cantidad mínima de nodos recomendada para lograr una garantía a la BFT es 4, ya que, en un clúster de 4 nodos, la falla de
 1 nodo se puede tolerar y los otros 3 permanecen funcionando con normalidad.

:::

## Paso 1: Inicializa las carpetas de datos para IBFT y genera las claves del validador {#step-1-initialize-data-folders-for-ibft-and-generate-validator-keys}

Para comenzar el funcionamiento con IBFT, debe inicializar las carpetas de datos, uno para cada nodo:

````bash
polygon-edge secrets init --data-dir test-chain-1
````

````bash
polygon-edge secrets init --data-dir test-chain-2
````

````bash
polygon-edge secrets init --data-dir test-chain-3
````

````bash
polygon-edge secrets init --data-dir test-chain-4
````

Cada uno de estos comandos imprimirá la clave del validador, la clave BLS pública y la [ID del nodo](https://docs.libp2p.io/concepts/peer-id/). Necesitarás la identificación del primero de los nodos para el paso siguiente.

:::warning Guarda la clave pública de BLS

Si la red se está ejecutando con BLS lo cual sucede por defecto, se requiere la clave pública BLS para proponer en el modo PoA y para participar en el modo PoS. Polygon Edge solo guarda la clave privada de BLS, es la responsabilidad del usuario preservar la clave privada de BLS.

:::

## Paso 2: Prepara la cadena de conexión multiaddr para el nodo de arranque {#step-2-prepare-the-multiaddr-connection-string-for-the-bootnode}

Para que un nodo establezca la conectividad de forma exitosa, debe saber a cuál `bootnode`servidor conectarse para obtener
 información acerca de todos los otros nodos de la red. Él `bootnode`también se lo denomina como servidor`rendezvous` en la jerga p2p.

`bootnode`no es una instancia especial del nodo de Polygon Edge Cada nodo de Polygon Edge puede servir como un`bootnode`, pero
 cada nodo de Polygon Edge necesita tener un conjunto de nodos especificados de arranque que se contactarán para proporcionar información sobre cómo conectarse con todos los otros nodos de la red.

Con el fin de crear la cadena de conexión para especificar el nodo de arranque, necesitamos ajustarnos
 al [formato multiaddr](https://docs.libp2p.io/concepts/addressing/):
```
/ip4/<ip_address>/tcp/<port>/p2p/<node_id>
```

En esta guía, trataremos los primeros y segundos nodos como los nodos de arranque para todos los otros nodos. Lo que sucederá en este escenario
 es que los nodos que se conectan al`node 1` u `node 2`obtendrán información sobre cómo conectarse unos con otros, a través del nodo de arranque
 que se contactó de forma mutua.

:::info Es necesario que especifiques al menos un bootnode para iniciar un nodo

Se requiere como mínimo **un** bootnode para que los otros nodos de la red puedan descubrirse entre sí. Se recomiendan más bootnodes, ya que
 estos proporcionan resiliencia a la red en caso de interrupciones.
 En esta guía, mencionaremos dos nodos, pero esto se puede cambiar sobre la marcha, sin consecuencias sobre la validez del archivo`genesis.json`.

:::

Dado que estamos ejecutando en el huésped local, es seguro suponer que`<ip_address>` es`127.0.0.1`.

Para él `<port>`usaremos `10001`dado que configuraremos el servidor libp2p para que `node 1`escuche en este puerto más adelante.

Y, por último, necesitamos él`<node_id>` el cual podemos obtener del resultado del comando`polygon-edge secrets init --data-dir test-chain-1` que se ejecutó anteriormente para generar claves y directorios de datos para él`node1`

Después del ensamblaje, la cadena de conexión multiaddr que va al`node 1` que utilizaremos como el bootnode, se verá así (solo el `<node_id>`que está al final debería variar):
```
/ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
```
Del mismo modo, construimos el multiaddr para el segundo nodo de arranque como se muestra a continuación.
```
/ip4/127.0.0.1/tcp/20001/p2p/16Uiu2HAmS9Nq4QAaEiogE4ieJFUYsoH28magT7wSvJPpfUGBj3Hq
```

:::info Nombres de los huéspedes DNS en lugar de IP

Polygon Edge es compatible con los nombres de los huéspedes DNS para la configuración de los nodos. Esta es una función muy útil para las implementaciones basadas en la nube, ya que la IP del nodo puede cambiar por varias razones.

El formato multiaddr para la cadena de conexión cuando se utilizan nombres de huéspedes DNS es el siguiente:
`/dns4/sample.hostname.com/tcp/<port>/p2p/nodeid`

:::


## Paso 3 Generar el archivo genesis con los 4 nodos como validadores {#step-3-generate-the-genesis-file-with-the-4-nodes-as-validators}

````bash
polygon-edge genesis --consensus ibft --ibft-validators-prefix-path test-chain- --bootnode /ip4/127.0.0.1/tcp/10001/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW --bootnode /ip4/127.0.0.1/tcp/20001/p2p/16Uiu2HAmS9Nq4QAaEiogE4ieJFUYsoH28magT7wSvJPpfUGBj3Hq
````

Lo que hace este comando es lo siguiente:

* Él`--ibft-validators-prefix-path` establece la ruta de la carpeta de prefijo a la especificada que IBFT en Polygon Edge puede
 usar Este directorio se utiliza para hospedar la carpeta`consensus/` donde se guarda la clave privada del validador. La clave pública de validador es necesaria para construir el archivo de genesis - la lista inicial de nodos de arranque. Esta bandera solo tiene sentido cuando se configura en la red del huésped local como en un escenario del mundo real no podemos esperar que todos los directorios de datos de los nodos para estar en el mismo sistema de archivos desde donde podemos leer fácilmente las claves públicas.
* Él`--bootnode` establece la dirección del nodo de arranque que habilitará que los nodos se encuentren entre sí.
 Usaremos la cadena multiaddr del`node 1`, como se menciona en **paso 2**.

El resultado de este comando es el archivo `genesis.json`que contiene el bloque de génesis de nuestra nueva cadena de bloques, con el conjunto de validadores predefinidos y la configuración para cual nodo contactar primero para establecer la conectividad.

:::info Saldos de cuentas de preminado

Es probable que quieras configurar tu red de cadena de bloques con algunas direcciones que tengan saldos “preminados”.

Para conseguir eso, pasa tantas banderas `--premine`como desees por cada dirección que quieras que se inicialice con un determinado saldo
 en la cadena de bloques.

Por ejemplo, si nos gustaría preminar 1000 ETH para la dirección `0x3956E90e632AEbBF34DEB49b71c28A83Bc029862` de nuestro bloque genesis, tendríamos que proporcionar el siguiente argumento:

```
--premine=0x3956E90e632AEbBF34DEB49b71c28A83Bc029862:1000000000000000000000
```

**Ten en cuenta que la cantidad preminada está en WEI, no en ETH.**

:::

:::info Establece el gas limit del bloque

El gas limit por defecto de cada bloque es `5242880`. Este valor se escribe en el archivo genesis, pero es posible que quieras
 aumentarlo o disminuirlo.

```go title="command/helper/helper.go"
const (
	GenesisFileName       = "./genesis.json"
	DefaultChainName      = "example"
	DefaultChainID        = 100
	DefaultPremineBalance = "0x3635C9ADC5DEA00000"
	DefaultConsensus      = "pow"
	GenesisGasUsed        = 458752
	GenesisGasLimit       = 5242880 // The default block gas limit
)
```

Para hacer eso, puedes usar la bandera `--block-gas-limit` seguida del valor deseado, como se muestra a continuación:

```shell
--block-gas-limit 1000000000
```

:::

:::info Establece el límite descriptor de archivos del sistema

El límite descriptor de archivos por defecto (máximo número de archivos abiertos) en algunos sistemas operativos es bastante pequeño. Si se espera que los nodos tengan un rendimiento elevado, quizá deberías considerar aumentar este límite en el nivel del sistema operativo.

Para la distribución Ubuntu, el procedimiento es el siguiente: (si no estás usando distribución Ubuntu o Debian, revisa los documentos oficiales para tu sistema operativo):
- Revisa los límites actuales del sistema operativo (archivos abiertos)
```shell title="ulimit -a"
ubuntu@ubuntu:~$ ulimit -a
core file size          (blocks, -c) 0
data seg size           (kbytes, -d) unlimited
scheduling priority             (-e) 0
file size               (blocks, -f) unlimited
pending signals                 (-i) 15391
max locked memory       (kbytes, -l) 65536
max memory size         (kbytes, -m) unlimited
open files                      (-n) 1024
pipe size            (512 bytes, -p) 8
POSIX message queues     (bytes, -q) 819200
real-time priority              (-r) 0
stack size              (kbytes, -s) 8192
cpu time               (seconds, -t) unlimited
max user processes              (-u) 15391
virtual memory          (kbytes, -v) unlimited
file locks                      (-x) unlimited
```

- Aumentar el límite de archivos abiertos
	- De manera local. Solo afecta a la sesión actual:
	```shell
	ulimit -u 65535
	```
	- De manera global o por usuario (agrega límites al final del archivo /etc/security/limits.conf):
	```shell
	sudo vi /etc/security/limits.conf  # we use vi, but you can use your favorite text editor
	```
	```shell title="/etc/security/limits.conf"
	# /etc/security/limits.conf
	#
	#Each line describes a limit for a user in the form:
	#
	#<domain>        <type>  <item>  <value>
	#
	#Where:
	#<domain> can be:
	#        - a user name
	#        - a group name, with @group syntax
	#        - the wildcard *, for default entry
	#        - the wildcard %, can be also used with %group syntax,
	#                 for maxlogin limit
	#        - NOTE: group and wildcard limits are not applied to root.
	#          To apply a limit to the root user, <domain> must be
	#          the literal username root.
	#
	#<type> can have the two values:
	#        - "soft" for enforcing the soft limits
	#        - "hard" for enforcing hard limits
	#
	#<item> can be one of the following:
	#        - core - limits the core file size (KB)
	#        - data - max data size (KB)
	#        - fsize - maximum filesize (KB)
	#        - memlock - max locked-in-memory address space (KB)
	#        - nofile - max number of open file descriptors
	#        - rss - max resident set size (KB)
	#        - stack - max stack size (KB)
	#        - cpu - max CPU time (MIN)
	#        - nproc - max number of processes
	#        - as - address space limit (KB)
	#        - maxlogins - max number of logins for this user

	#        - maxsyslogins - max number of logins on the system
	#        - priority - the priority to run user process with
	#        - locks - max number of file locks the user can hold
	#        - sigpending - max number of pending signals
	#        - msgqueue - max memory used by POSIX message queues (bytes)
	#        - nice - max nice priority allowed to raise to values: [-20, 19]
	#        - rtprio - max realtime priority
	#        - chroot - change root to directory (Debian-specific)
	#
	#<domain>      <type>  <item>         <value>
	#

	#*               soft    core            0
	#root            hard    core            100000
	#*               hard    rss             10000
	#@student        hard    nproc           20
	#@faculty        soft    nproc           20
	#@faculty        hard    nproc           50
	#ftp             hard    nproc           0
	#ftp             -       chroot          /ftp
	#@student        -       maxlogins       4

	*               soft    nofile          65535
	*               hard    nofile          65535

	# End of file
	```
Como alternativa, puedes modificar parámetros adicionales, guardar el archivo y reiniciar el sistema.
 Después de reiniciar, revisa el límite descriptor de archivo de nuevo.
 Debería estar configurado según el valor que definiste en el archivo limits.conf.

:::


## Paso 4: ejecutar todos los clientes {#step-4-run-all-the-clients}

Debido a que vamos a intentar ejecutar una red Polygon Edge que consiste en 4 nodos todos en la misma máquina, necesitamos tomar cuidado de evitar los conflictos de puerto. Es por esto que utilizaremos el siguiente razonamiento para determinar los puertos de escucha de cada servidor de nodos:

- `10000` para el servidor gRPC de`node 1` `20000` para el servidor GRPC de`node 2`, etc.
- `10001` para el servidor libp2p de`node 1`, `20001`para el servidor libp2p de`node 2`, etc.
- `10002` para el servidor JSON-RPC de`node 1`, `20002`para el servidor JSON-RPC de`node 2`, etc.

Para ejecutar el **primer** cliente (tenga en cuenta el puerto, `10001`ya que se usó como parte de libp2p multiaddr en el **paso 2** junto con la ID 1 del nodo):

````bash
polygon-edge server --data-dir ./test-chain-1 --chain genesis.json --grpc-address :10000 --libp2p :10001 --jsonrpc :10002 --seal
````

Para ejecutar el **segundo** cliente:

````bash
polygon-edge server --data-dir ./test-chain-2 --chain genesis.json --grpc-address :20000 --libp2p :20001 --jsonrpc :20002 --seal
````

Para ejecutar el **tercer** cliente:

````bash
polygon-edge server --data-dir ./test-chain-3 --chain genesis.json --grpc-address :30000 --libp2p :30001 --jsonrpc :30002 --seal
````

Para ejecutar el **cuarto** cliente:

````bash
polygon-edge server --data-dir ./test-chain-4 --chain genesis.json --grpc-address :40000 --libp2p :40001 --jsonrpc :40002 --seal
````

Revisar brevemente lo que se ha hecho hasta ahora:

* Se ha especificado que el directorio para los datos del cliente sea **./test-chain-\***
* Los servidores GRPC se han iniciado en los puertos **10000**, **20000**, **30000** y **40000**, para cada nodo respectivamente
* Los servidores libp2p se han iniciado en los puertos. **10001**, **20001**, **30001** y **40001**, para cada nodo respectivamente
* Los servidores JSON-RPC se han iniciado en los puertos. **10002**, **20002**, **30002** y **40002**, para cada nodo respectivamente
* Él *sello* de la bandera significa que el nodo que se está comenzando va a participar en el sellado del bloque
* La *bandera de la cadena*especifica qué archivo de génesis debe usarse para la configuración de la cadena

Puedes obtener más información sobre la estructura del archivo genesis en la sección [Comandos CLI](/docs/edge/get-started/cli-commands).

Después de ejecutar los comandos previos, has configurado una red Polygon Edge de 4 nodos, capaz de sellar bloques y de recuperarse
 de un fallo en el nodo.

:::info Iniciar al cliente mediante el archivo configuración

En lugar de especificar todos los parámetros de configuración como argumentos CLI, el cliente también puede iniciar mediante un archivo configuración, si se ejecuta el siguiente comando:

````bash
polygon-edge server --config <config_file_path>
````
Ejemplo:

````bash
polygon-edge server --config ./test/config-node1.json
````
Actualmente, solo tenemos apoyo `json`basado en el ejemplo de archivo de configuración que se puede encontrar [aquí](/docs/edge/configuration/sample-config)

:::

:::info Pasos para ejecutar un nodo no validador

Un no validador siempre se sincronizará con los últimos bloques que haya recibido del nodo validador; puedes iniciarse en un nodo no validador ejecutando el siguiente comando:

````bash
polygon-edge server --data-dir <directory_path> --chain <genesis_filename> --grpc-address <portNo> --libp2p <portNo> --jsonrpc <portNo>
````
Por ejemplo, puedes agregar **el quinto** cliente no validador al ejecutar el siguiente comando:

````bash
polygon-edge server --data-dir ./test-chain --chain genesis.json --grpc-address :50000 --libp2p :50001 --jsonrpc :50002
````
:::

:::info Especificar el precio límite

Un nodo Polygon Edge se puede iniciar con un **límite de precio** establecido para las transacciones entrantes.

La unidad para el límite de precio es`wei`.

Establecer un límite de precio implica que cualquier transacción que se procese a través del nodo actual necesita tener un precio de gas**más alto** entonces el límite de precio establecido, de lo contrario, no se incluirá en un bloque.

El hecho de que la mayoría de los nodos respeten un determinado límite de precio genera que se cumpla la regla de que las transacciones en la red
 no pueden estar por debajo de un cierto umbral de precio.

El valor por defecto del límite de precio es`0`, lo que significa que no se aplica a todo por defecto.

Ejemplo de cómo utilizar la bandera`--price-limit`:
````bash
polygon-edge server --price-limit 100000 ...
````

Vale la pena señalar que los precios límite **se cumplen solo sobre transacciones no locales**, lo que significa
 que el precio límite no se aplica a transacciones que se añaden al nodo de forma local.

:::

:::info URL WebSocket

Por defecto, cuando ejecutas el Polygon Edge, se genera una URL WebSocket en función de la ubicación de la cadena.
 El esquema URL `wss://`se usa para enlaces HTTPS y él `ws://`para HTTP.

URL del WebSocket del huésped local:
````bash
ws://localhost:10002/ws
````
Ten en cuenta que el número del puerto depende del puerto JSON-RPC elegido para el nodo.

URL del WebSocket de Edgenet
````bash
wss://rpc-edgenet.polygon.technology/ws
````
:::



## paso 5: interactuar con la red de Polygon-Edge {#step-5-interact-with-the-polygon-edge-network}

Ahora que has configurado al menos 1 cliente que ejecute, puedes continuar e interactuar con la cadena de bloques utilizando la cuenta que preminaste arriba y al especificar la URL JSON-RPC a cualquiera de los 4 nodos:
- Nodo 1: `http://localhost:10002`
- Nodo 2: `http://localhost:20002`
- Nodo 3: `http://localhost:30002`
- Nodo 4: `http://localhost:40002`

Siga esta guía para emitir comandos de operador al recién construido grupo: [Cómo consultar la información del operador](/docs/edge/working-with-node/query-operator-info) (los puertos GRPC para el grupo que hemos construido son `10000`/`20000`/`30000`/`40000` para cada nodo respectivamente)