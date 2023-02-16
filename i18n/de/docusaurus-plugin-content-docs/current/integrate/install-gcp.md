---
id: install-gcp
title: Bereitstellen von Polygon-Knoten in Google Cloud
sidebar_label: Google Cloud Deployment
description: Einfache Bereitstellung Ihrer Polygon-Knoten in der Google Cloud
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

# Bereitstellung von Polygon Knoten in Google Cloud {#deploy-polygon-nodes-on-google-cloud}

In diesem Dokument beschreiben wir, wie Polygon-Knoten in einer VM-Instanz auf Google Cloud bereitgestellt werden.

### Hardware-Anforderungen {#hardware-requirements}

Überprüfe die Mindestanforderungen und empfohlenen [Hardware](/docs/maintain/validate/validator-node-system-requirements) in Polygon Wiki.

### Software-Anforderungen {#software-requirements}

Verwenden Sie jedes moderne Debian- oder Ubuntu mit langfristiger Unterstützung, d. h. Debian 11, Ubuntu 20.04. Wir werden uns in dieser Bedienungsanleitung auf Ubuntu 20.04 konzentrieren

## Instanz bereitstellen (2 Wege) {#deploy-instance-2-ways}

Sie können mindestens zwei Möglichkeiten nutzen, um eine Instanz in der Google Cloud zu erstellen:

* gcloud cli, lokale oder [Cloud Shell](https://cloud.google.com/shell)
* Web-Konsole

Wir behandeln in dieser Bedienungsanleitung den ersten Fall. Beginnen wir mit der Bereitstellung über CLI:
1. Folgen Sie [der Rubrik "Bevor Sie beginnen"](https://cloud.google.com/compute/docs/instances/create-start-instance#before-you-begin), um das Befehlszeilen-Tool von gcloud zu installieren und zu konfigurieren. Achten Sie auf die Standardregion und -zone, wählen Sie diejenigen, die näher bei Ihnen oder Ihren Kunden liegen. Sie können mit [gcping.com](https://gcping.com) die Latenz messen, um den nächstgelegenen Standort zu wählen.
2. Passen Sie die folgenden Befehlsvariablen mithilfe Ihres bevorzugten Editors vor der Ausführung an, wenn dies erforderlich ist
   * `POLYGON_NETWORK`- Wählen Sie o`mainnet`der das au`mumbai`szuführende Testnet
   * `POLYGON_NODETYPE`- Wählen Sie`archive` den auszuführenden `fullnode`Knotentyp
   * `POLYGON_BOOTSTRAP_MODE`- Wählen Sie den Bootstrap Modus o`snapshot`der`from_scratch`
   * `POLYGON_RPC_PORT`- Wählen Sie JSON RPC bor Knotenanschluss zum Abhören; der Standardwert wird bei der Erstellung der VM-Instanz und in den Firewall-Regeln verwendet.
   * `EXTRA_VAR``network_version=testnet-v4`- Bor- und Heimdall-Abzweigungen auswählen, m`network_version=mainnet-v1`it N`mainnet`etzwerk und N`mumbai`etzwerk verwenden
   * `INSTANCE_NAME`- den Namen einer VM-Instanz mit Polygon, die wir erstellen werden.
   * `INSTANCE_TYPE`- GCP [Rechnertyp](https://cloud.google.com/compute/docs/machine-types), es wird der Standardwert empfohlen, Sie können diesen bei Bedarf später ändern.
   * `BOR_EXT_DISK_SIZE`- Zusätzliche Festplattengröße in GB, die mit Bor verwendet werden soll, Standardwert mit `fullnode`wird empfohlen, Sie können diesen bei Bedarf erweitern. Sie brauchen jedoch 8192GB+ mit `archive`
   * `HEIMDALL_EXT_DISK_SIZE`- einer zusätzlichen Festplattengröße in GB, die mit Heimdall verwendet werden soll, es wird der Standardwert empfohlen
   * `DISK_TYPE`- GCP [Festplattentyp](https://cloud.google.com/compute/docs/disks#disk-types), SSD wird nachdrücklich empfohlen. Möglicherweise müssen Sie das Gesamt-SSD-GB-Kontingent in der Region, in der Sie den Knoten einrichten, erhöhen.

3. Mit dem folgenden Befehl können Sie eine Instanz mit korrekten Hardware- und Softwareanforderungen erstellen. Im folgenden Beispiel setzen wir Polygon a`mainnet`us mi`snapshot`t dem Mo`fullnode`dus ein:
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
Die Instanz sollte in wenigen Minuten erstellt werden.

## Melden Sie sich bei der Instanz an (optional) {#login-to-instance-optional}

Es dauert ein paar Minuten, um die erforderliche Software und ein paar Stunden, um einen ausgewählten Snapshot herunterzuladen. Sie sollten sehen, dass funktionierende `bor`und `heimdalld`Prozesse weitere Laufwerke belegen. Zwecks Kontrolle können Sie die folgenden Befehle ausführen. Verbinden Sie sich and den Instanz-SSH-Service mittels `gcloud`SSH-Wrapper:
```bash
gcloud compute ssh ${INSTANCE_NAME}
# inside the connected session
sudo su -

ps uax|egrep "bor|heimdalld"
df -l -h
```
Sie können den folgenden Befehl verwenden, um den Installationsfortschritt zu sehen, es ist bei bootstrap wirklich praktisch `snapshot`
```bash
# inside the connected session
screen -dr
```
Verwenden Sie die `Control+a d`Tastenkombination, um die Fortschrittsüberprüfung zu beenden.

Sie können die folgenden Befehle verwenden, um Bor und Heimdall-Protokolle abzurufen:
```bash
# inside the connected session
journalctl -fu bor
journalctl -fu heimdalld
```
:::note
Blockchain-Daten werden auf zusätzlichen Laufwerken gespeichert, die standardmäßig auf der VM-Instanz-Entferung aufbewahrt werden. Sie müssen zusätzliche Festplatten manuell entfernen, wenn Sie diese Daten nicht mehr benötigen.
:::

Am Ende erhältst du eine Instanz, wie im Diagramm unten gezeigt:<img src={useBaseUrl("img/mainnet/polygon-instance.svg")} />

Wenn Sie auf ein Problem mit dieser Bedienungsanleitung stoßen – eröffnen Sie bitte ein [Thema](https://github.com/maticnetwork/matic-docs/issues) oder erstellen [eine PR](https://github.com/maticnetwork/matic-docs/pulls) auf [GitHub](https://github.com/maticnetwork/matic-docs).
