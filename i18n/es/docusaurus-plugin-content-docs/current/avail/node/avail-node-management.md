---
id: avail-node-management
title: Cómo ejecutar un nodo Avail
sidebar_label: Run an Avail node
description: "Aprende a ejecutar un nodo Avail."
keywords:
  - docs
  - polygon
  - avail
  - node
image: https://matic.network/banners/matic-network-16x9.png
slug: avail-node-management
---
import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';
import useBaseUrl from '@docusaurus/useBaseUrl';

:::tip Práctica común

Los usuarios suelen ejecutar nodos en un servidor en la nube. Es posible que consideres usar un proveedor de VPS para ejecutar un nodo.

:::

## Requisitos previos {#prerequisites}

La siguiente lista de hardware estándar es una recomendación de especificaciones de hardware que tu entorno debería
 tener.

<Tabs
defaultValue="non-val"
values={[
{ label: 'Run Avail Locally', value: 'non-val', },
{ label: 'Run a Validator Node', value: 'val', },
]
}>

<TabItem value="non-val">

Las especificaciones de hardware indican que deberías contar con los siguientes requisitos mínimos:

* 4 GB de RAM
* CPU de 2 núcleos
* SSD de 20-40 GB

</TabItem>
<TabItem value="val">

Las recomendaciones de hardware para ejecutar un validador en una cadena basada en Substrate son las siguientes:

* CPU: Intel(R) Core(TM) i7-7700K CPU a 4,20 GHz
* Almacenamiento: una unidad de estado sólido NVMe de aproximadamente 256 GB. Debe tener el tamaño razonable para afrontar
 el crecimiento de la cadena de bloques.
* Memoria: ECC de 64 GB

</TabItem>
</Tabs>

### Requisitos previos para el nodo: instalar Rust y dependencias {#node-prerequisites-install-rust-dependencies}

:::info Pasos de instalación de acuerdo con Substrate

Avail es una cadena basada en Substrate y requiere la misma configuración para ejecutar una cadena de Substrate.

Puedes obtener más documentación sobre la instalación en Documentación
 **[sobre cómo empezar de Substrate](https://docs.substrate.io/v3/getting-started/installation/)**

:::

Una vez que elijas un entorno para ejecutar tu nodo, asegúrate de tener Rust instalado.
 Si ya instalaste Rust, ejecuta el siguiente comando para asegurarte de estar usando la versión más reciente.

```sh
rustup update
```

Si no es así, comienza por ejecutar el siguiente comando para obtener la versión más reciente de Rust:

```sh
curl https://sh.rustup.rs -sSf | sh -s -- -y
```

Para configurar tu shell, ejecuta lo siguiente:

```sh
source $HOME/.cargo/env
```

Para verificar tu instalación, consulta:

```sh
rustc --version
```

<Tabs
defaultValue="node"
values={[
{ label: 'Run a Local Node', value: 'node', },
{ label: 'Run a Validator Node', value: 'deploy', },
]
}>

<TabItem value="node">

## Cómo ejecutar Avail en forma local {#run-avail-locally}

Clona el [código fuente de Avail](https://github.com/maticnetwork/avail):

```sh
git clone git@github.com:maticnetwork/avail.git
```

Compila el código fuente:

```sh
cargo build --release
```

:::caution Este proceso suele llevar un tiempo

:::

Ejecuta un nodo de desarrollo local con un almacén de datos temporal:

```sh
./target/release/data-avail --dev --tmp
```

</TabItem>
<TabItem value="deploy">

## Implementaciones de disponibilidad de datos {#data-availability-deployments}

:::info Incorporación de validadores

En el estado actual de Avail, el equipo de Avail mantendrá la red y ejecutará
 validadores internos.

:::

:::warning Administración del sistema

Si bien Avail de Polygon está en una fase de red de prueba, en general, los usuarios cuentan con **gran experiencia en administración
 de sistemas** para ejecutar nodos validadores.

Los nodos validadores son responsables de mantener y asegurar la red, para ello, hacen staking de tokens por un valor
 real. Los validadores deben comprender cómo administrar su nodo, su hardware y configuración asociados,
 y tener cuidado, ya que están sujetos a recortes debido a acciones como estar fuera de línea o equivocaciones.

En caso de duda, comunícate con el Equipo de interacción con validadores.

:::

<Tabs
defaultValue="validator"
values={[
{ label: 'Avail Validator Setup', value: 'validator', },
{ label: 'Build Data Availability', value: 'build', },
{ label: 'Build and Run Light Client with Data Availability', value: 'light', },
]
}>

<TabItem value="validator">

## Configuración de Docker {#docker-setup}

La forma más fácil de desplegar tu nodo validador de Avail es por medio de Docker.

### Ejecuta la versión más reciente del contenedor Docker {#run-the-latest-version-of-the-docker-container}

Usa los parámetros por defecto y expone el puerto P2P con `-p 30333` mediante la siguiente ejecución:

```shell
docker run -p 30333 --name my_val 0xpolygon/avail:latest
```

Cualquier parámetro adicional se agregará al binario `data-avail` como argumento.
 Si quieres usar una clave de nodo específica y limitar la cantidad máxima de conexiones entrantes
 a `10`, puedes usar lo siguiente:

```shell
docker run -p 30333 --name my_val 0xpolygon/avail:latest --in-peers=10 --node-key 80027666cebec66464611eb0d5c36416213d83a9c689006a80efcf479826de7d
```

Esta imagen utiliza dos volúmenes:
  - `/da/state` para guardar la base de datos de la cadena
  - `/da/keystore` para guardar las claves privadas del validador

Lo más probable es que quieras vincular estos volúmenes a un punto específico, por ejemplo:

```shell
docker run -p 30333 --name my_val -v /volumes/da/state:/da/state -v /volumes/da/keystore/:/da/keystore 0xpolygon/avail:latest
```

### Cómo introducir claves privadas {#insert-private-keys}

El validador utilizará estas claves privadas para firmar bloques y finalizar la cadena cuando
 actúa como validador activo. Se almacenan en `/da/keystore`en formato de texto simple, de manera que
 debes tener sumo cuidado con respecto a ese volumen.

Para introducir esas claves, abriremos una shell dentro del contenedor en ejecución:

```shell
docker exec -it my_val bash
root@5f55e51e5a85:/da# /da/bin/data-avail key insert \
      --chain=/da/genesis/testnet.chain.spec.raw.json \
      --base-path=/da/state/ \
      --keystore-path=/da/keystore/ \
      --suri=0x7d98...cae6 \
      --key-type=babe \
      --scheme=Sr25519
```

El parámetro **--suri** es la clave privada a modo de frase mnemotécnica (o secreta) con la cual puedes generar
 una mediante la herramienta `subkey` en Substrate.

:::note Obtén información sobre la subclave

Si deseas conocer cómo usar una subclave, ingresa en la
 [Documentación acerca de subclaves de Substrate](https://docs.substrate.io/v3/tools/subkey/).

:::

Se debe repetir este comando **para cada par de tipos de clave
 y esquema** que se muestran en la siguiente tabla:

| Tipo de clave | Esquema |
| -------- | --------- |
| babe | Sr25519 |
| gran | *Ed25519* |
| imon | Sr25519 |
| audi | Sr25519 |

## Unir tokens de AVL {#bond-avl-tokens}

Se recomienda encarecidamente que configures una cuenta de Stash y una controladora y que tengas claves separadas
 (dos cuentas independientes) para ambas.

:::info Claves de Stash y de controladora

-
-



:::



:::tip





:::



 -
 -



*
*
*

:::note



:::

*

<img src={useBaseUrl("img/avail/dev-ext.png")} width="100%" height="100%"/>



<img src={useBaseUrl("img/avail/add_validator_bound_step.png")} width="100%" height="100%"/>



<img src={useBaseUrl("img/avail/bond-avl-val.png")} width="100%" height="100%"/>

##  {#set-session-keys}



###  {#rotate-you-session-keys}



```shell
docker exec -it my_val bash
root@5f55e51e5a85:/da# curl \
      -H "Content-Type: application/json" \
      -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' \
      http://localhost:9933
```





###  {#transaction}





<img src={useBaseUrl("img/avail/set-session-keys.png")} width="100%" height="100%"/>



##  {#validate}



</TabItem>
<TabItem value ="build">

##  {#build-from-the-source-code}



```shell
git clone git@github.com:maticnetwork/avail.git
```



```shell
cargo build --release -p data-avail
```

###  {#optional-how-to-generate-deterministic-wasm}

:::note


:::



1.

2.

```shell
srtool build -r runtime/ --package da-runtime
```



```shell
Found 1.57.0, we will be using paritytech/srtool:1.57.0 for the build
🧰 Substrate Runtime Toolbox - srtool v0.9.19 🧰
        - by Chevdor -
info: using existing install for '1.57.0-x86_64-unknown-linux-gnu'
info: override toolchain for '/build' set to '1.57.0-x86_64-unknown-linux-gnu'

1.57.0-x86_64-unknown-linux-gnu unchanged - rustc 1.57.0 (f1edd0429 2021-11-29)

🏗  Building node-template-runtime as release using rustc 1.57.0 (f1edd0429 2021-11-29)
⏳ That can take a little while, be patient... subsequent builds will be faster.
 Since you have to wait a little, you may want to learn more about Substrate runtimes:
 https://docs.substrate.io/v3/getting-started/architecture/
   Updating git repository `https://github.com/maticnetwork/plonk.git`
   Updating crates.io index
Downloading crates ...
  Downloaded addr2line v0.17.0
  Downloaded void v1.0.2
  ...

  Compiling pallet-staking v3.0.0 (/build/frame/staking)
  Compiling pallet-babe v3.0.0 (/build/frame/babe)
    Finished release [optimized] target(s) in 5m 31s

✨ Your Substrate WASM Runtime is ready! ✨
Summary generated with srtool v0.9.19 using the docker image paritytech/srtool:1.57.0:
Package     : node-template-runtime v2.0.0
GIT commit  : 0c920993026117aa83c905bfcbe881a71ae3e8a3
GIT tag     : v3.0.0
GIT branch  : da-poc-upgrade-3.0
Rustc       : rustc 1.57.0 (f1edd0429 2021-11-29)
Time        : 2022-01-18T15:55:30Z

== Compact
Version     : node-template-1 (node-template-1.tx1.au10)
Metadata    : V12
Size        : 1.75 MB (1832581 bytes)
Proposal    : 0xb1b534eb700006140cc980c89c1f3a9ad7a5ababa3e2aa8b9a17c5ae71d9b61c
IPFS        : QmanwTMjMhWL8uL974VzrA6XVUg17x7czYqEftop6dhkP2
BLAKE2_256  : 0xa1f8434cba25d4bee440d61b9ce6eeaa0d948ff2173187d940e8c3d87086737c
Wasm        : ./bin/node-template/runtime//target/srtool/release/wbuild/node-template-runtime/node_template_runtime.compact.wasm

== Compressed
No compressed runtime found
```



</TabItem>
<TabItem value='light'>

##



```shell
export DOCKER_BUILDKIT = 1
docker build --ssh default -t client:asdr --build-arg BRANCH=feature/app-specific-data-retrieval_2 -f images/client/Dockerfile images/client/
```



```shell
docker-compose -f docker-compose.light-client.yml up
```

###  {#using-monk-templates}

####  {#testnet-using-three-validators}



####  {#step-1-build-images}

```shell
export DOCKER_BUILDKIT=1
docker build -t da:ava-33  --build-arg BRANCH=miguel/ava-33-create-monk-template-for-da-testnet -f images/da/Dockerfile images/da/    
```

####  {#step-2-load-monk-templates}



-
-

```shell
monk s ns-delete /templates/local/polygon
monk load monk/polygon-da-base.matic.today.yaml
monk load monk/polygon-da-devnet.matic.today.yaml
```

####  {#step-3-run-templates}



```shell
monk run polygon/da-dev-validator-1 polygon/da-dev-validator-2 polygon/da-dev-validator-3
```



```shell
monk logs -f -l 100 polygon/da-dev-validator-1
```



```
2022-03-22 10:52:20 ✨ Imported #9 (0x911b…bdf5)    
2022-03-22 10:52:23 💤 Idle (2 peers), best: #9 (0x911b…bdf5), finalized #7 (0x6309…0366), ⬇ 1.5kiB/s ⬆ 1.8kiB/s    
2022-03-22 10:52:28 💤 Idle (2 peers), best: #9 (0x911b…bdf5), finalized #7 (0x6309…0366), ⬇ 1.2kiB/s ⬆ 1.2kiB/s    
2022-03-22 10:52:33 💤 Idle (2 peers), best: #9 (0x911b…bdf5), finalized #7 (0x6309…0366), ⬇ 1.2kiB/s ⬆ 1.2kiB/s    
2022-03-22 10:52:38 💤 Idle (2 peers), best: #9 (0x911b…bdf5), finalized #7 (0x6309…0366), ⬇ 1.1kiB/s ⬆ 1.1kiB/s    
2022-03-22 10:52:40 Rows: 1 Cols: 4 Size: 128    
2022-03-22 10:52:40 Time to extend block 150.509µs    
2022-03-22 10:52:40 Time to prepare 181.938µs    
2022-03-22 10:52:40 Number of CPU cores: 16    
2022-03-22 10:52:40 Time to build a commitment 1.766672ms    
2022-03-22 10:52:40 ✨ Imported #10 (0x64f4…84b5)    
2022-03-22 10:52:43 💤 Idle (2 peers), best: #10 (0x64f4…84b5), finalized #8 (0x3c88…cfe1), ⬇ 1.6kiB/s ⬆ 1.6kiB/s    
2022-03-22 10:52:48 💤 Idle (2 peers), best: #10 (0x64f4…84b5), finalized #8 (0x3c88…cfe1), ⬇ 1.1kiB/s ⬆ 1.1kiB/s    
2022-03-22 10:52:53 💤 Idle (2 peers), best: #10 (0x64f4…84b5), finalized #8 (0x3c88…cfe1), ⬇ 1.2kiB/s ⬆ 1.2kiB/s    
2022-03-22 10:52:58 💤 Idle (2 peers), best: #10 (0x64f4…84b5), finalized #8 (0x3c88…cfe1), ⬇ 1.2kiB/s ⬆ 1.2kiB/s    
2022-03-22 10:53:00 Rows: 1 Cols: 4 Size: 128    
2022-03-22 10:53:00 Time to extend block 146.593µs    
2022-03-22 10:53:00 Time to prepare 175.756µs    
2022-03-22 10:53:00 Number of CPU cores: 16    
2022-03-22 10:53:00 Time to build a commitment 1.891133ms    
2022-03-22 10:53:00 ✨ Imported #11 (0x0a5e…43d6)
```

####  {#purge-node-state}



```
monk purge polygon/da-dev-validator-1 polygon/da-dev-validator-2 polygon/da-dev-validator-3
```

</TabItem>
</Tabs>
</TabItem>
</Tabs>
