---
id: install-gcp
title: Menyebarkan node Polygon pada Google Cloud
sidebar_label: Google Cloud Deployment
description: Penyebaran sederhana dari node Polygon Anda di Google Cloud
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

# Menyebarkan Node Polygon pada Google Cloud {#deploy-polygon-nodes-on-google-cloud}

Dalam dokumen ini, kita akan menjelaskan bagaimana cara menyebarkan node Polygon ke dalam contoh VM di Google Cloud.

### Persyaratan perangkat keras {#hardware-requirements}

Periksa [persyaratan perangkat keras](/docs/maintain/validate/validator-node-system-requirements) minimum dan direkomendasikan di Polygon Wiki.

### Persyaratan perangkat lunak {#software-requirements}

Gunakan Debian modern atau Ubuntu Linux OS dengan dukungan jangka panjang, yaitu Debian 11, Ubuntu 20.04. Kita akan berfokus pada Ubuntu 20.04 di manual ini

## Sebar instans (2 cara) {#deploy-instance-2-ways}

Anda dapat menggunakan setidaknya dua cara untuk membuat instans di Google Cloud:

* gcloud cli, lokal atau [Cloud Shell](https://cloud.google.com/shell)
* Konsol web

Kita akan membahas kasus pertama di manual ini. Mari kita mulai dengan penyebaran menggunakan CLI:
1. Ikuti [bagian "Sebelum Anda mulai"](https://cloud.google.com/compute/docs/instances/create-start-instance#before-you-begin) untuk menginstal dan mengonfigurasi alat baris perintah gcloud.
Perhatikan wilayah dan zona default, pilih yang lebih dekat dengan Anda atau pelanggan Anda. Anda dapat menggunakan [gcping.com](https://gcping.com) untuk mengukur latensi untuk memilih lokasi terdekat.
2. Sesuaikan variabel perintah berikut menggunakan editor favorit Anda sebelum mengeksekusi, jika dibutuhkan
   * `POLYGON_NETWORK` - pilih `mainnet` atau `mumbai` jaringan testnet untuk dijalankan
   * `POLYGON_NODETYPE` - pilih `archive`, `fullnode` jenis node untuk dijalankan
   * `POLYGON_BOOTSTRAP_MODE` - pilih mode bootstrap `snapshot` atau `from_scratch`
   * `POLYGON_RPC_PORT` - pilih port node bor JSON RPC untuk mendengarkan, nilai default adalah apa yang digunakan pada pembuatan instans VM dan dalam aturan firewall
   * `EXTRA_VAR` - pilih cabang Bor dan Heimdall, gunakan `network_version=mainnet-v1` dengan `mainnet` jaringan dan `network_version=testnet-v4` dengan `mumbai` jaringan
   * `INSTANCE_NAME` - nama instans VM dengan Polygon yang akan kita buat
   * `INSTANCE_TYPE` - [jenis mesin](https://cloud.google.com/compute/docs/machine-types) GCP, nilai default direkomendasikan, Anda dapat mengubahnya nanti ketika diperlukan
   * `BOR_EXT_DISK_SIZE` - ukuran disk tambahan dalam GB untuk digunakan dengan Bor, nilai default dengan `fullnode` direkomendasikan, Anda dapat meningkatkannya nanti jika diperlukan. Namun, Anda akan membutuhkan 8192GB+ dengan node `archive`
   * `HEIMDALL_EXT_DISK_SIZE` - ukuran disk tambahan dalam GB untuk digunakan dengan Heimdall, nilai default direkomendasikan
   * `DISK_TYPE` - [jenis disk](https://cloud.google.com/compute/docs/disks#disk-types) GCP, SSD sangat direkomendasikan. Anda mungkin perlu meningkatkan kuota SSDS GB total di wilayah tempat Anda memutar node.

3. Gunakan perintah berikut untuk membuat instans dengan persyaratan perangkat keras dan perangkat lunak yang benar. Pada contoh di bawah ini, kami sebar Polygon `mainnet`dari `snapshot` dengan`fullnode` mode:
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
Instans akan dibuat selama beberapa menit

## Masuk ke instans (opsional) {#login-to-instance-optional}

Dibutuhkan beberapa menit untuk menginstal semua perangkat lunak yang diperlukan dan beberapa jam untuk mengunduh snapshot ketika dipilih.
Anda akan melihat `bor` bekerja dan proses `heimdalld` mengisi drive tambahan. Anda dapat menjalankan perintah berikut untuk memeriksanya.
Hubungkan ke layanan instans SSH menggunakan `gcloud` SSH wrapper:
```bash
gcloud compute ssh ${INSTANCE_NAME}
# inside the connected session
sudo su -

ps uax|egrep "bor|heimdalld"
df -l -h
```
Anda dapat menggunakan perintah berikut untuk melihat kemajuan instalasi, ini sangat berguna dalam kasus bootstrap `snapshot`
```bash
# inside the connected session
screen -dr
```
Gunakan kombinasi kunci `Control+a d`untuk memutuskan sambungan dari tinjauan kemajuan.

Anda dapat menggunakan perintah berikut untuk mendapatkan log Bor dan Heimdall:
```bash
# inside the connected session
journalctl -fu bor
journalctl -fu heimdalld
```
:::note

Data blockchain disimpan ke drive tambahan yang disimpan secara default saat penghapusan instans VM. Anda perlu menghapus disk tambahan secara manual jika Anda tidak membutuhkan data ini lagi.

:::

Pada akhirnya Anda akan mendapatkan contoh seperti yang ditunjukkan pada diagram di bawah ini:<img src={useBaseUrl("img/mainnet/polygon-instance.svg")} />

Jika Anda mengalami isu dengan manual ini - jangan ragu untuk membuka [isu](https://github.com/maticnetwork/matic-docs/issues) atau [membuat PR](https://github.com/maticnetwork/matic-docs/pulls) di [GitHub](https://github.com/maticnetwork/matic-docs).
