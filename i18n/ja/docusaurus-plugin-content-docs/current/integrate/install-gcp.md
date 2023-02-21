---
id: install-gcp
title: Google CloudにPolygonノードをデプロイする
sidebar_label: Google Cloud Deployment
description: Google Cloud上のPolygonノードを簡単に展開できます。
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

# Google CloudにPolygonノードをデプロイする {#deploy-polygon-nodes-on-google-cloud}

本文では、Google Cloud上のVMインスタンスにPolygonノードを展開する方法について説明します。

### ハードウェア要件 {#hardware-requirements}

最小および推奨の[ハードウェア要件](/docs/maintain/validate/validator-node-system-requirements)をPolygon Wikiで確認してください。

### ソフトウェア要件 {#software-requirements}

あらゆる長期サポート付きの最新のDebianまたはUbuntu Linux。例はDebian 11、Ubuntu 20.04です。 このマニュアルでは、Ubuntu 20.04に焦点を当てます。

## デプロイ事例（2つの方法） {#deploy-instance-2-ways}

Google Cloudでインスタンスを作成するには、少なくとも２つの方法を使用できます。

* gcloud cli、ローカルまたは [クラウドシェル](https://cloud.google.com/shell)
* webコンソール

このマニュアルでは最初のケースをカバーします。まずCLIを使用したデプロイから開始します。
1.  [「開始する前に」セクション](https://cloud.google.com/compute/docs/instances/create-start-instance#before-you-begin) に従ってインストールとgcloudコマンドラインツールの設定を行います。デフォルトの領域とゾーンに注意し、あなたまたはあなたの顧客に近いものを選択します。待ち時間を測定するには、[gcping.com](https://gcping.com) を使用して最も近い場所を選択することもできます。
2. 必要に応じて、好みのエディタを使用して実行する前に以下のコメント変数を調整します。
   * `POLYGON_NETWORK` - 選択 `mainnet` または `mumbai` テストネットネットワークを実行します
   * `POLYGON_NODETYPE` - 選択 `archive`、`fullnode` ノードタイプを実行します
   * `POLYGON_BOOTSTRAP_MODE` - 選択するブートストラップモードは `snapshot` または `from_scratch`
   * `POLYGON_RPC_PORT` - 聞くためのJSON RPCバーノードを選択します。デフォルト値はVMインスタンス作成とファイアウォールルールで使用されているものです。
   * `EXTRA_VAR` - BorとHeimdallのブランチを選択します。 `network_version=mainnet-v1` と `mainnet` ネットワークおよび `network_version=testnet-v4` と·`mumbai` ネットワークを使用します。
   * `INSTANCE_NAME` - Polygonで作成するVMインスタンスの名前です
   * `INSTANCE_TYPE` - GCP [マシンタイプ](https://cloud.google.com/compute/docs/machine-types)、デフォルト値が推奨されます。必要に応じて後でこれを変更することもできます。
   * `BOR_EXT_DISK_SIZE` - GB。Borと使用する場合の追加ディスクサイズ、デフォルト値と `fullnode` が推奨されます。必要に応じて後で拡張することもできます。8192GB+と `archive` ノードスルーが必要です
   * `HEIMDALL_EXT_DISK_SIZE` - GB。Heimdallと使用する場合の追加ディスクサイズ、デフォルト値が推奨されます
   * `DISK_TYPE` - GCP [ディスクタイプ](https://cloud.google.com/compute/docs/disks#disk-types)、SSDを強く推奨します。 ノードをスピンアップしている領域のSSDの総GB割り当て量を増やす必要があるかもしれません。

3. 以下のコマンドを使用して、ハードウェアとソフトウェアの要件が正しいインスタンスを作成します。下記の例ではPolygonを `mainnet` から `snapshot` に `fullnode` モードでデプロイします。
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
インスタンスは数分間で作成すべきです。

## インスタンスへのログイン（オプション） {#login-to-instance-optional}

必要なソフトウェアをすべてインストールするのに数分かかるほか、選択した場合にはスナップショットをダウンロードするのに数時間かかります。作業 `bor` と `heimdalld` プロセスが追加ドライブを満たすことがわかるはずです。次のコマンドの実行を通じてチェックすることもできます。
インスタンスSSHサービスに `gcloud` SSHラッパーを使用して接続します。
```bash
gcloud compute ssh ${INSTANCE_NAME}
# inside the connected session
sudo su -

ps uax|egrep "bor|heimdalld"
df -l -h
```
インストール進行状況を監視するには、次のコメントを使用できますが、 `snapshot` ブートストラップの場合には本当に便利です。
```bash
# inside the connected session
screen -dr
```
進行レビューから切断するには、 `Control+a d` 鍵のコンビネーションを使用します。

BorログとHeimdallログを取得するには、以下のコマンドを使用することもできます。
```bash
# inside the connected session
journalctl -fu bor
journalctl -fu heimdalld
```
:::note

ブロックチェーンデータはVMインスタンス削除時にデフォルトで保持される追加ドライブに保存されます。このデータがもう必要ない場合は追加ディスクを手動で削除する必要があります。
:::

最後に、下記の図に示すようにインスタンスを取得します：<img src={useBaseUrl("img/mainnet/polygon-instance.svg")} />

このマニュアルで問題に直面した場合には、 [問題](https://github.com/maticnetwork/matic-docs/issues) を開くか、 [PRの作成](https://github.com/maticnetwork/matic-docs/pulls) を [GitHub](https://github.com/maticnetwork/matic-docs)で気軽に行ってください。
