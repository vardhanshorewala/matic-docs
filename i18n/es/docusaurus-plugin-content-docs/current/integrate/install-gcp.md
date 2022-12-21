---
id: install-gcp
title: Desplegar nodos Polygon en Google Cloud
sidebar_label: Google Cloud Deployment
description: "Despliegue simple de tus nodos de Polygon en Google Cloud."
keywords:
- docs
- polygon
- gcp
- google cloud
slug: install-gcp
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## Descripción {#description}

En este documento, describiremos cómo desplegar los nodos de Polygon en la instancia de VM de Google Cloud.

## Requisitos de hardware {#hardware-requirements}

Revisa las recomendaciones y los [requisitos mínimos de hardware](/docs/maintain/validate/validator-node-system-requirements) en los documentos de Polygon.

## Requisitos de software {#software-requirements}

Utiliza cualquier SO moderno Debian o Ubuntu Linux con soporte a largo plazo, es decir, Debian 11, Ubuntu 20.04. En este manual, nos centraremos en Ubuntu 20.04.

## Instancia de despliegue (2 maneras) {#deploy-instance-2-ways}

Hay al menos dos maneras para crear una instancia en Google Cloud:

* gcloud cli, local o [Cloud Shell](https://cloud.google.com/shell)
* Consola de web

Revisaremos el primer caso en este manual. Empecemos con el despliegue con CLI:
1. Sigue los pasos en la [sección "Antes de comenzar"](https://cloud.google.com/compute/docs/instances/create-start-instance#before-you-begin) para instalar y configurar la herramienta de línea de comandos de gcloud.
Presta atención en la región y zona por defecto; elige una que tú o tus clientes tengan más cerca. Puedes utilizar [gcping.com](https://gcping.com) para medir la latencia y elegir la ubicación más cercana.
2. Ajusta las siguientes variables de comandos con tu editor favorito antes de ejecutarlo, cuando sea necesario
   * `POLYGON_NETWORK`: elige la red de prueba `mainnet` o `mumbai` para ejecutar
   * `POLYGON_NODETYPE`: elige `archive`, tipo de nodo `fullnode` para ejecutar
   * `POLYGON_BOOTSTRAP_MODE`: elige el modo de arranque `snapshot` o `from_scratch`
   * `POLYGON_RPC_PORT`: elige el puerto del nodo de Bor JSON RPC para escuchar; el valor por defecto es lo que se utiliza en la creación de instancias VM y en las reglas de firewall
   * `EXTRA_VAR`: elige las ramas Bor y Heimdall, utiliza `network_version=mainnet-v1` con la red `mainnet` y `network_version=testnet-v4` con la red `mumbai`
   * `INSTANCE_NAME`: el nombre de una instancia VM con Polygon que vamos a crear
   * `INSTANCE_TYPE`: [tipo de máquina](https://cloud.google.com/compute/docs/machine-types) GCP; se recomienda el valor por defecto. Puedes cambiarlo más tarde si es necesario
   * `BOR_EXT_DISK_SIZE`: tamaño de disco adicional en GB para usar con Bor; `fullnode`se recomienda el valor por defecto con . Puedes ampliarlo más tarde si es necesario. Necesitarás más de 8192 GB con el nodo `archive`
   * `HEIMDALL_EXT_DISK_SIZE`: tamaño de disco adicional en GB para usar con Heimdall. Se recomienda el valor por defecto
   * `DISK_TYPE`: [tipo de disco](https://cloud.google.com/compute/docs/disks#disk-types) GCP. Un SSD es altamente recomendable. Es posible que tengas que aumentar la cuota total de GB del SSD en la región en la que estés ejecutando el nodo.

3. Utiliza el siguiente comando para crear una instancia con los requisitos correctos de hardware y software. En el ejemplo a continuación, desplegamos la `mainnet` de Polygon de `snapshot` con el modo `fullnode`:
```bash
   export POLYGON_NETWORK=mainnet
   export POLYGON_NODETYPE=fullnode
   export POLYGON_BOOTSTRAP_MODE=snapshot
   export POLYGON_RPC_PORT=8747
   export GCP_NETWORK_TAG=polygon
   export EXTRA_VAR=(bor_branch=v0.2.16 heimdall_branch=v0.2.11  network_version=mainnet-v1 node_type=sentry/sentry heimdall_network=${POLYGON_NETWORK})
   gcloud compute firewall-rules create "polygon-p2p" --allow=tcp:26656,tcp:30303,udp:30303 --description="polygon p2p" --target-tags=${GCP_NETWORK_TAG}
   gcloud compute firewall-rules create "polygon-rpc" --allow=tcp:${POLYGON_RPC_PORT} --description="polygon rpc" --target-tags=${GCP_NETWORK_TAG}
   export INSTANCE_NAME=polygon-0
   export INSTANCE_TYPE=e2-standard-8
   export BOR_EXT_DISK_SIZE=1024
   export HEIMDALL_EXT_DISK_SIZE=500
   export DISK_TYPE=pd-ssd
   gcloud compute instances create ${INSTANCE_NAME} \
   --image-project=ubuntu-os-cloud \
   --image-family=ubuntu-2004-lts \
   --boot-disk-size=20 \
   --boot-disk-type=${DISK_TYPE} \
   --machine-type=${INSTANCE_TYPE} \
   --create-disk=name=${INSTANCE_NAME}-bor,size=${BOR_EXT_DISK_SIZE},type=${DISK_TYPE},auto-delete=no \
   --create-disk=name=${INSTANCE_NAME}-heimdall,size=${HEIMDALL_EXT_DISK_SIZE},type=${DISK_TYPE},auto-delete=no \
   --tags=${GCP_NETWORK_TAG} \
   --metadata=user-data='
   #cloud-config

   bootcmd:
   - screen -dmS polygon su -l -c bash -c "curl -L https://raw.githubusercontent.com/maticnetwork/node-ansible/master/install-gcp.sh | bash -s -- -n '${POLYGON_NETWORK}' -m '${POLYGON_NODETYPE}' -s '${POLYGON_BOOTSTRAP_MODE}' -p '${POLYGON_RPC_PORT}' -e \"'${EXTRA_VAR}'\"; bash"'
```
La instancia debería crearse en un par de minutos.

## Iniciar sesión en la instancia (opcional) {#login-to-instance-optional}

Instalar todo el software necesario llevará un par de minutos, y la descarga de Snapshot cuando se elija, un par de horas.
Deberías ver que los procesos de trabajo de `bor` y `heimdalld` llenan los discos adicionales. Puedes ejecutar los siguientes comandos para revisarlo.
Conéctate al servicio de SSH de la instancia con el contenedor de SSH de `gcloud`:
```bash
gcloud compute ssh ${INSTANCE_NAME}
# inside the connected session
sudo su -

ps uax|egrep "bor|heimdalld"
df -l -h
```
Puedes usar el siguiente comando para ver el progreso de la instalación. Es realmente útil en caso de arranque de `snapshot`.
```bash
# inside the connected session
screen -dr
```
Utiliza la combinación de clave `Control+a d` para desconectarte de la revisión de progreso.

Puedes usar los siguientes comandos para obtener los registros de Bor y Heimdall:
```bash
# inside the connected session
journalctl -fu bor
journalctl -fu heimdalld
```
:::note

Los datos de la cadena de bloques se guardan en unidades adicionales que se mantienen por defecto en la eliminación de instancias de VM. Deberás quitar los discos adicionales manualmente si ya no necesitas estos datos.

:::

Al final, tendrás una instancia como la que se muestra en el siguiente diagrama:
<img src={useBaseUrl("img/mainnet/polygon-instance.svg")} />

Si tienes algún inconveniente con este manual, no dudes en [preguntarnos](https://github.com/maticnetwork/matic-docs/issues) o [crear una PR](https://github.com/maticnetwork/matic-docs/pulls) en [GitHub](https://github.com/maticnetwork/matic-docs).
