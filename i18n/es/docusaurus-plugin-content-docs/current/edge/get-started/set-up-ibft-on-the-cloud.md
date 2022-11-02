---
id: set-up-ibft-on-the-cloud
title: Configuración de la nube
description: "Guía de configuración de la nube paso a paso."
keywords:
  - docs
  - polygon
  - edge
  - cloud
  - setup
  - genesis
---

:::info Esta guía es para configurar la red principal o la red de prueba

La guía que está abajo te indicará cómo configurar una red Polygon Edge en un proveedor en la nube para una configuración de producción de tu red de prueba o de tu red principal.

Si quieres configurar una red de Polygon Edge de forma local para hacer pruebas de forma rápida antes `polygon-edge`de hacer una configuración de producción, consulta
 [Configuración local](/docs/edge/get-started/set-up-ibft-locally)

:::

## Requisitos {#requirements}

Consulta [la parte que](/docs/edge/get-started/installation) se refiere a Instalación para instalar Polygon Edge.

### Cómo configurar la conectividad de la máquina virtual (VM) {#setting-up-the-vm-connectivity}

Según el proveedor en la nube que elijas, puedes configurar la conectividad y las reglas entre las máquinas virtuales con un firewall,
 grupos de seguridad o lista de control de acceso.

`polygon-edge`Como la única parte que se necesita que esté expuesta a otras máquinas virtuales es el servidor libp-2p, solo con permitir
 toda la comunicación entre las máquinas virtuales en el puerto libp-2p por defecto, `1478`es suficiente.

## Resumen {#overview}

![Configuración en la nube](/img/edge/ibft-setup/cloud.svg)

A través de esta guía, nuestro objetivo es establecer una red de cadena de `polygon-edge`bloques que funcione a través de la utilización del [protocolo de consenso IBFT](https://github.com/ethereum/EIPs/issues/650).
 La red de cadena de bloques constará de 4 nodos, de los cuales la totalidad son nodos validadores y, por lo tanto, son elegibles tanto para proponer bloques y para validar bloques que provienen de otros proponentes.
 Cada uno de los 4 nodos se ejecutará en su propia VM, ya que el propósito de esta guía es proporcionarte una red Polygon Edge completamente funcional, al tiempo que las claves de los validadores se mantienen privadas para una configuración de red sin confianza.

Para lograrlo, te guiaremos a través de 4 pasos sencillos:

0. Dale un vistazo a la lista de **Requisitos** que se publicó anteriormente
1. Genera las claves privadas para cada uno de los validadores e inicializa el directorio de datos
2. Prepara el hilo de conexión que el bootnode se pueda para compartir`genesis.json`
3. `genesis.json`Crea el en tu máquina local y envíalo/transfiérelo a cada uno de los nodos
4. Inicia todos los nodos

:::info Número de validadores

No hay un mínimo para el número de validadores en un clúster, lo que implica que los clústeres con solo 1 nodo validador son posibles. Ten en cuenta que con un _simple_ clúster de nodos, no hay **tolerancia al choque** y no hay **garantía BFT**.

El número mínimo de nodos recomendado para lograr una garantía BFT es 4, ya que en un clúster de 4 nodos, la falla de
 1 nodo se puede tolerar y los otros 3 permanecen funcionando con normalidad.

:::

## Paso 1: inicializa las carpetas de datos y genera las claves de los validadores {#step-1-initialize-data-folders-and-generate-validator-keys}

Para ponerte en marcha con Polygon Edge, es necesario que incialices la carpeta de datos, en cada nodo:


````bash
node-1> polygon-edge secrets init --data-dir data-dir
````

````bash
node-2> polygon-edge secrets init --data-dir data-dir
````

````bash
node-3> polygon-edge secrets init --data-dir data-dir
````

````bash
node-4> polygon-edge secrets init --data-dir data-dir
````

Cada uno de los comandos imprimirá la clave del [validador](https://docs.libp2p.io/concepts/peer-id/), la clave BLS pública y la identificación del nodo. Necesitarás la identificación del primero de los nodos para el paso siguiente.

:::warning Guarda la clave pública BLS

Si la red se está ejecutando con BLS, lo que se hace por defecto, se solicita la clave pública BLS para proponer en el modo PoA y para hacer staking en el modo PoS. Polygon solo guarda la llave privada BLS; es tu responsabilidad preservar la clave pública BLS.

:::

:::warning ¡No compartas tu directorio de datos con nadie!

Los directorios de datos que se generaron anteriormente, además de inicializar los directorios para mantener el estado de la cadena de bloques, también generarán tus claves privadas de validador.
 **Esta clave se debe mantener en secreto, ya que, si te la roban, alguien podrán hacerse pasar por el validador en la red.**

:::

## Paso 2: prepara el hilo de conexión multiaddr para el Bootnode {#step-2-prepare-the-multiaddr-connection-string-for-the-bootnode}

Para que un nodo establezca la conectividad con éxito, debes saber qué `bootnode`servidor conectar para obtener
 información sobre todos los nodos restantes de la red. El `bootnode`a veces también se conoce como el servidor `rendezvous` en la jerga p2p.

`bootnode`no es una instancia especial del nodo de Polygon Edge. Cada nodo de Polygon edge puede funcionar como un `bootnode`y
 cada nodo de Polygon Edge necesita tener un conjunto de Bootnodes específicos, que se contactarán para proporcionar información sobre cómo conectar con
 todos los nodos restantes de la red.

Para crear el hilo de conexión para especificar el bootnode, es necesario ajustarse
 al [formato multiaddr](https://docs.libp2p.io/concepts/addressing/):
```
/ip4/<ip_address>/tcp/<port>/p2p/<node_id>
```

En esta guía, trataremos los primeros y segundos nodos como los bootnodes para todos los otros nodos. Lo que sucederá en este escenario
 `node 1`es que los nodos que se `node 2`conectan a o a obtendrán información sobre cómo conectar unos a otros, a través del nodo que se contactó de forma mutua.

:::info Es necesario especificar al menos un bootnode para iniciar un nodo

Se requiere al menos **un** bootnode, para que los otros nodos de la red puedan descubrir entre sí. Se recomiendan más bootnodes, ya que
 estos proporcionan resiliencia a la red en caso de interrupciones.
 En esta guía, enumeraremos dos nodos, pero esto se puede cambiar sobre la marcha, sin consecuencias en la validez del archivo `genesis.json`.

:::

Como la primera parte del hilo de la conexión multiaddr es la `<ip_address>`, en este punto necesitarás ingresar una dirección IP a la que se pueda llegar a través de otros nodos; según tu configuración puede ser una dirección IP pública o privada, no `127.0.0.1`.

Para `<port>` utilizaremos `1478`, ya que es el puerto libp2p por defecto.

Y, por último, se necesita el , el `<node_id>`cual podemos obtener del resultado del comando `polygon-edge secrets init --data-dir data-dir` que se ejecutó anteriormente para generar claves y directorios de datos para el `node 1`)

Después del ensamblaje, el hilo de conexión multiaddr que va al `node 1` que utilizaremos como un bootnode, buscará algo como esto (solo el `<node_id>`que está en el extremo debería ser diferente):
```
/ip4/<public_or_private_ip>/tcp/1478/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
```
Del mismo modo, construimos multiaddr para el segundo bootnode, como se muestra abajo
```
/ip4/<public_or_private_ip>/tcp/1478/p2p/16Uiu2HAmS9Nq4QAaEiogE4ieJFUYsoH28magT7wSvJPpfUGBj3Hq
```
:::info Nombres de host DNS en lugar de nombres de IP

Polygon Edge es compatible con los nombres de host DNS para los nodos de configuración. Esta es una función muy útil para las implementaciones basadas en la nube, ya que el IP del nodo puede cambiar a causa de varias razones.

El formato multiaddr para el hilo de conexión mientas se utilizan nombres de host DNS, como se indica a continuación:`/dns4/sample.hostname.com/tcp/<port>/p2p/nodeid`


:::

## Paso 3: generar el archivo génesis con los 4 nodos como validadores {#step-3-generate-the-genesis-file-with-the-4-nodes-as-validators}

Ese paso se puede ejecutar en tu máquina local, pero deberás tener las llaves públicas de validador para cada uno de los 4 validadores.

Los validadores pueden compartir el `Public key (address)` de forma segura, como se muestra a continuación en el resultado de sus comandos `secrets init`, de manera que
 puedes generar de forma segura el archivo genesis.json con aquellos validadores en el conjunto validador, que se identifica por sus claves públicas:

```
[SECRETS INIT]
Public key (address) = 0xC12bB5d97A35c6919aC77C709d55F6aa60436900
BLS Public key       = 0x9952735ca14734955e114a62e4c26a90bce42b4627a393418372968fa36e73a0ef8db68bba11ea967ff883e429b3bfdf
Node ID              = 16Uiu2HAmVZnsqvTwuzC9Jd4iycpdnHdyVZJZTpVC8QuRSKmZdUrf
```

Dado que has recibido las 4 claves públicas de los validadores, puedes ejecutar el siguiente comando para generar el `genesis.json`

````bash
polygon-edge genesis --consensus ibft --ibft-validator=0xC12bB5d97A35c6919aC77C709d55F6aa60436900 --ibft-validator=<2nd_validator_pubkey> --ibft-validator=<3rd_validator_pubkey> --ibft-validator=<4th_validator_pubkey> --bootnode=<first_bootnode_multiaddr_connection_string_from_step_2> --bootnode <second_bootnode_multiaddr_connection_string_from_step_2> --bootnode <optionally_more_bootnodes>
````

Lo que hace este comando es lo siguiente:

* El  `--ibft-validator`establece la clave pública del validador que se debe incluir en el conjunto de validadores inicial del bloque génesis. Puede haber muchos validadores iniciales.
* El `--bootnode` establece la dirección del bootnode que habilitará que los nodos se encuentren entre sí
 Utilizaremos el hilo multiaddr del `node 1`, como se mencionó en el **Paso 2**, aunque siempre puedes agregar tantos bootnode como desees, como se muestra anteriormente.

:::info Saldos de cuentas de priminería

Es probable que quieras configurar tu red de cadena de bloques con algunas direcciones que tengan saldos “preminados”.

Para eso, pasa tantas banderas `--premine`como desees por cada dirección que quieras que se inicialice con un determinado saldo
 en la cadena de bloques.

`0x3956E90e632AEbBF34DEB49b71c28A83Bc029862`Por ejemplo, si nos gustaría preminar 1000 ETH para dirigir en nuestro bloque génesis, tendríamos que proporcionar el siguiente argumento:

```
--premine=0x3956E90e632AEbBF34DEB49b71c28A83Bc029862:1000000000000000000000
```

**Ten en cuenta que la cantidad preminada está en WEI, no en ETH.**

:::

:::info Establece el límite de gas del bloque

El límite de gas por defecto de cada bloque es `5242880`. Este valor está escrito en el archivo génesis, pero es posible que quieras
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



```shell
--block-gas-limit 1000000000
```

:::

:::info




-
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

-
	-
	```shell
	ulimit -u 65535
	```
	-
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

:::


1.
2.
3.





##  {#step-4-run-all-the-clients}

:::note






####  {#example}





`polygon-edge ... --libp2p 0.0.0.0:10001 --nat 192.0.2.1`



`polygon-edge ... --libp2p 0.0.0.0:10001 --dns dns/example.io`



:::




````bash
node-1> polygon-edge server --data-dir ./data-dir --chain genesis.json  --libp2p 0.0.0.0:1478 --nat <public_or_private_ip> --seal
````



````bash
node-2> polygon-edge server --data-dir ./data-dir --chain genesis.json --libp2p 0.0.0.0:1478 --nat <public_or_private_ip> --seal
````



````bash
node-3> polygon-edge server --data-dir ./data-dir --chain genesis.json --libp2p 0.0.0.0:1478 --nat <public_or_private_ip> --seal
````



````bash
node-4> polygon-edge server --data-dir ./data-dir --chain genesis.json --libp2p 0.0.0.0:1478 --nat <public_or_private_ip> --seal
````



:::info



````bash
polygon-edge server --config <config_file_path>
````


````bash
polygon-edge server --config ./test/config-node1.json
````


:::

:::info



````bash
polygon-edge server --data-dir <directory_path> --chain <genesis_filename>  --libp2p <IPAddress:PortNo> --nat <public_or_private_ip>
````


````bash
polygon-edge server --data-dir ./data-dir --chain genesis.json --libp2p 0.0.0.0:1478 --nat<public_or_private_ip>
````
:::

:::info











````bash
polygon-edge server --price-limit 100000 ...
````


:::

:::info



````bash
ws://localhost:10002/ws
````



````bash
wss://rpc-edgenet.polygon.technology/ws
````
:::