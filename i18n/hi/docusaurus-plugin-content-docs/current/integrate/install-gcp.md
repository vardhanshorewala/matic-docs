---
id: install-gcp
title: गूगल क्लाउड पर पॉलीगॉन नोड्स तैनात करें
sidebar_label: Google Cloud Deployment
description: गूगल क्लाउड पर अपने पॉलीगॉन नोड्स की सरल तैनाती
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

# गूगल क्लाउड पर पॉलीगॉन नोड तैनात करें {#deploy-polygon-nodes-on-google-cloud}

इस दस्तावेज़ में, हम यह वर्णन करेंगे कि गूगल क्लाउड पर पॉलीगॉन नोड्स को एक वीएम इंस्टैंस में कैसे तैनात किया जाए.

### हार्डवेयर आवश्यकताएं {#hardware-requirements}

पॉलीगॉन विकीपीडिया में न्यूनतम और अनुशंसित [हार्डवेयर की आवश्यकताओं](/docs/maintain/validate/validator-node-system-requirements) को जाँचें

### सॉफ्टवेयर आवश्यकताएं {#software-requirements}

दीर्घावधि सहायता वाले किसी भी आधुनिक डेबियन या उबुन्तु लिनक्स OS, यानी डेबियन 11, उबुन्तु 20.04 का उपयोग करें. हम इस मैनुअल में उबुन्तु 20.04 पर ध्यान केंद्रित करेंगे

## डिप्लॉय इंस्टैंस (2 तरीके) {#deploy-instance-2-ways}

आप गूगल क्लाउड में एक इंस्टैंस बनाने के लिए कम से कम दो तरीकों का इस्तेमाल कर सकते हैं:

* gcloud cli, स्थानीय या [क्लाउड शेल](https://cloud.google.com/shell)
* वेब कंसोल

हम इस मैनुअल में पहले मामले को कवर करेंगे. आइये CLI का इस्तेमाल करके डिप्लॉयमेंट के साथ शुरूआत करते हैं:
1. gcloud कमांड-लाइन टूल को इंस्टॉल और कॉन्फ़िगर करने के लिए ["शुरूआत करने से पहले" सेक्शन](https://cloud.google.com/compute/docs/instances/create-start-instance#before-you-begin) को फॉलो करें. डिफ़ॉल्ट रीजन और ज़ोन पर ध्यान दें, अपने ऊपर या अपने ग्राहकों के करीब मौजूद किसी को चुनें. आप निकटतम स्थान चुनने के लिए लेटेंसी मापने के लिए [gcping.com](https://gcping.com) का इस्तेमाल कर सकते हैं.
2. जरूरत पड़ने पर, एग्जीक्यूट करने से पहले अपने पसंदीदा एडिटर का इस्तेमाल करके निम्नलिखित कमांड वेरिएबल को एडजस्ट करें
   * `POLYGON_NETWORK`- रन करने के लिए `mainnet`या `mumbai`टेस्टनेट नेटवर्क चुनें
   * `POLYGON_NODETYPE`- रन करने के लिए,`archive` `fullnode`नोड टाइप चुनें
   * `POLYGON_BOOTSTRAP_MODE`- बूटस्ट्रैप मोड `snapshot`या`from_scratch` चुनें
   * `POLYGON_RPC_PORT`- JSON RPC बोर नोड पोर्ट चुनें जिस पर सुनना है, जिसका डिफ़ॉल्ट वैल्यू वही है जो VM इंस्टैंस का निर्माण करते समय और फायरवॉल नियमों में इस्तेमाल किया जाता है
   * `EXTRA_VAR`- बोर और हेम्डल शाखाएं चुनें, नेटवर्क `network_version=mainnet-v1`के साथ `mainnet`और नेटवर्क `mumbai`के साथ`network_version=testnet-v4` इस्तेमाल करें
   * `INSTANCE_NAME`- पॉलीगॉन के साथ एक VM इंस्टैंस का नाम जिसे हम बनाने जा रहे हैं
   * `INSTANCE_TYPE`- GCP [मशीन टाइप](https://cloud.google.com/compute/docs/machine-types), डिफ़ॉल्ट वैल्यू की सिफारिश की जाती है, जरूरत पड़ने पर आप इसे बाद में बदलें सकते हैं
   * `BOR_EXT_DISK_SIZE`- बोर के साथ इस्तेमाल करने के लिए GB में अतिरिक्त डिस्क साइज, `fullnode`के साथ डिफ़ॉल्ट वैल्यू की सिफारिश की जाती है, जरूरत पड़ने पर आप इसे बाद में बढ़ा सकते हैं. हालांकि आपको `archive`नोड के साथ 8192 GB+ की जरूरत होगी
   * `HEIMDALL_EXT_DISK_SIZE`- हेम्डल के साथ इस्तेमाल करने के लिए GB में अतिरिक्त डिस्क साइज, डिफ़ॉल्ट वैल्यू की सिफारिश की जाती है
   * `DISK_TYPE`- GCP [डिस्क टाइप](https://cloud.google.com/compute/docs/disks#disk-types), SSD की उच्च सिफारिश की जाती है. आपको उस रीजन में कुल SSD GB कोटा को बढ़ाना पड़ सकता है जिस रीजन में आप नोड को स्पिन कर रहे हैं.

3. सटीक हार्डवेयर और सॉफ्टवेयर आवश्यकताओं के साथ एक इंस्टैंस का निर्माण करने के लिए निम्नलिखित कमांड का इस्तेमाल करें. नीचे दिए गए उदाहरण में हम मोड के `fullnode`के साथ `snapshot`से पॉलीगॉन `mainnet`को डिप्लॉय करते हैं:
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
इंस्टैंस को दो मिनट के दौरान बनाया जाना चाहिए

## इंस्टैंस के लिए लॉगिन करें (वैकल्पिक) {#login-to-instance-optional}

सभी आवश्यक सॉफ्टवेयर को इंस्टाल करने के लिए दो-चार मिनट और चुने जाने पर एक स्नैपशॉट को डाउनलोड करने के लिए दो-चार घंटे का समय लगेगा. आपको अतिरिक्त ड्राइव को भरने की `bor`और `heimdalld`प्रक्रिया दिखाई देनी चाहिए. आप इसे जांचने के लिए निम्नलिखित कमांड्स को रन कर सकते हैं.
`gcloud` SSH रैपर का इस्तेमाल करके इंस्टैंस SSH सर्विस से कनेक्ट करें:
```bash
gcloud compute ssh ${INSTANCE_NAME}
# inside the connected session
sudo su -

ps uax|egrep "bor|heimdalld"
df -l -h
```
आप इंस्टालेशन की प्रगति को देखने के लिए निम्नलिखित कमांड का इस्तेमाल कर सकते हैं, यह `snapshot`बूटस्ट्रैप के मामले में सच में बहुत आरामदायक है
```bash
# inside the connected session
screen -dr
```
प्रगति समीक्षा से डिस्कनेक्ट करने के लिए `Control+a d`कुंजी संयोजन का इस्तेमाल करें.

आप बोर और हेम्डल लॉग को हासिल करने के लिए निम्नलिखित कमांड्स का इस्तेमाल कर सकते हैं:
```bash
# inside the connected session
journalctl -fu bor
journalctl -fu heimdalld
```
:::note
ब्लॉकचेन डेटा को अतिरिक्त ड्राइवों में सहेजा जाता है जिन्हें डिफ़ॉल्ट रूप में VM इंस्टैंस निष्कासन पर रखा जाता है. यदि आपको अबइस डेटा की जरूरत नहीं है तो आपको अतिरिक्त डिस्क को मैन्युअल रूप से हटाना पड़ेगा.
:::

अंत में आपको एक इंस्टैंस मिलेगा जैसा कि नीचे दिए गए आरेख पर दिखाया गया है:<img src={useBaseUrl("img/mainnet/polygon-instance.svg")} />

यदि आपको इस मैनुअल के साथ कोई समस्या होती है - कृपया निःसंकोच होकर [GitHub](https://github.com/maticnetwork/matic-docs) पर एक[ मुद्दा ](https://github.com/maticnetwork/matic-docs/issues)खोलें या [एक PR बनाएं](https://github.com/maticnetwork/matic-docs/pulls).
