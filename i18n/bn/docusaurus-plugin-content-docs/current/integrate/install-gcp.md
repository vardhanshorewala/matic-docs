---
id: install-gcp
title: গুগল ক্লাউডে Polygon নোড Deploy  করুন
sidebar_label: Google Cloud Deployment
description: গুগল ক্লাউডে আপনার Polygon নোডের সহজ deployment মেন্ট
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

# গুগল ক্লাউডে Polygon নোড স্থাপন করুন {#deploy-polygon-nodes-on-google-cloud}

এই ডকুমেন্টে আমরা কিভাবে Google Cloud-এ একটি VM ইনস্ট্যান্সে Polygon নোডকে deploy  করতে হবে তা বর্ণনা করব।

### হার্ডওয়্যারের প্রয়োজনীয়তা {#hardware-requirements}

Polygon in সর্বনিম্ন এবং প্রস্তাবিত [হার্ডওয়্যার প্রয়োজনীয়তা](/docs/maintain/validate/validator-node-system-requirements) চেক করুন।

### সফটওয়্যারের প্রয়োজনীয়তা {#software-requirements}

দীর্ঘমেয়াদী সহায়তা সহ যেকোনো আধুনিক Debian বা Ubuntu Linux OS ব্যবহার করুন, অর্থাৎ Debian 11, Ubuntu 20.04। এই ম্যানুয়ালে আমরা Ubuntu 20.04-এর উপর আলোকপাত করব

## ডিপ্লয়ের ইনস্ট্যান্স (2 উপায়) {#deploy-instance-2-ways}

Google Cloud-এ একটি ইনস্ট্যান্স তৈরি করতে আপনি কমপক্ষে দুটি উপায় ব্যবহার করতে পারেন:

* gcloud cli, স্থানীয় বা [ক্লাউড শেল](https://cloud.google.com/shell)
* ওয়েব কনসোল

এই ম্যানুয়ালে আমরা প্রথম বিষয়টি আলোচনা করব। CLI ব্যবহার করে ডিপ্লয়মেন্ট করার মাধ্যমে শুরু করা যাক:
1. gcloud কমান্ড-লাইন টুল ইনস্টল এবং কনফিগার করার জন্য ["শুরু করার আগে" সেকশন](https://cloud.google.com/compute/docs/instances/create-start-instance#before-you-begin) অনুসরণ করুন।
ডিফল্ট অঞ্চল এবং জোনের উপর মনোযোগ দিন, আপনার বা আপনার গ্রাহকদের নিকটতম যা আছে তা নির্বাচন করুন। নিকটতম অবস্থান নির্বাচন করার জন্য ল্যাটেন্সি পরিমাপ করতে আপনি [gcping.com](https://gcping.com) ব্যবহার করতে পারেন।
2. প্রয়োজন হলে, এক্সিকিউট করার পূর্বে আপনার পছন্দের এডিটর ব্যবহার করে নিম্নলিখিত কমান্ড ভেরিয়েবলগুলো সমন্বয় করুন
   * `POLYGON_NETWORK` - রান করার জন্য `mainnet` বা `mumbai` টেস্টনেট নেটওয়ার্ক নির্বাচন করুন
   * `POLYGON_NODETYPE` - রান করার জন্য `archive`, `fullnode` নোডের প্রকার নির্বাচন করুন
   * `POLYGON_BOOTSTRAP_MODE` - বুটস্ট্র্যাপ মোড `snapshot` বা `from_scratch` নির্বাচন করুন
   * `POLYGON_RPC_PORT` - শোনার জন্য JSON RPC Bor নোড পোর্ট নির্বাচন করুন, VM ইনস্ট্যান্স তৈরি ও ফায়ারওয়ালের নিয়মাবলীতে ব্যবহৃত মানই হচ্ছে ডিফল্ট মান
   * `EXTRA_VAR` - Bor ও Heimdall শাখাগুলো নির্বাচন করুন, `mainnet` নেটওয়ার্কের সাথে `network_version=mainnet-v1` এবং `mumbai` নেটওয়ার্কের সাথে `network_version=testnet-v4` ব্যবহার করুন
   * `INSTANCE_NAME` - Polygon-এর সাথে আমরা যে VM ইনস্ট্যান্স তৈরি করতে যাচ্ছি তার নাম
   * `INSTANCE_TYPE` - GCP [মেশিনের প্রকার](https://cloud.google.com/compute/docs/machine-types), ডিফল্ট মানকেই সুপারিশ করা হচ্ছে, প্রয়োজন হলে আপনি পরে তা পরিবর্তন করতে পারবেন
   * `BOR_EXT_DISK_SIZE` - Bor-এর সাথে ব্যবহার করার জন্য GB-তে ডিস্কের অতিরিক্ত আকার, `fullnode`-এর সাথে ডিফল্ট মান সুপারিশ করা হয়, প্রয়োজন হলে আপনি পরে তা বৃদ্ধি করতে পারবেন। যদিও `archive` নোডের সাথে আপনার 8192GB+ প্রয়োজন হবে
   * `HEIMDALL_EXT_DISK_SIZE` - Heimdall-এর সাথে ব্যবহার করার জন্য ডিস্কের অতিরিক্ত আকার, ডিফল্ট মান সুপারিশ করা হয়
   * `DISK_TYPE` - GCP [ডিস্কের প্রকার](https://cloud.google.com/compute/docs/disks#disk-types), SSD-এর ব্যাপারে জোরালোভাবে সুপারিশ করা হয়। আপনি যে অঞ্চলে নোডটি স্পিনিং আপ করছেন তার জন্য আপনাকে মোট SSD GB কোটা বৃদ্ধি করতে হতে পারে।

3. সঠিক হার্ডওয়্যার এবং সফটওয়্যারের প্রয়োজনীয়তা সহ একটি ইনস্ট্যান্স তৈরি করতে নিম্নলিখিত কমান্ড ব্যবহার করুন। নিচের উদাহরণে, আমরা `snapshot` থেকে `fullnode` মোড সহ Polygon `mainnet` ডিপ্লয় করছি:
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
কয়েক মিনিটের মধ্যেই ইনস্ট্যান্সটি তৈরি হয়ে যাওয়ার কথা

## ইনস্ট্যান্সে লগইন করুন (ঐচ্ছিক) {#login-to-instance-optional}

প্রয়োজনীয় সকল সফটওয়্যার ইনস্টল হতে কয়েক মিনিট সময় লাগবে এবং নির্বাচন করার পর একটি স্ন্যাপশট ডাউনলোড করতে কয়েক ঘন্টা সময় লাগবে।
আপনি `bor` ও `heimdalld` প্রক্রিয়াগুলোকে অতিরিক্ত ড্রাইভগুলো পূরণ হতে দেখবেন। এটি চেক করতে আপনি নিম্নলিখিত কমান্ড চালাতে পারেন।
`gcloud` SSH র‍্যাপার ব্যবহার করে ইনস্ট্যান্স SSH পরিষেবার সাথে যুক্ত হন:
```bash
gcloud compute ssh ${INSTANCE_NAME}
# inside the connected session
sudo su -

ps uax|egrep "bor|heimdalld"
df -l -h
```
ইনস্টলেশনের অগ্রগতি দেখতে আপনি নিম্নলিখিত কমান্ড ব্যবহার করতে পারেন, `snapshot` bootstrap-এর ক্ষেত্রে এটি সত্যিই সুবিধাজনক
```bash
# inside the connected session
screen -dr
```
অগ্রগতির পর্যালোচনা থেকে বিচ্ছিন্ন করতে `Control+a d` কী সমন্বয় ব্যবহার করুন।

Bor এবং Heimdall-এর লগগুলো পেতে আপনি নিম্নলিখিত কমান্ড ব্যবহার করতে পারেন:
```bash
# inside the connected session
journalctl -fu bor
journalctl -fu heimdalld
```
:::note

ব্লকচেইন ডেটা অতিরিক্ত ড্রাইভে সংরক্ষিত হয়, যা ডিফল্টরূপে VM ইনস্ট্যান্স অপসারণকারীতে রাখা হয়। আপনার যদি আর এই ডেটার প্রয়োজন না হয়, তবে আপনাকে ম্যানুয়াল উপায়ে অতিরিক্ত ডিস্কগুলো অপসারণ করতে হবে।

:::

শেষে আপনি নীচের ডায়াগ্রামে দেখানো একটি উদাহরণ পাবেন:<img src={useBaseUrl("img/mainnet/polygon-instance.svg")} />

এই ম্যানুয়ালের কোনো কিছু যদি ঠিকভাবে বুঝতে না পারেন - তাহলে অনুগ্রহ করে [GitHub](https://github.com/maticnetwork/matic-docs)-এ একটি [সমস্যা](https://github.com/maticnetwork/matic-docs/issues) খুলুন বা [একটি PR তৈরি করুন](https://github.com/maticnetwork/matic-docs/pulls)।
