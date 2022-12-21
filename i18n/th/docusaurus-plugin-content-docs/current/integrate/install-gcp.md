---
id: install-gcp
title: ปรับใช้โหนด Polygon ใน Google Cloud
sidebar_label: Google Cloud Deployment
description: "การปรับใช้โหนด Polygon ของคุณใน Google Cloud"
keywords:
- docs
- polygon
- gcp
- google cloud
slug: install-gcp
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## รายละเอียด {#description}

ในเอกสารฉบับนี้ เราจะอธิบายวิธีปรับใช้โหนด Polygon กับ VM instance ใน Google Cloud

## ข้อกำหนดเกี่ยวกับฮาร์ดแวร์ {#hardware-requirements}

ตรวจสอบรายการฮาร์ดแวร์ขั้นต่ำ และ[รายการฮาร์ดแวร์](/docs/maintain/validate/validator-node-system-requirements) ที่แนะนำ ในเอกสาร Polygon

## ข้อกำหนดเกี่ยวกับซอฟท์แวร์ {#software-requirements}

ใช้เวอร์ชันใหม่ใดๆ ของ Debian หรือ Ubuntu Linux OS ซึ่ง ประกอบด้วยการสนับสนุนระยะยาว เช่น Debian 11 , Ubuntu 20.04 เราจะเน้นระบบ Ubuntu 20.04 ในคู่มือฉบับนี้

## ปรับใช้ instance (2 วิธี) {#deploy-instance-2-ways}

คุณสามารถใช้วิธีอย่างน้อย 2 วิธี  เพื่อสร้าง instance ใน Google Cloud:

* gcloud cli, local หรือ [Cloud Shell](https://cloud.google.com/shell)
* เว็บคอนโซล

เราจะอธิบายกรณีแรกในคู่มือฉบับนี้ เราจะเริ่มต้นด้วยการปรับใช้ผ่านการใช้ CLI
1. ติดตามส่วน ["ก่อนคุณเริ่ม"](https://cloud.google.com/compute/docs/instances/create-start-instance#before-you-begin) เพื่อติดตั้งและกำหนดค่ เครื่องมือบรรทัดคำสั่ง gcloud
ให้ความสำคัญกับภูมิภาคเริ่มต้นและโซน ให้เลือกที่อยู่ใกล้คุณ หรือลูกค้าของคุณ คุณ สามารถ ใช้ [gcping.com](https://gcping.com) เพื่อวัดความล่าช้าระหว่างสองจุด เพื่อเลือกตำแหน่งที่ตั้งที่ใกล้ที่สุด
2. ปรับตัวแปรคำสั่งดังต่อไปนี้ โดยใช้เครื่องมือแก้ไขที่นิยมของคุณก่อนดำเนินการถ้าจำเป็นต้องทำ
   * `POLYGON_NETWORK` - เลือกเครือข่าย `mainnet` หรือ `mumbai` testnet เพื่อเรียกใช้
   * `POLYGON_NODETYPE` - เลือก `archive`,`fullnode` ประเภทโหนด เพื่อเรียกใช้
   * `POLYGON_BOOTSTRAP_MODE` - เลือก โหมด bootstrap `snapshot` หรือ `from_scratch`
   * `POLYGON_RPC_PORT` - เลือก JSON RPC bor โหนดพอร์ต เพื่อใช้ใน การฟังค่าเริ่มต้น ต้องเป็นค่าที่ใช้ในการสร้าง VM instance creation และ กับข้อบังคับไฟร์วอลล์
   * `EXTRA_VAR` - เลือก สาขา Bor และ Heimdall ให้ใช้ `network_version=mainnet-v1` กับ เครือข่าย `mainnet` และ `network_version=testnet-v4` กับ เครือข่าย `mumbai`
   * `INSTANCE_NAME` - ชื่อ ของ VM instance ใน Polygon  ซึ่งเรากำลังจะสร้าง
   * `INSTANCE_TYPE` - GCP [ประเภทเครื่อง](https://cloud.google.com/compute/docs/machine-types), ค่า เริ่มต้น ที่แนะนำ ซึ่ง คุณ สามารถ เปลี่ยน ในภายหลัง ถ้า จำเป็น
   * `BOR_EXT_DISK_SIZE` - ขนาด ดิสก์ เพิ่มเติ่ม เป็น GB เพื่อ ให้ใช้ กับ ค่า เริ่มต้น ของ bor โดย `fullnode` เป็น ที่แนะนำ คุณ สามารถ เปลี่ยน มัน ได้ ในภายหลัง ถ้า จำเป็น คุณจะต้องการ 8192GB+ กับ `archive` โหนด
   * `HEIMDALL_EXT_DISK_SIZE` - ขนาดดิสก์เพิ่มเติมเป็น GB เพื่อใช้กับ heimdall โดยแนะนำให้ใช้ค่าเริ่มต้น
   * `DISK_TYPE` - GCP [ประเภท ดิสก์](https://cloud.google.com/compute/docs/disks#disk-types), SSD เป็น ที่ แนะนำ อย่างมาก คุณ อาจ ต้อง เพิ่ม โควตา SSD เป็น GB ใน ภูมิภาค ซึ่ง คุณ ใช้ เพื่อ เพิ่มขึ้น ความเร็ว ของ โหนด

3. ใช้ คำสั่ง ดังต่อไปนี้ เพื่อ สร้าง instance กับ ฮาร์ดแวร ที่ถูกต้อง และ ตาม ข้อกำหนด เกี่ยวกับ ซอฟต์แวร์ ใน ตัวอย่าง ดังต่อไปนี้ เรา จะ ปรับใช้ Polygon `mainnet` จาก `snapshot` กับ `fullnode` โหมด
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
คุณ ควร สร้าง instance ภายใน ไม่กี่ นาที

## เข้าสู่ระบบ เพื่อ สร้าง instance (ให้เลือกได้) {#login-to-instance-optional}

คุณ ต้อง ใช้ เวลา ไม่ กี่ นาที เพื่อ ติดตั้ง ซอฟต์แวร์ ทั้งหมด ที่ จำเป็น และ อีก ไม่ กี่ ชั่วโมง เพื่อ ดาวน์โหลด snapshot เมื่อ ได้ เลือก
คุณ ต้อง เห็น ว่า กระบวนการ `bor` และ `heimdalld` ทำงาน อยู่ โดย เติม ไดรฟ์ เพิ่มเติม คุณ สามารถ เรียกใช้ คำสั่ง ดังต่อไปนี้ เพื่อ ตรวจสอบ เรื่องนั้น
เชื่อมต่อ กับ บริการ SSH instance โดย ใช้ `gcloud` SSH wrapper:
```bash
gcloud compute ssh ${INSTANCE_NAME}
# inside the connected session
sudo su -

ps uax|egrep "bor|heimdalld"
df -l -h
```
คุณ สามารถ ใช้ คำสั่ง ดังต่อไปนี้ เพื่อ ติดตาม ความคืบหน้า ของ การติดตั้ง ซึ่ง มี ประโยชน์ จริง ๆ ใน กรณี `snapshot` bootstrap
```bash
# inside the connected session
screen -dr
```
ใช้ ชุด `Control+a d` คีย์ เพื่อ เลิก เชื่อมต่อ กับ การตรวจสอบ ความคืบหน้า

คุณ สามารถ ใช้ คำสั่ง ดังต่อไปนี้ เพื่อ ได้มา ซึ่ง logs ของ bor และ heimdall
```bash
# inside the connected session
journalctl -fu bor
journalctl -fu heimdalld
```
:::note

ข้อมูล บล็อกเชน ถูก บันททึก ใน ไดรฟ์ เพิ่มเติม ซึ่ง ตาม ค่าเริ่มต้น ถูก เก็บ ไว้ ใน การ ลบ instance VM คุณ จำเป็นต้อง ลบ ดิสก์ เพิ่มเติม ด้วย ตนเอง ถ้า คุณ ไม่ ต้องการ ข้อมูล นี้ อีก

:::

สุดท้าย คุณ จะ ได้ มา ซึ่ง instance ตาม ที่ แสดง ให้เห็น ใน แผนการ ด้านล่าง
<img src={useBaseUrl("img/mainnet/polygon-instance.svg")} />

หาก คุณ ประสบ ปัญหา กับ ตำรา ฉบับนี้ - โปรด อย่า เกร่งใจ และ แจ้ง [ปัญหา](https://github.com/maticnetwork/matic-docs/issues) หรือ [สร้าง PR](https://github.com/maticnetwork/matic-docs/pulls) ใน [GitHub](https://github.com/maticnetwork/matic-docs)
