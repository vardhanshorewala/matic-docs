---
id: setup-bor
title: Configurar Bor (capa de producción de bloques)
description: Desarrolla tu próxima app de cadena de bloques en Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
### Configurar Bor (capa de producción de bloques) {#setup-bor}

Utiliza la rama `master`o la `develop`rama, que contiene la última liberación estable.

    $ mkdir -p $GOPATH/src/github.com/maticnetwork$ cd $ GOPATH/src/github.com/maticnetwork $ git clon https://github.com/maticnetwork/bor cd. bor $ hacer bor-all
Ahora, tienes instalado bor en tu sistema local y el binario está disponible en el camino.`./build/bin/bor`

**Conectarse a la consola (opcional).**

Este es un paso opcional. No necesitas conectarte a una consola. Solo puedes hacerlo si estás interesado en otros detalles.

Al igual que Geth, ¡puedes conectarte a la consola de bor para ejecutar varios tipos de consultas! Desde tu comando `dataDir`ejecutar, el siguiente comando.

**contratos de Génesis**

    $ cd ~/matic/tesnets Ingresa el submódulo $ git. Actualización de submódulo $ git: $ cd ~/matic/tesnets/genesis-contracts Instalar $ npm Ingresa el submódulo $ git. Actualización de submódulo $ git: $ cd ~/matic/tesnets/genesis-contracts/matic-contracts Instalar $ npm $ Los scripts de los nodos de scripts/process-templates.js --bor-chain-id 15001 $npm ejecuta trufa: compile
Una vez que son procesadas las plantillas, necesitamos establecer validadores en `tesnets/genesis-contracts/validators.js`archivo. Este archivo debería tener este aspecto:

    validadores de const = { dirección: "0x6c468CF8c9879006E22EC4029696E005C2319C9D", Participación de apuesta: 10, // sin 10^18 Saldo: 1000 // sin 10^18 } ]
Genera el conjunto validador de Bor utilizando el `validators.js`archivo:

    $ cd ~/matic/testnets/genesis-contracts nodo de $ generate-borvalidatorset.js --bor-chain-id 15001 --heimdall-chain-id heimdall-P5rXwg.
Este comando generará`genesis-contracts/contracts/BorValidatorSet.sol`.

Genera genesis.json, una vez que `BorValidatorSet.sol`se genera:

    $ cd ~/matic/testnets/genesis-contracts nodo de $ generate-genesis.js --bor-chain-id 15001 --heimdall-chain-id heimdall-P5rXwg.
Esto generará`genesis-contracts/genesis.json`

**Iniciar bor**

Una vez que se genera el archivo génesis en`~/matic/tesnets/genesis-contracts/genesis.json`

Prepara el nodo Bor (capa de producción de bloques)

    $ cd ~/matic/testnets/bor-devnet $ bash setup.sh
Inicia el bor utilizando el siguiente comando:

    $ cd ~/matic/testnets/bor-devnet $ bash start.sh 1
Bor funcionará en el 8545.

Si quieres limpiar Bor y volver a empezar:

    $ bash clean.sh $ bash setup.sh $ bash start.sh 1
### Para probar Bor y Heimdall {#to-test-bor-and-heimdall}

Para probar Bor y Heimdall, necesitas ejecutar Bor y Heimdall, el servidor de descanso de Heimdall y el puente, todo en paralelo.

### [Opcional] Ejecuta el servidor de descanso heimdall detrás de un proxy de nginx para el front-end {#run-heimdall-rest-server-behind-nginx-proxy-for-front-end}

Sigue estas instrucciones [https://kirillplatonov.com/2017/11/12/simple_reverse_proxy_on_mac_with_nginx/](https://kirillplatonov.com/2017/11/12/simple_reverse_proxy_on_mac_with_nginx/) para ejecutar nginx en la máquina local (mac osx).

Añade el siguiente contenido `/usr/local/etc/nginx/nginx.conf`y reinicia el nginx:

    worker_processes 1; eventos worker_connections 1024; } http servidor escuchar 80; server_name localhost; ubicación / add_header 'Access-Control-Allow-Origin' * siempre; add_header 'Access-Control-Allow-Credentials': Autorización, autorización, aceptación, origen, DNT, add_header Keep-Alive, agente de usuario, 'Access-Control-Allow-Headers' 'Access-Control-Allow-Headers' control de caché, tipo de contenido, rango de contenido. add_header 'Access-Control-Allow-Methods' POST, OPCIONES, PUBLIQUE, BORRA, PARCH; si ($request_method = 'OPTIONS'): add_header 'Access-Control-Allow-Origin' * siempre; add_header 'Access-Control-Allow-Credentials': Autorización, autorización, aceptación, origen, DNT, add_header Keep-Alive, agente de usuario, 'Access-Control-Allow-Headers' 'Access-Control-Allow-Headers' control de caché, tipo de contenido, rango de contenido. add_header 'Access-Control-Allow-Methods' POST, OPCIONES, PUBLIQUE, BORRA, PARCH; add_header 'Access-Control-Max-Age' 1728000; add_header 'Content-Type': "text/plain charset=UTF-8"; add_header 'Content-Length': 0; regresa 204; proxy_redirect desactivado; $host de proxy_set_header host; proxy_set_header X-real-ip $remote_addr; proxy_set_header X-forward-for $proxy_add_x_forwarded_for; http://127.0.0.1:1317; } }
Vuelve a cargar nginx utilizando los cambios de configuración:

    Sudo nginx -s recarga