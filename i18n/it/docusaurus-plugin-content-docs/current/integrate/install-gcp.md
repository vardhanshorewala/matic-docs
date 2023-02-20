---
id: install-gcp
title: Distribuire i nodi di Polygon su Google Cloud
sidebar_label: Google Cloud Deployment
description: Semplice implementazione dei tuoi nodi Polygon su Google Cloud
keywords:
- docs
- polygon
- deploy
- nodes
- gcp
- google cloud
slug: install-gcp
image: https://wiki.polygon.technology/img/polygon-wiki.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

# Distribuire i nodi di Polygon su Google Cloud {#deploy-polygon-nodes-on-google-cloud}

In questo documento descriveremo come distribuire i nodi di Polygon in un'istanza VM su Google Cloud.

### Requisiti hardware {#hardware-requirements}

Controlla i [requisiti hardware](/docs/maintain/validate/validator-node-system-requirements) minimi e consigliati in Polygon Wiki.

### Requisiti software {#software-requirements}

Usa qualsiasi sistema operativo Debian o Ubuntu Linux moderno con supporto a lungo termine, ad esempio Debian 11, Ubuntu 20.04. In questo manuale ci concentreremo su Ubuntu 20.04

## Implementare l'istanza (2 modi) {#deploy-instance-2-ways}

Puoi utilizzare almeno due modi per creare un'istanza su Google Cloud:

* gcloud cli, locale o [Cloud Shell](https://cloud.google.com/shell)
* Console web

In questo manuale tratteremo il primo caso. Iniziamo l'implementazione utilizzando CLI:
1. Segui [la sezione "Prima di iniziare"](https://cloud.google.com/compute/docs/instances/create-start-instance#before-you-begin) per installare e configurare lo strumento da riga di comando gcloud.
Fai attenzione alla regione e all'area predefinita, scegli quelle più vicine a te o ai tuoi clienti. Puoi utilizzare [gcping.com](https://gcping.com) per misurare la latenza e scegliere la posizione più vicina.
2. Prima dell'esecuzione, modifica le seguenti variabili di comando utilizzando il tuo editor preferito, quando richiesto
   * `POLYGON_NETWORK` - scegli la rete testnet `mainnet` o `mumbai` per eseguire
   * `POLYGON_NODETYPE` - scegli `archive`, tipo di nodo `fullnode` per eseguire
   * `POLYGON_BOOTSTRAP_MODE` - scegli la modalità bootstrap `snapshot` o `from_scratch`
   * `POLYGON_RPC_PORT` - scegli la porta del nodo Bor JSON RPC su cui ascoltare, il valore predefinito è quello utilizzato nella creazione dell'istanza VM e nelle regole del firewall
   * `EXTRA_VAR` - scegli i rami Bor e Heimdall, usa `network_version=mainnet-v1` con la rete `mainnet` e `network_version=testnet-v4` con la rete `mumbai`
   * `INSTANCE_NAME` - il nome di un'istanza VM con Polygon che creeremo
   * `INSTANCE_TYPE` - [tipo di macchina](https://cloud.google.com/compute/docs/machine-types) GCP, è consigliato il valore predefinito, se necessario è possibile cambiarlo in seguito
   * `BOR_EXT_DISK_SIZE` - spazio addizionale del disco in GB da usare con Bor, è consigliato il valore predefinito con `fullnode`, se necessario puoi espanderlo in seguito. Avrai comunque bisogno di 8192GB+ con il nodo `archive`
   * `HEIMDALL_EXT_DISK_SIZE` - spazio addizionale del disco in GB da usare con Heimdall, è consigliato il valore predefinito
   * `DISK_TYPE` - [tipo di disco](https://cloud.google.com/compute/docs/disks#disk-types) GCP, è altamente consigliato SSD. Potresti dover aumentare la quota totale di GB SSD nell'area in cui stai avviando il nodo.

3. Usa il seguente comando per creare un'istanza con i giusti requisiti di hardware e software. Nell'esempio che segue implementiamo Polygon `mainnet` da `snapshot` con la modalità `fullnode`:
```bash
   export POLYGON_NETWORK=mainnet
   export POLYGON_NODETYPE=fullnode
   export POLYGON_BOOTSTRAP_MODE=snapshot
   export POLYGON_RPC_PORT=8747
   export GCP_NETWORK_TAG=polygon
   export EXTRA_VAR=(bor_branch=v0.3.3 heimdall_branch=v0.3.0  network_version=mainnet-v1 node_type=sentry/sentry heimdall_network=${POLYGON_NETWORK})
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
L'istanza dovrebbe essere creata in un paio di minuti

## Accedi all'istanza (facoltativo) {#login-to-instance-optional}

Saranno necessari un paio di minuti per installare tutti i software richiesti e un paio d'ore per scaricare uno snapshot una volta scelto. Dovresti visualizzare i processi `bor` e `heimdalld` in esecuzione sulle unità aggiuntive. Puoi eseguire i seguenti comandi per verificarlo.
Connettiti al servizio SSH dell'istanza utilizzando il wrapper SSH `gcloud`:
```bash
gcloud compute ssh ${INSTANCE_NAME}
# inside the connected session
sudo su -

ps uax|egrep "bor|heimdalld"
df -l -h
```
Puoi utilizzare il seguente comando per guardare lo stato di avanzamento dell'installazione, è davvero utile in caso di bootstrap `snapshot`
```bash
# inside the connected session
screen -dr
```
Usa la combinazione di tasti `Control+a d` per disconnetterti dalla revisione dello stato di avanzamento.

Puoi utilizzare i seguenti comandi per ottenere i registri di Bor ed Heimdall:
```bash
# inside the connected session
journalctl -fu bor
journalctl -fu heimdalld
```
:::note
I dati della blockchain vengono salvati su drive aggiuntivi mantenuti di default sulla rimozione dell'istanza VM. Devi rimuovere manualmente i dischi aggiuntivi nel caso tu non abbia più bisogno di questi dati.
:::

Alla fine otterrete un'istanza come mostrato nel diagramma sottostante:<img src={useBaseUrl("img/mainnet/polygon-instance.svg")} />

Se riscontri un problema con questo manuale, crea una [richiesta](https://github.com/maticnetwork/matic-docs/issues) o [ un PR](https://github.com/maticnetwork/matic-docs/pulls) su [GitHub](https://github.com/maticnetwork/matic-docs).
