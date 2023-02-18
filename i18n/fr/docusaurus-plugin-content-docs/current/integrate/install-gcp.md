---
id: install-gcp
title: Déployez des nœuds Polygon sur Google Cloud
sidebar_label: Google Cloud Deployment
description: déploiement simple de vos nœuds Polygon sur Google Cloud
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

# Déployez des nœuds Polygon sur Google Cloud {#deploy-polygon-nodes-on-google-cloud}

Dans ce document, nous décrirons comment déployer des nœuds Polygon dans une instance VM sur Google Cloud.

### Configuration matérielle requise {#hardware-requirements}

Vérifiez les [exigences matérielles](/docs/maintain/validate/validator-node-system-requirements) minimales et recommandées dans Polygon Wiki.

### Configuration logicielle requise {#software-requirements}

Utilisez n'importe quel système d'exploitation moderne Debian ou Ubuntu Linux avec une prise en charge à long terme, par exemple Debian 11, Ubuntu 20.04. Nous nous concentrerons sur Ubuntu 20.04 dans ce manuel

## Déployer l'instance (2 façons) {#deploy-instance-2-ways}

Vous pouvez utiliser au moins deux méthodes pour créer une instance dans Google Cloud :

* gcloud cli, local ou [Cloud Shell](https://cloud.google.com/shell)
* Console web

Nous aborderons le premier cas dans ce manuel. Commençons par le déploiement en utilisant CLI :
1. Suivez [la section « Avant de commencer](https://cloud.google.com/compute/docs/instances/create-start-instance#before-you-begin) pour installer et configurer l'outil de ligne de commande gcloud. Faites attention à la région et à la zone par défaut : choisissez celles qui sont plus proches de vous ou de vos clients. Vous pouvez utiliser [gcping.com](https://gcping.com) pour mesurer la latence afin de choisir l'emplacement le plus proche.
2. Ajustez les variables de commande suivantes à l'aide de votre éditeur favori avant de l'exécuter, si nécessaire
   * `POLYGON_NETWORK` - choisir le testnet du réseau `mainnet` ou `mumbai` à exécuter
   * `POLYGON_NODETYPE` - choisir `archive``fullnode` le type de nœud à exécuter
   * `POLYGON_BOOTSTRAP_MODE` - choisir le mode bootstrap `snapshot` ou `from_scratch`
   * `POLYGON_RPC_PORT` - choisir le port de nœud JSON RPC Bor à écouter. La valeur par défaut est celle utilisée pour la création d'instance de VM et dans les règles de pare-feu
   * `EXTRA_VAR` - choisir les branches Bor et Heimdall, les utiliser `network_version=mainnet-v1`avec le réseau `mainnet` et `network_version=testnet-v4` avec le réseau `mumbai`
   * `INSTANCE_NAME` - le nom d'une instance de VM avec Polygon que nous allons créer
   * `INSTANCE_TYPE` - [Type de machine](https://cloud.google.com/compute/docs/machine-types) GCP. La valeur par défaut est recommandée, vous pouvez la modifier ultérieurement si nécessaire
   * `BOR_EXT_DISK_SIZE` - taille de disque supplémentaire en Go à utiliser avec Bor. La valeur par défaut avec `fullnode`est recommandée, vous pouvez l'augmenter plus tard si nécessaire. Vous aurez besoin de 8192 Go+ avec le nœud `archive`
   * `HEIMDALL_EXT_DISK_SIZE` - taille de disque supplémentaire en Go à utiliser avec Heimdall. La valeur par défaut est recommandée
   * `DISK_TYPE` - le [type de disque](https://cloud.google.com/compute/docs/disks#disk-types) GCP, SSD est fortement recommandé. Vous devrez peut-être augmenter le quota total de Go SSD dans la zone où vous faites tourner le nœud vers le haut.

3. Utilisez la commande suivante pour créer une instance avec les exigences matérielles et logicielles correctes. Dans l'exemple ci-dessous, nous déployons Polygon `mainnet`à partir de `snapshot` avec le `fullnode`mode:
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
L'instance doit être créée pendant quelques minutes

## Connexion à l'instance (facultatif) {#login-to-instance-optional}

Il faudra quelques minutes pour installer tous les logiciels requis et quelques heures pour télécharger un instantané au moment choisi. Vous devriez voir fonctionner `bor` et les processus `heimdalld` remplir des disques supplémentaires. Vous pouvez exécuter les commandes suivantes pour le vérifier.
Se connecter au service SSH de l'instance à l'aide du `gcloud` wrapper SSH:
```bash
gcloud compute ssh ${INSTANCE_NAME}
# inside the connected session
sudo su -

ps uax|egrep "bor|heimdalld"
df -l -h
```
Vous pouvez utiliser la commande suivante pour suivre la progression de l'installation, qui est vraiment pratique en cas de `snapshot` bootstrap
```bash
# inside the connected session
screen -dr
```
Utilisez la combinaison de touches `Control+a d` pour vous déconnecter de l'aperçu de progression.

Vous pouvez utiliser les commandes suivantes pour obtenir les journaux Bor et Heimdall :
```bash
# inside the connected session
journalctl -fu bor
journalctl -fu heimdalld
```
:::note

Les données de la blockchain sont enregistrées sur des lecteurs supplémentaires qui sont conservés par défaut lors de la suppression de l'instance de VM. Vous devez supprimer manuellement des disques supplémentaires si vous n'avez plus besoin de ces données.
:::

À la fin, vous obtiendrez une instance comme indiqué sur le diagramme ci-dessous:<img src={useBaseUrl("img/mainnet/polygon-instance.svg")} />

Si vous rencontrez un problème avec ce manuel, n'hésitez pas à signaler un [problème](https://github.com/maticnetwork/matic-docs/issues) ou à [créer un PR](https://github.com/maticnetwork/matic-docs/pulls) sur [GitHub](https://github.com/maticnetwork/matic-docs).
