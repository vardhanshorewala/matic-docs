---
id: install-gcp
title: Desplegar nodos de Polygon en Google Cloud
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

En este documento, describiremos cómo desplegar nodos de Polygon en una instancia de VM en Google Cloud

## Requisitos de hardware {#hardware-requirements}

Comprueba los [requisitos de hardware](/docs/maintain/validate/validator-node-system-requirements) mínimos y recomendados en los documentos de Polygon

## Requisitos de software {#software-requirements}

Usa cualquier sistema operativo moderno de Linux Ubuntu o Debian con soporte a largo plazo, es decir, Debian 11, Ubuntu 20.04. Nos centraremos en Ubuntu 20.04 en este manual

## Instancia de despliegue (2 maneras) {#deploy-instance-2-ways}

Puedes usar al menos dos formas de crear una instancia en Google Cloud:

* gcloud cli, local o [Cloud Shell](https://cloud.google.com/shell)
* Consola web

Abordaremos el primero caso en este manual. Comencemos con el despliegue utilizando CLI:
1. Sigue la [sección "Antes de comenzar"](https://cloud.google.com/compute/docs/instances/create-start-instance#before-you-begin) para instalar y configurar la herramienta de línea de comando de gcloud.
Presta atención a la región y zona predeterminadas, elige las más cercanas a ti o a tus clientes. Puedes usar [gcping.com](https://gcping.com) para medir la latencia para elegir la ubicación más cercana.
2. Ajusta las siguientes variables de comando usando tu editor favorito antes de ejecutar, cuando sea necesario
   * `POLYGON_NETWORK` - elige `mainnet` o la red testnet `mumbai` para ejecutar
   * `POLYGON_NODETYPE` - elige `archive`, tipo de nodo `fullnode` para ejecutar
   * `POLYGON_BOOTSTRAP_MODE` - elige bootstrap modo `snapshot` o `from_scratch`
   * `POLYGON_RPC_PORT` - elige el puerto del nodo bor JSON RPC para escuchar, el valor predeterminado es el que se usó en la creación de la instancia VM y en las reglas de firewall
   * `EXTRA_VAR` - elige las sucursales de Bor y Heimdall, usa `network_version=mainnet-v1` con la red `mainnet` y `network_version=testnet-v4` con la red `mumbai`
   * `INSTANCE_NAME` - el nombre de una instancia VM con Polygon que vamos a crear
   * `INSTANCE_TYPE` - [tipo de máquina](https://cloud.google.com/compute/docs/machine-types) GCP, se recomienda el valor predeterminado, puedes cambiarlo más tarde si es necesario
   * `BOR_EXT_DISK_SIZE` - tamaño de disco adicional en GB para usar con Bor, se recomienda el valor predeterminado con `fullnode`, puedes expandirlo más tarde si es necesario. Sin embargo, necesitarás 8192GB+ con el nodo `archive`
   * `HEIMDALL_EXT_DISK_SIZE` - tamaño de disco adicional en GB para usar con Heimdall, se recomienda el valor predeterminado
   * `DISK_TYPE` - [tipo de disco](https://cloud.google.com/compute/docs/disks#disk-types) GCP, SSD es muy recomendable. Es posible que debas aumentar la cuota total de GB de SSD en la región en la que estás poniendo en marcha el nodo

3. Usa el siguiente comando para crear una instancia con los requisitos de hardware y software correctos. En el siguiente ejemplo, desplegamos la `mainnet` de Polygon desde `snapshot` con el modo `fullnode`:
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
La instancia debe crearse durante un par de minutos

## Iniciar sesión en la instancia (opcional) {#login-to-instance-optional}

Tomará un par de minutos instalar todo el software requerido y un par de horas descargar una instantánea cuando se seleccione.
Deberías ver los procesos de `bor` y `heimdalld` en funcionamiento llenando unidades adicionales. Puedes ejecutar los siguientes comandos para comprobarlo.
Conéctate al servicio SSH de la instancia utilizando el envoltorio SSH de `gcloud`:
```bash
gcloud compute ssh ${INSTANCE_NAME}
# inside the connected session
sudo su -

ps uax|egrep "bor|heimdalld"
df -l -h
```
Puedes usar el siguiente comando para observar el progreso de la instalación, es realmente útil en caso de bootstrap de `snapshot`
```bash
# inside the connected session
screen -dr
```
Usa la combinación de teclas `Control+a d` para desconectarte de la revisión del progreso.

Puedes usar los siguientes comandos para obtener los registros de Bor y Heimdall:
```bash
# inside the connected session
journalctl -fu bor
journalctl -fu heimdalld
```
:::note

Los datos de la cadena de bloques se guardan en unidades adicionales que se conservan por defecto al eliminar la instancia de VM. Debes eliminar los discos adicionales manualmente si ya no necesitas estos datos.

:::

Al final, obtendrás una instancia como se muestra en el siguiente diagrama:
<img src={useBaseUrl("img/mainnet/polygon-instance.svg")} />

Si encuentras un problema con este manual, no dudes en abrir un [problema](https://github.com/maticnetwork/matic-docs/issues) o [crear un PR](https://github.com/maticnetwork/matic-docs/pulls) en [GitHub](https://github.com/maticnetwork/matic-docs).
