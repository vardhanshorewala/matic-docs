---
id: install-gcp
title: Mag-deploy ng mga Polygon node sa Google Cloud
sidebar_label: Google Cloud Deployment
description: "Simpleng pag-deploy ng iyong mga Polygon node sa Google Cloud."
keywords:
- docs
- polygon
- gcp
- google cloud
slug: install-gcp
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## Paglalarawan {#description}

Sa dokumentong ito, ilalarawan namin kung paano mag-deploy ng mga Polygon node sa instance ng VM sa Google Cloud

## Mga kinakailangan sa hardware {#hardware-requirements}

Tingnan ang minimum at inirerekomendang [mga kinakailangan sa hardware](/docs/maintain/validate/validator-node-system-requirements) sa mga dokumento ng Polygon

## Mga kinakailangan sa software {#software-requirements}

Gumamit ng anumang makabagong Debian o Ubuntu Linux OS na may pangmatagalang suporta, ibig sabihin Debian 11, Ubuntu 20.04. Magpopokus tayo sa Ubuntu 20.04 sa manual na ito

## I-deploy ang instance (2 paraan) {#deploy-instance-2-ways}

Maaari kang gumamit ng hindi bababa sa dalawang paraan para gumawa ng instance sa Google Cloud:

* gcloud cli, local o [Cloud Shell](https://cloud.google.com/shell)
* Web console

Tatalakayin namin ang unang kaso sa manual na ito. Magsimula tayo sa pag-deploy gamit ang CLI:
1. Sundin ang [seksyong "Bago tayo magsimula"](https://cloud.google.com/compute/docs/instances/create-start-instance#before-you-begin) para i-install at i-configure ang gcloud command-line tool.
Bigyang-pansin ang default na rehiyon at zone, piliin ang mga mas malapit sa iyo o sa iyong mga customer. Maaari mong gamitin ang [gcping.com](https://gcping.com) upang sukatin ang latency para piliin ang pinakamalapit na lokasyon.
2. I-adjust ang mga sumusunod na command variable gamit ang paborito mong editor bago magsagawa, kapag kinakailangan
   * `POLYGON_NETWORK` - piliin ang `mainnet` o `mumbai` testnet network para patakbuhin
   * `POLYGON_NODETYPE` - piliin ang `archive`,`fullnode` na uri ng node para patakbuhin
   * `POLYGON_BOOTSTRAP_MODE` - piliin ang bootstrap mode na `snapshot` o `from_scratch`
   * `POLYGON_RPC_PORT` - piliin ang JSON RPC bor node port na papakinggan, ang default na value ay ang ginagamit sa paggawa ng instance ng VM at sa mga tuntunin ng firewall
   * `EXTRA_VAR` - piliin ang mga sangay ng Bor at Heimdall, gamitin ang `network_version=mainnet-v1` sa `mainnet` network at `network_version=testnet-v4` sa `mumbai` network
   * `INSTANCE_NAME` - ang pangalan ng isang instance ng VM sa Polygon na gagawin natin
   * `INSTANCE_TYPE` - GCP [machine type](https://cloud.google.com/compute/docs/machine-types), inirerekomenda ang default na value, Maaari mo itong baguhin sa ibang pagkakataon kung kinakailangan
   * `BOR_EXT_DISK_SIZE` - karagdagang laki ng disk sa GB na gagamitin sa Bor, inirerekomenda ang default na value na may `fullnode`, maaari mo itong palawigin sa ibang pagkakataon kung kinakailangan. Gayunman, kakailanganin mo ng 8192GB+ na may `archive` node
   * `HEIMDALL_EXT_DISK_SIZE` - karagdagang laki ng disk sa GB na gagamitin sa Heimdall, inirerekomenda ang default na value
   * `DISK_TYPE` - GCP [disk type](https://cloud.google.com/compute/docs/disks#disk-types), lubusang inirerekomenda ang SSD. Maaaring kailanganin mong dagdagan ang kabuuang SSD GB quota sa rehiyon kung saan mo pinapatakbo ang node.

3. Gamitin ang sumusunod na command para gumawa ng instance na may tamang mga kinakailangan sa hardware at software. Sa halimbawa sa ibaba, dine-deploy natin ang Polygon `mainnet` mula sa `snapshot` gamit ang `fullnode` mode:
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
Dapat gawin ang instance sa loob ng ilang minuto

## Mag-login sa instance (opsyonal) {#login-to-instance-optional}

Tatagal nang ilang minuto para i-install ang lahat ng kinakailangang software at ilang oras para mag-download ng snapshot kapag pinili.
Dapat kang makakita ng mga gumaganang proseso ng `bor` at `heimdalld` na nagpupuno sa mga karagdagang drive. Maaari mong patakbuhin ang mga sumusunod na command para tingnan ito.
Ikonekta ang instance sa serbisyo ng SSH gamit ang `gcloud` SSH wrapper:
```bash
gcloud compute ssh ${INSTANCE_NAME}
# inside the connected session
sudo su -

ps uax|egrep "bor|heimdalld"
df -l -h
```
Maaari mong gamitin ang sumusunod na command para pagmasdan ang pag-usad ng pag-install, talagang kapaki-pakinabang ito sa kaso ng `snapshot` bootstrap
```bash
# inside the connected session
screen -dr
```
Gamitin ang `Control+a d` na kumbinasyon ng key para dumiskonekta mula sa pagsusuri ng pag-usad.

Maaari mong gamitin ang mga sumusunod na command para makuha ang mga log ng Bor at Heimdall:
```bash
# inside the connected session
journalctl -fu bor
journalctl -fu heimdalld
```
:::note

Sine-save ang data ng blockchain sa mga karagdagang drive na pinapanatili nang default kapag inalis ang instance ng VM. Kailangan mong alisin ang mga karagdagang disk nang mano-mano kung hindi mo na kailangan ang data na ito.

:::

Sa huli, makakakuha ka ng instance tulad ng ipinapakita sa diagram sa ibaba:
<img src={useBaseUrl("img/mainnet/polygon-instance.svg")} />

Kung magkaroon ka ng isyu sa manual na ito - mangyaring huwag mag-atubiling magbukas ng [isyu](https://github.com/maticnetwork/matic-docs/issues) o [gumawa ng PR](https://github.com/maticnetwork/matic-docs/pulls) sa [GitHub](https://github.com/maticnetwork/matic-docs).
