---
id: setup-bor
title: Configurar Bor
description: Desarrolla tu próxima app de cadena de bloques en Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
### Configurar Bor {#setup-bor}

Utiliza la rama `master`o `develop`, que contiene la última versión estable.

    $ mkdir -p $GOPATH/src/github.com/maticnetwork $ cd $GOPATH/src/github.com/maticnetwork $ git clone https://github.com/maticnetwork/bor
    $ cd bor
     $ make bor-all

Ahora, tienes instalado bor en tu sistema local y el binario está disponible en la ruta `./build/bin/bor`

**Conectarse a la consola (opcional)**

Este es un paso opcional. No necesitas conectarte a una consola. Solo puedes hacerlo si estás interesado en otros detalles.

Al igual que Geth, ¡puedes conectarte a la consola de bor para ejecutar varios tipos de consultas! Desde tu `dataDir` ejecuta el siguiente comando.

**Contratos de génesis**

    $ cd ~/matic/tesnets
     $ git submodule init
     $ git submodule update

     $ cd ~/matic/tesnets/genesis-contracts
     $ npm install

     $ git submodule init
     $ git submodule update
     $ cd ~/matic/tesnets/genesis-contracts/matic-contracts
     $ npm install
     $ node scripts/process-templates.js --bor-chain-id 15001
     $ npm run truffle:compile

Una vez que son procesadas las plantillas, necesitamos establecer validadores en el archivo  `tesnets/genesis-contracts/validators.js`. Este archivo debería tener este aspecto:

    const validators = [
       {
         address: "0x6c468CF8c9879006E22EC4029696E005C2319C9D",
         stake: 10, // without 10^18
         balance: 1000 // without 10^18
       }
     ]

Genera el conjunto validador de Bor utilizando el archivo `validators.js`:

    $ cd ~/matic/testnets/genesis-contracts
     $ node generate-borvalidatorset.js --bor-chain-id 15001 --heimdall-chain-id heimdall-P5rXwg

Este comando generará `genesis-contracts/contracts/BorValidatorSet.sol`.

Genera genesis.json, una vez que `BorValidatorSet.sol` se genera:

    $ cd ~/matic/testnets/genesis-contracts
     $ node generate-genesis.js --bor-chain-id 15001 --heimdall-chain-id heimdall-P5rXwg

Esto generará `genesis-contracts/genesis.json`

**Iniciar bor**

Una vez que se genera el archivo génesis en `~/matic/tesnets/genesis-contracts/genesis.json`

Prepara el nodo Bor:

    $ cd ~/matic/testnets/bor-devnet
     $ bash setup.sh

Inicia el bor utilizando el siguiente comando:

    $ cd ~/matic/testnets/bor-devnet
     $ bash start.sh 1

Bor funcionará en el 8545.

Si quieres limpiar Bor y volver a empezar:

    $ bash clean.sh
     $ bash setup.sh
     $ bash start.sh 1

### Para probar Bor y Heimdall {#to-test-bor-and-heimdall}

Para probar Bor y Heimdall, necesitas ejecutar Bor y Heimdall, el servidor de descanso de Heimdall y el puente, todo en paralelo.

### [Opcional] Ejecuta el servidor rest de heimdall detrás de un proxy de nginx para el front-end {#run-heimdall-rest-server-behind-nginx-proxy-for-front-end}

Sigue estas instrucciones [https://kirillplatonov.com/2017/11/12/simple_reverse_proxy_on_mac_with_nginx/](https://kirillplatonov.com/2017/11/12/simple_reverse_proxy_on_mac_with_nginx/) para ejecutar nginx en la máquina local (mac osx).

Añade el siguiente contenido en `/usr/local/etc/nginx/nginx.conf` y reinicia el nginx:

    worker_processes  1;

    events {
         worker_connections 1024;
     }

     http {
         server {
             listen 80;
            server_name localhost;

             location / {
               add_header 'Access-Control-Allow-Origin' * always;
               add_header 'Access-Control-Allow-Credentials' 'true';
               add_header 'Access-Control-Allow-Headers' 'Authorization,Accept,Origin,DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Content-Range,Range';
               add_header 'Access-Control-Allow-Methods' 'GET,POST,OPTIONS,PUT,DELETE,PATCH';

               if ($request_method = 'OPTIONS') {
                 add_header 'Access-Control-Allow-Origin' * always;
                 add_header 'Access-Control-Allow-Credentials' 'true';
                 add_header 'Access-Control-Allow-Headers' 'Authorization,Accept,Origin,DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type,Content-Range,Range';
                 add_header 'Access-Control-Allow-Methods' 'GET,POST,OPTIONS,PUT,DELETE,PATCH';
                 add_header 'Access-Control-Max-Age' 1728000;
                 add_header 'Content-Type' 'text/plain charset=UTF-8';
                 add_header 'Content-Length' 0;
                return 204;
              }

               proxy_redirect off;
               proxy_set_header host $host;
               proxy_set_header X-real-ip $remote_addr;
               proxy_set_header X-forward-for $proxy_add_x_forwarded_for;
               proxy_pass http://127.0.0.1:1317;
            }
         }
     }

Vuelve a cargar nginx utilizando los cambios de configuración:

    sudo nginx -s reload