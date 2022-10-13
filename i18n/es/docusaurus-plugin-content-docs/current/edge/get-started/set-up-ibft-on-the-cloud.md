---
id: set-up-ibft-on-the-cloud
title: Configuración en la nube
description: "Guía de configuración en la nube paso a paso."
keywords:
  - docs
  - polygon
  - edge
  - cloud
  - setup
  - genesis
---

:::info Esta guía es para configurar la red principal o la red de prueba

La guía que está a continuación te indicará cómo configurar una red Polygon Edge en un proveedor en la nube para una configuración de producción de tu red de prueba o de tu red principal.

Si quieres configurar una red Polygon Edge de forma local para probar con rapidez el `polygon-edge` antes de hacer una configuración de producción, consulta
 [Configuración local](/docs/edge/get-started/set-up-ibft-locally)

:::

## Requisitos {#requirements}

Consulta el apartado [Instalación](/docs/edge/get-started/installation) para instalar Polygon Edge.

### Cómo configurar la conectividad de la máquina virtual (VM) {#setting-up-the-vm-connectivity}

Según el proveedor en la nube que elijas, puedes configurar la conectividad y las reglas entre las VM, a través de un firewall,
 grupos de seguridad o listas de control de acceso.

Como la única parte de `polygon-edge` que se necesita que esté expuesta a otras VM es el servidor libp-2p, solo con permitir
 toda la comunicación entre las VM en el puerto libp-2p por defecto, `1478`es suficiente.

## Resumen {#overview}

![Configuración en la nube](/img/edge/ibft-setup/cloud.svg)

A través de esta guía, nuestro objetivo es establecer una red de cadena de bloques `polygon-edge`que funcione a través de la utilización del [protocolo de consenso IBFT](https://github.com/ethereum/EIPs/issues/650).
 La red de cadena de bloques constará de 4 nodos, de los cuales la totalidad son nodos validadores y, por lo tanto, son elegibles tanto para proponer bloques como para validar bloques que provienen de otros proponentes.
 Cada uno de los 4 nodos se ejecutará en su propia VM, ya que el propósito de esta guía es proporcionarte una red Polygon Edge completamente funcional, al tiempo que las claves de los validadores se mantienen privadas para garantizar una configuración de red sin confianza.

Para lograrlo, te guiaremos a través de 4 pasos sencillos:

0. Dale un vistazo a la lista de **Requisitos** que se publicó anteriormente
1. Genera las claves privadas para cada uno de los validadores e inicializa el directorio de datos
2. Prepara la cadena de conexión para que el bootnode se coloque en el `genesis.json` compartido
3. Crea el `genesis.json` en tu máquina local y envíalo/transfiérelo a cada uno de los nodos
4. Inicia todos los nodos

:::info Número de validadores

No hay un mínimo para el número de validadores en un clúster, lo que implica que pueden existir clústeres con solo 1 nodo validador. Ten en cuenta que con un clúster de nodos _simple_ no existe **tolerancia a fallas** **ni garantía por fallas bizantinas (BFT)**.

El número mínimo de nodos recomendado para lograr una garantía BFT es 4, ya que, en un clúster de 4 nodos, la falla de
 1 nodo se puede tolerar y los otros 3 permanecen funcionando con normalidad.

:::

## Paso 1: inicializa las carpetas de datos y genera las claves de los validadores {#step-1-initialize-data-folders-and-generate-validator-keys}

Para ponerte en marcha con Polygon Edge, es necesario que inicialices las carpetas de datos, en cada nodo:


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

Cada uno de estos comandos imprimirá la clave del validador, la clave BLS pública y la [ID del nodo](https://docs.libp2p.io/concepts/peer-id/). Necesitarás la ID de nodo del primero de los nodos para el paso siguiente.

:::warning Guarda la clave pública BLS

Si la red se está ejecutando con BLS (que se hace por defecto), se solicita la clave pública BLS para proponer en el modo PoA y para hacer staking en el modo PoS. Polygon solo guarda la clave privada BLS; es tu responsabilidad preservar la clave pública BLS.

:::

:::warning ¡No compartas tu directorio de datos con nadie!

Los directorios de datos que se generaron anteriormente, además de inicializar los directorios para mantener el estado de la cadena de bloques, también generarán tus claves privadas de validador.
 **Esta clave se debe mantener en secreto, ya que, si te la roban, alguien podría hacerse pasar por el validador de la red.**

:::

## Paso 2: prepara la cadena de conexión multiaddr para el Bootnode {#step-2-prepare-the-multiaddr-connection-string-for-the-bootnode}

Para que un nodo establezca la conectividad de forma satisfactoria, debes saber qué servidor `bootnode`conectar para obtener
 información sobre todos los otros nodos de la red. Al `bootnode` también se lo llama servidor `rendezvous` en la jerga p2p.

`bootnode` no es una instancia especial de un nodo Polygon Edge. Cada nodo Polygon Edge puede funcionar como un `bootnode` y
 cada nodo Polygon Edge necesita tener un conjunto de bootnodes específicos, que se contactarán para proporcionar información sobre cómo conectar con
 todos los otros nodos de la red.

Con el fin de crear la cadena de conexión para especificar el bootnode, es necesario que te ajustes
 al [formato multiaddr](https://docs.libp2p.io/concepts/addressing/):
```
/ip4/<ip_address>/tcp/<port>/p2p/<node_id>
```

En esta guía, trataremos los primeros y segundos nodos como los bootnodes para todos los otros nodos. Lo que sucederá en este escenario
 es que los nodos que se conectan al `node 1` o al `node 2` obtendrán información sobre cómo conectarse unos con otros, a través del nodo que se contactó de forma mutua.

:::info Es necesario que especifiques al menos un bootnode para iniciar un nodo

Se requiere como mínimo **un** bootnode para que los otros nodos de la red puedan descubrirse entre sí. Se recomiendan más bootnodes, ya que
 estos proporcionan resiliencia a la red en caso de interrupciones.
 En esta guía, mencionaremos dos nodos, pero esto se puede cambiar sobre la marcha, sin consecuencias sobre la validez del archivo `genesis.json`.

:::

Como la primera parte de la cadena de conexión multiaddr es la `<ip_address>`, en este punto necesitarás ingresar una dirección IP a la que se pueda llegar a través de otros nodos; según tu configuración puede ser una dirección IP pública o privada, no `127.0.0.1`.

Para el `<port>` utilizaremos `1478`, ya que es el puerto libp2p por defecto.

Y, por último, necesitamos el `<node_id>`, el cual podemos obtener del resultado del comando `polygon-edge secrets init --data-dir data-dir` que se ejecutó anteriormente para generar claves y directorios de datos para el `node 1`)

Después del ensamblaje, la cadena de conexión multiaddr que va al `node 1` que utilizaremos como el bootnode, se verá así (solo el `<node_id>`que está al final debería variar):
```
/ip4/<public_or_private_ip>/tcp/1478/p2p/16Uiu2HAmJxxH1tScDX2rLGSU9exnuvZKNM9SoK3v315azp68DLPW
```
Del mismo modo, construimos multiaddr para el segundo bootnode, como se muestra a continuación
```
/ip4/<public_or_private_ip>/tcp/1478/p2p/16Uiu2HAmS9Nq4QAaEiogE4ieJFUYsoH28magT7wSvJPpfUGBj3Hq
```
:::info Nombres de host DNS en lugar de IP

Polygon Edge es compatible con los nombres de host DNS para la configuración de los nodos. Esta es una función muy útil para las implementaciones basadas en la nube, ya que la IP del nodo puede cambiar por varias razones.

El formato multiaddr para la cadena de conexión al utilizar nombres de host DNS, es el siguiente:`/dns4/sample.hostname.com/tcp/<port>/p2p/nodeid`


:::

## Paso 3: generar el archivo genesis con los 4 nodos como validadores {#step-3-generate-the-genesis-file-with-the-4-nodes-as-validators}

Ese paso se puede ejecutar en tu máquina local, pero deberás tener las claves públicas de validador para cada uno de los 4 validadores.

Los validadores pueden compartir la `Public key (address)` de forma segura, como se muestra a continuación en el resultado de sus comandos `secrets init`, de manera que
 puedes generar sin mayores riesgos el archivo genesis.json con aquellos validadores en el conjunto de validadores inicial, que se identifica por sus claves públicas:

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

* El `--ibft-validator` establece la clave pública del validador que se debe incluir en el conjunto de validadores inicial del bloque genesis. Puede haber muchos validadores iniciales.
* El `--bootnode` establece la dirección del bootnode que habilitará que los nodos se encuentren entre sí
 Utilizaremos la cadena multiaddr del `node 1`, como se mencionó en el **paso 2**, aunque siempre puedes agregar tantos bootnode como desees, tal como se muestra anteriormente.

:::info Saldos de cuentas de preminería

Es probable que quieras configurar tu red de cadena de bloques con algunas direcciones que tengan saldos “preminados”.

Para conseguir eso, pasa tantas banderas `--premine`como desees por cada dirección que quieras que se inicialice con un determinado saldo
 en la cadena de bloques.

Por ejemplo, si nos gustaría preminar 1000 ETH para la dirección `0x3956E90e632AEbBF34DEB49b71c28A83Bc029862` de nuestro bloque genesis, tendríamos que proporcionar el siguiente argumento:

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

Después de especificar lo siguiente:
1. Las claves públicas de los validadores que se incluirán en el bloque genesis como el conjunto de validadores
2. Las cadenas de conexión multiaddr de Bootnode
3. Las cuentas y los saldos preminados que se incluirán en el bloque genesis

y de generar el `genesis.json`, deberías copiarlo a todas las VM de la red. Según tu configuración, puedes
 copiarlo/pegarlo, enviarlo al nodo operador o, simplemente, ejecutarle un comando SCP/FTP de nuevo.

Puedes obtener más información sobre la estructura del archivo genesis en la sección [Comandos CLI](/docs/edge/get-started/cli-commands).

## Paso 4: ejecutar todos los clientes {#step-4-run-all-the-clients}

:::note Establecer conexiones en red en proveedores en la nube

La mayoría de los proveedores no exponen sus direcciones IP (especialmente los públicos) como una interfaz de red directa en su VM, sino que configuran un proxy NAT invisible.


Para permitir que los nodos se conecten entre sí, en este caso, necesitarías escuchar en la dirección IP `0.0.0.0` para enlazar todas las interfaces, pero aún así sería imperativo especificar la dirección IP o la dirección DNS que otros nodos pueden usar para conectarse a tu instancia. Esto se logra ya sea al utilizar el argumento `--nat`o el argumento `--dns`, donde puedes especificar tu IP externa o tu dirección DNS, respectivamente.

#### Ejemplo {#example}

La dirección IP asociada que quieres escuchar es `192.0.2.1`, pero no está vinculada de forma directa a ninguna de tus interfaces de red.

Para permitir que los nodos se conecten, pasarías los siguientes parámetros:

`polygon-edge ... --libp2p 0.0.0.0:10001 --nat 192.0.2.1`

O, si quieres especificar una dirección DNS `dns/example.io`, pasa los siguientes parámetros:

`polygon-edge ... --libp2p 0.0.0.0:10001 --dns dns/example.io`

Esto haría que tu nodo escuche en todas las interfaces, pero también provocaría que se sepa que los clientes se están conectando a él a través de la dirección `--nat`o `--dns` especificada.

:::

Para ejecutar el **primer** cliente:


````bash
node-1> polygon-edge server --data-dir ./data-dir --chain genesis.json  --libp2p 0.0.0.0:1478 --nat <public_or_private_ip> --seal
````

Para ejecutar el **segundo** cliente:

````bash
node-2> polygon-edge server --data-dir ./data-dir --chain genesis.json --libp2p 0.0.0.0:1478 --nat <public_or_private_ip> --seal
````

Para ejecutar el **tercer** cliente:

````bash
node-3> polygon-edge server --data-dir ./data-dir --chain genesis.json --libp2p 0.0.0.0:1478 --nat <public_or_private_ip> --seal
````

Para ejecutar el **cuarto** cliente:

````bash
node-4> polygon-edge server --data-dir ./data-dir --chain genesis.json --libp2p 0.0.0.0:1478 --nat <public_or_private_ip> --seal
````

Después de ejecutar los comandos previos, has configurado una red Polygon Edge de 4 nodos, capaz de sellar bloques y de recuperarse
 de un fallo en el nodo.

:::info Iniciar el cliente mediante el archivo config

En lugar de especificar todos los parámetros de configuración como argumentos CLI, el cliente también se puede iniciar mediante un archivo config, si se ejecuta el siguiente comando:

````bash
polygon-edge server --config <config_file_path>
````
Ejemplo:

````bash
polygon-edge server --config ./test/config-node1.json
````
En la actualidad, solo tenemos compatibilidad con archivos basados en la configuración `json`; el archivo de configuración de ejemplo se puede encontrar [aquí](/docs/edge/configuration/sample-config)

:::

:::info Pasos para ejecutar un nodo no validador

Un no validador siempre se sincronizará con los últimos bloques que haya recibido del nodo validador; puedes iniciar un nodo no validador si ejecutas el siguiente comando:

````bash
polygon-edge server --data-dir <directory_path> --chain <genesis_filename>  --libp2p <IPAddress:PortNo> --nat <public_or_private_ip>
````
Por ejemplo, puedes agregar **el quinto** cliente no validador al ejecutar el siguiente comando:

````bash
polygon-edge server --data-dir ./data-dir --chain genesis.json --libp2p 0.0.0.0:1478 --nat<public_or_private_ip>
````
:::

:::info Especificar el price limit

Un nodo Polygon Edge se puede iniciar con un **prime limit** establecido para las transacciones entrantes.

La unidad para el price limit es `wei`.

Establecer un price limit implica que cualquier transacción que se procese a través del nodo actual necesitará tener un precio del gas **más alto** que el price limit establecido; de lo contrario, no se incluirá en un bloque.

El hecho de que la mayoría de los nodos respeten un determinado price limit genera que se cumpla la regla de que las transacciones en la red
 no pueden estar por debajo de un cierto umbral de precio.

El valor por defecto del price limit es `0`, lo que significa que no se aplica a todo por defecto.

Ejemplo de cómo utilizar la bandera `--price-limit`:
````bash
polygon-edge server --price-limit 100000 ...
````

Vale la pena señalar que los price limit **se cumplen solo sobre transacciones no locales**, lo que significa
 que el price limit no se aplica a transacciones que se añaden al nodo de forma local.

:::

:::info URL WebSocket

Por defecto, cuando ejecutas el Polygon Edge, se genera una URL WebSocket en función de la ubicación de la cadena.
 El esquema URL `wss://`se usa para enlaces HTTPS y el `ws://` para HTTP.

URL WebSocket del localhost
````bash
ws://localhost:10002/ws
````
Ten en cuenta que el número del puerto depende del puerto JSON-RPC elegido para el nodo.

URL WebSocket de Edgenet
````bash
wss://rpc-edgenet.polygon.technology/ws
````
:::