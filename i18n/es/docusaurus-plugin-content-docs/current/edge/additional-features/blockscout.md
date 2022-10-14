---
id: blockscout
title: Blockscout
description: Cómo configurar una instancia de Blockscout para trabajar con Polygon Edge.
keywords:
  - docs
  - polygon
  - edge
  - blockscout
  - deploy
  - setup
  - instance
---

## Resumen {#overview}
Esta guía entra en detalles sobre cómo compilar y desplegar la instancia de Blockscout para trabajar con Polygon-Edge. Blockscout tiene su propia [documentación](https://docs.blockscout.com/for-developers/manual-deployment), pero esta guía se enfoca en unas instrucciones simples pero detalladas paso a paso de como configurar la instancia de Blockscout.

## Entorno {#environment}
* Sistema operativo: de servidor Ubuntu 20.04 LTS [descargar enlace](https://releases.ubuntu.com/20.04/) con permisos sudo
* servidor: de Hardware: 8CPU / 16GB de RAM / 50GB de HDD (LVM)
* Servidor de base de datos: Servidor dedicado con 2 CPU / 4GB de RAM / 100GB de SSD / PostgreSQL 13.4

### Servidor DB {#db-server}
El requisito para seguir esta guía es tener un servidor de base datos listo y configurado de un usuario db. Esta guía no entrará en detalles sobre cómo desplegar y configurar el servidor PostgreSQL. Hay muchas guías ahora para hacer esto, por ejemplo [Guía DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-install-postgresql-on-ubuntu-20-04-quickstart)

:::info DESCARGO DE RESPONSABILIDAD
Esta guía está destinada únicamente para ayudarte a poner en marcha Blockscout en una sola instancia que no es la configuración ideal.   
 Para la producción, probablemente querrás introducir proxy inverso, equilibrador de carga, opciones de escalabilidad, etc. en la arquitectura.
:::

# Procedimiento de Despliegue Blockscout {#blockscout-deployment-procedure}

## Parte 1 instalar dependencias {#part-1-install-dependencies}
Antes de iniciar necesitamos asegurarnos de que tengamos todos los binarios instalados en los que es dependiente el blockscout.

### Actualizar y mejorar el sistema {#update-upgrade-system}
```bash
sudo apt -y update && sudo apt -y upgrade
```

### Agregar repositorios erlang {#add-erlang-repos}
```bash
# go to your home dir
cd ~
# download deb
wget https://packages.erlang-solutions.com/erlang-solutions_2.0_all.deb
# download key
wget https://packages.erlang-solutions.com/ubuntu/erlang_solutions.asc
# install repo
sudo dpkg -i erlang-solutions_2.0_all.deb
# install key
sudo apt-key add erlang_solutions.asc
# remove deb
rm erlang-solutions_2.0_all.deb
# remove key
rm erlang_solutions.asc
```

### Agregar repositorios NodeJS {#add-nodejs-repo}
```bash
sudo curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -
```

### Instalar Rust  {#install-rust}
```bash
sudo curl https://sh.rustup.rs -sSf | sh -s -- -y
```

### Instalar la versión requerida de Erlang {#install-required-version-of-erlang}
```bash
sudo apt -y install esl-erlang=1:24.*
```

### Instalar la versión requerida de Elixir {#install-required-version-of-elixir}
La versión de Elixir debe ser     . Si intentamos e instalamos esta versión desde el repositorio oficial,  se actualizará a `Erlang/OTP 25`y no queremos eso.
 Debido a esto, necesitamos instalar el precompilado específico `elixir`de la página de versiones de GitHub.

```bash
cd ~
mkdir /usr/local/elixir
wget https://github.com/elixir-lang/elixir/releases/download/v1.13.4/Precompiled.zip
sudo unzip -d /usr/local/elixir/ Precompiled.zip
rm Precompiled.zip
```

Ahora tenemos que configurar correctamente `exlixir`el sistema binario.
```bash
sudo ln -s /usr/local/elixir/bin/elixir /usr/local/bin/elixir
sudo ln -s /usr/local/elixir/bin/mix /usr/local/bin/mix
sudo ln -s /usr/local/elixir/bin/iex /usr/local/bin/iex
sudo ln -s /usr/local/elixir/bin/elixirc /usr/local/bin/elixirc
```

Revisar si `elixir`y `erlang`se instalan correctamente ejecutando`elixir -v`.
 Este debe ser el resultado:
```bash
Erlang/OTP 24 [erts-12.3.1] [source] [64-bit] [smp:8:8] [ds:8:8:10] [async-threads:1] [jit]

Elixir 1.13.4 (compiled with Erlang/OTP 22)
```

:::warning

     debe ser la versión y `Elixir`debe ser la versión `1.13.*`
 Si ese no es el caso, tendrá problemas para compilar Blockscout y/o ejecutarlo.
:::   
:::info

Revisa la página oficial ***[de requisitos de Blockscout](https://docs.blockscout.com/for-developers/information-and-settings/requirements)***

:::

### Instala NodeJS {#install-nodejs}
```bash
sudo apt -y install nodejs
```

### Instala la carga {#install-cargo}
```bash
sudo apt -y install cargo
```

### Instala otras dependencias {#install-other-dependencies}
```bash
sudo apt -y install automake libtool inotify-tools gcc libgmp-dev make g++ git
```

### Opcionalmente instala cliente postgresql para revisar tu conexión db {#optionally-install-postgresql-client-to-check-your-db-connection}
```bash
sudo apt install -y postgresql-client
```

## Parte 2 establece variables de entorno {#part-2-set-environment-variables}
Necesitamos establecer las variables de entorno, antes de comenzar con la compilación de Blockscout. En esta guía estableceremos solo el mínimo básico para hacer que funcione. Lista completa de variables que puedes establecer, puedes encontrar [aquí](https://docs.blockscout.com/for-developers/information-and-settings/env-variables)

### Establece la conexión de la base de datos como variable de entorno {#set-database-connection-as-environment-variable}
```bash
# postgresql connection example:  DATABASE_URL=postgresql://blockscout:Passw0Rd@db.instance.local:5432/blockscout
export DATABASE_URL=postgresql://<db_user>:<db_pass>@<db_host>:<db_port>/<db_name> # db_name does not have to be existing database

# we set these env vars to test the db connection with psql
export PGPASSWORD=Passw0Rd
export PGUSER=blockscout
export PGHOST=db.instance.local
export PGDATABASE=postgres # on AWS RDS postgres database is always created
```

Ahora prueba tu conexión DB con los parámetros proporcionados. Dado que proporcionó PG env vars, debería poder conectarse a la base de datos solo ejecutando:
```bash
psql
```

Si la base de datos está configurada correctamente, deberías ver un aviso de psql:
```bash
psql (12.9 (Ubuntu 12.9-0ubuntu0.20.04.1))
SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA384, bits: 256, compression: off)
Type "help" for help.

blockscout=>
```

De lo contrario, podrías ver un error como este:
```bash
psql: error: FATAL:  password authentication failed for user "blockscout"
FATAL:  password authentication failed for user "blockscout"
```
Si este es el caso [estos documentos](https://ubuntu.com/server/docs/databases-postgresql) podría ayudarte.

:::info Una conexión DB
Asegúrate de haber ordenado todos los problemas de conexión db antes de proceder a la siguiente parte. Tendrás que proporcionar privilegios de super usuario para el usuario de blockscout.
:::
```bash
postgres@ubuntu:~$ createuser --interactive
Enter name of role to add: blockscout
Shall the new role be a superuser? (y/n) y
```

## Parte 3 Clonar y compilar Blockscout {#part-3-clone-and-compile-blockscout}
Ahora finalmente llegamos a iniciar la instalación de Blockscout.

### Clona el repositorio de Blockscout {#clone-blockscout-repo}
```bash
cd ~
git clone https://github.com/Trapesys/blockscout
```

### Genera una base de clave secreta para proteger  {#generate-secret-key-base-to-protect-production-build}
```bash
cd blockscout
mix deps.get
mix local.rebar --force
mix phx.gen.secret
```
En la última línea, debería ver una larga cadena de caracteres aleatorios.     
 Esto debe establecerse como tu      variable de entorno antes del siguiente paso.
 Por ejemplo:
```bash
export SECRET_KEY_BASE="912X3UlQ9p9yFEBD0JU+g27v43HLAYl38nQzJGvnQsir2pMlcGYtSeRY0sSdLkV/"
```

### Establece el modo de producción {#set-production-mode}
```bash
export MIX_ENV=prod
```

### Compilar {#compile}
Cd dentro de un directorio de clon e inicia la compilación

```bash
cd blockcout
mix local.hex --force
mix do deps.get, local.rebar --force, deps.compile, compile
```

:::info

Si has implementado anteriormente, elimina los activos estáticos de la compilación anterior ***mezcla phx.digest.clean***.

:::

### Migra las bases de datos {#migrate-databases}
:::info
Esta parte fallará si no configuraste tu conexión DB correctamente, no proporcionaste, o has definido los parámetros incorrectos en la variable de entorno de DATABASE_URL. El usuario de la base de datos necesita tener privilegios de super usuario.
:::
```bash
mix do ecto.create, ecto.migrate
```

Si primero necesitas soltar la base de datos, ejecuta
```bash
mix do ecto.drop, ecto.create, ecto.migrate
```

### Instala las dependencias npm y compila los activos de la interfaz {#install-npm-dependencies-and-compile-frontend-assets}
Necesitas cambiar el directorio a la carpeta que contiene los activos de la interfaz

```bash
cd apps/block_scout_web/assets
sudo npm install
sudo node_modules/webpack/bin/webpack.js --mode production
```

:::info Sé paciente
La compilación de estos activos puede tomar unos minutos, y no mostrará ninguna salida. Puede parecer como que el proceso está atascado, pero solo sé paciente. Cuando finaliza el proceso de compilación, debería generar algo como: `webpack 5.69.1 compiled with 3 warnings in 104942 ms`

:::

### Construye los activos estáticos {#build-static-assets}
Para este paso necesitas regresar a la raíz de tu carpeta de clon de Blockscout.
```bash
cd ~/blockscout
sudo mix phx.digest
```

### Genera los certificados auto asignados {#generate-self-signed-certificates}
:::info

Puedes omitir este paso si no utilizas`https`.

:::
```bash
cd apps/block_scout_web
mix phx.gen.cert blockscout blockscout.local
```

## Parte 4 crear y ejecutar el servicio de Blockscout {#part-4-create-and-run-blockscout-service}
En esta parte necesitamos configurar un servicio del sistema, ya que queremos ejecutar Blockscout en el fondo y persistir después de reiniciar el sistema

### Crea un archivo de servicio {#create-service-file}
```bash
sudo touch /etc/systemd/system/explorer.service
```

### Edita un archivo de servicio {#edit-service-file}
Utiliza tu editor de texto favorito para editar este archivo y configurar el servicio
```bash
sudo vi /etc/systemd/system/explorer.service
```
El contenido del archivo explorer.service debería verse así:
```bash
[Unit]
Description=Blockscout Server
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
RestartSec=1
User=root
StandardOutput=syslog
StandardError=syslog
WorkingDirectory=/usr/local/blockscout
ExecStart=/usr/local/bin/mix phx.server
EnvironmentFile=/usr/local/blockscout/env_vars.env

[Install]
WantedBy=multi-user.target
```

### Habilita el servicio de inicio en el boot del sistema {#enable-starting-service-on-system-boot}
```bash
sudo systemctl daemon-reload
sudo systemctl enable explorer.service
```

### Mover tu carpeta de clon de Blockscout a la ubicación de todo el sistema {#move-your-blockscout-clone-folder-to-system-wide-location}
El servicio de Blockscout necesita tener acceso a la carpeta que has clonado del repositorio de Blockscout y compilado todos los activos.
```bash
sudo mv ~/blockscout /usr/local
```

### Crea un archivo env vars que será utilizado por el servicio de Blockscout {#create-env-vars-file-which-will-be-used-by-blockscout-service}

```bash
sudo touch /usr/local/blockscout/env_vars.env
# use your favorite text editor
sudo vi /usr/local/blockscout/env_vars.env

# env_vars.env file should hold these values ( adjusted for your environment )
ETHEREUM_JSONRPC_HTTP_URL="localhost:8545"  # json-rpc API of the chain
ETHEREUM_JSONRPC_TRACE_URL="localhost:8545" # same as json-rpc API
DATABASE_URL='postgresql://blockscout:Passw0Rd@db.instance.local:5432/blockscout' # database connection from Step 2
SECRET_KEY_BASE="912X3UlQ9p9yFEBD0JU+g27v43HLAYl38nQzJGvnQsir2pMlcGYtSeRY0sSdLkV/" # secret key base
ETHEREUM_JSONRPC_WS_URL="ws://localhost:8545/ws" # websocket API of the chain
CHAIN_ID=93201 # chain id
HEART_COMMAND="systemctl restart explorer" # command used by blockscout to restart it self in case of failure
SUBNETWORK="Supertestnet POA" # this will be in html title
LOGO="/images/polygon_edge_logo.svg" # logo location
LOGO_FOOTER="/images/polygon_edge_logo.svg" # footer logo location
COIN="EDGE" # coin
COIN_NAME="EDGE Coin" # name of the coin
INDEXER_DISABLE_BLOCK_REWARD_FETCHER="true" # disable block reward indexer as Polygon Edge doesn't support tracing
INDEXER_DISABLE_PENDING_TRANSACTIONS_FETCHER="true" # disable pending transactions indexer as Polygon Edge doesn't support tracing
INDEXER_DISABLE_INTERNAL_TRANSACTIONS_FETCHER="true" # disable internal transactions indexer as Polygon Edge doesn't support tracing
MIX_ENV="prod" # run in production mode
BLOCKSCOUT_PROTOCOL="http" # protocol to run blockscout web service on
PORT=4000 # port to run blockscout service on
DISABLE_EXCHANGE_RATES="true" # disable fetching of exchange rates
POOL_SIZE=200 # the number of database connections
POOL_SIZE_API=300 # the number of read-only database connections
ECTO_USE_SSL="false" # if protocol is set to http this should be false
HEART_BEAT_TIMEOUT=60 # run HEARTH_COMMAND if heartbeat missing for this amount of seconds
INDEXER_MEMORY_LIMIT="10Gb" # soft memory limit for indexer - depending on the size of the chain and the amount of RAM the server has
FETCH_REWARDS_WAY="manual" # disable trace_block query
INDEXER_EMPTY_BLOCKS_SANITIZER_BATCH_SIZE=1000 # sanitize empty block in this batch size
```
:::info

Utiliza `SECRET_KEY_BASE`que generaste en la Parte 3.

:::Guarda el archivo y salte.

### Finalmente, inicia el servicio de Blockscout {#finally-start-blockscout-service}
```bash
sudo systemctl start explorer.service
```

## Parte 5 prueba la funcionalidad de tu instancia de Blockscout {#part-5-test-out-the-functionality-of-your-blockscout-instance}
Ahora todo lo que queda por hacer es revisar si se está ejecutando el servicio de Blockscout. Revisa el estado del servicio con:
```bash
sudo systemctl status explorer.service
```

Revisar la salida de servicio:
```bash
sudo journalctl -u explorer.service -f
```

Puedes revisar hay algunos nuevos puertos de escucha:
```bash
# if netstat is not installed
sudo apt install net-tools
sudo netstat -tulpn
```

Debes obtener una lista de puertos de escucha y en la lista debería haber algo como esto:
```
tcp        0      0 0.0.0.0:5432            0.0.0.0:*               LISTEN      28142/postgres
tcp        0      0 0.0.0.0:4000            0.0.0.0:*               LISTEN      42148/beam.smp
```

El servicio web de Blockscout ejecuta el puerto y el protocolo definidos en el archivo env. En este ejemplo se ejecuta en    (http).
 Si todo está bien, podrás accesar al portal web de Blockscout con`http://<host_ip>:4000`.

## Consideraciones {#considerations}
Para obtener el mejor rendimiento, es aconsejable tener un dedicado/local     nodo no validador de archivo completo
 que se utilizará exclusivamente para consultas de Blockscout.
 La`json-rpc` API de este nodo no necesita ser expuesta públicamente, ya que Blockscout ejecuta todas las consultas desde la interfaz.


## Pensamientos finales {#final-thoughts}
Acabamos de desplegar una única instancia de Blockscout, que funciona bien, pero para la producción deberías considerar colocar esta instancia detrás de un proxy inverso Nginx. También deberías pensar en la escalabilidad de la base de datos y de la instancia, dependiendo de tu caso de uso.

Definitivamente debería revisar la [documentación oficial Blockscout](https://docs.blockscout.com/) porque hay muchas opciones de personalización.