---
id: nightfall-wallet
title: Nightfallウォレット
sidebar: Nightfall Wallet
description: "Polygon Nightfallウォレットガイド。"
keywords:
  - docs
  - matic
  - polygon
  - nightfall
  - wallet
image: https://matic.network/banners/matic-network-16x9.png

---

Polygon Nightfallウォレットは、Nightfallメインネットベータリリースと相互作用できるブラウザウォレットです。

:::info Nightfallウォレットを使用して、デポジット、転送、引き出しを行います

### 制限 {#restrictions}

Nightfallが成熟した状態になる間、次の制約事項が適用されます：


| ERC20トークン | 最大デポジット | 最大引き出し |
|-------------|-------------|--------------|
| Matic | 250 MATIC | 1000 MATIC |
| WETH | 0.25 WETH | 1 WETH |
| DAI | 250 DAI | 1000 DAI |
| USDT | 250 USDT | 1000 USDT |
| USDC | 250 USDC | 1000 USDC |

:::

:::caution セキュリティ対策

NightfallウォレットはChromeブラウザでテストされます。ベータ版の間は、他のブラウザで走行距離が異なる場合があります。

**ChromeでNightfallを使用することを強くお勧めします**。

:::



## はじめに {#getting-started}

Polygon Web[メインネットウォレット](https://wallet-beta.polygon.technology)または[テストネットウォレット](https://wallet.testnet.polygon-nightfall.technology/)にアクセスし、MetaMaskアカウントを接続し、左側のPolygonウォレットを選択します。MetaMaskに関するヘルプが必要な場合は、[MetaMaskのPolygonドキュメントを参照してください](../../develop/metamask/tutorial-metamask.md)

![](../imgs/tools-wallet/polygon-wallet-click-nf.png)

この時点で、ウォレットからPolygonネットワークに切り替えるように要求され、Metamaskポップアップがスイッチの確認をリクエストします。

![](../imgs/tools-wallet/polygon-network.png)

次に、一番上のウォレットセクションでドロップダウンメニューをクリックし、`Polygon Nightfall`を選択すると、Ethereumメインネットに切り替える新しいリクエストが表示されます。Polygon Nightfallで動作するEthereumメインネットへの切り替えに同意してください。

![](../imgs/tools-wallet/polygon-network-dropdown-nf.png)

テストネットで作業している場合は、すぐにPolygon NightfallウォレットのランディングページにウォレットURLが表示されます。

![](../imgs/tools-wallet/wallet-main-screen.png)

最初の訪問時には、Nightfallウォレットを作成する必要があります。ニーモニックを生成してウォレットを作成するためのポップアップが表示されます。`Generate Mnemonic`、`Create Wallet`の順にクリックしてください。**このウォレットは、現在のデバイスでのみ使用できることに注意してください**。

![](../imgs/tools-wallet/generate-mnemonic-create-wallet.png)

:::caution コミットメントとニーモニックのバックアップ

ウォレットキーとトランザクションはブラウザ（IndexedDb）に保存されます。Nightfallウォレットに初めてアクセスするときに設定するニーモニックと同じです。

このニーモニックは必ず安全な場所に保管してください。L2でファンドと互換性のある証明を作成できる唯一の方法です。コミットメントも同じです。他のブラウザやマシンを使用するときは必ず`export commitments`を押して安全に保存してください。

:::

**コミットメントを失えば、ファンドは永遠に失われます**


この時点で、 MetamaskとNightfallウォレットアドレス(右上)の両方を見ることができます。

**トランザクションをスタートする前に、ウォレットのセットアップが完了するまであと数分お待ちください**。

ウォレットの左下の角に、ウォレットの状態が`Syncing Nightfall`と表示されます。この状態では、ウォレットはトランザクションの実行に必要なZK回路線とネットワーク状態を取得しています。

![](../imgs/tools-wallet/wallet-state-syncing.png)

ウォレットのステータスが`Nightfall Synced`に変わるまでお待機ください

![](../imgs/tools-wallet/wallet-state-synced.png)


## 元帳ハードウェアウォレットをNightfallに接続する方法 {#how-to-connect-a-ledger-hardware-wallet-to-nightfall}
[こちら](https://support.ledger.com/hc/en-us/articles/4404366864657-How-to-access-your-Ledger-Ethereum-ETH-account-via-Metamask?docs=true)のMetamask公式サイトに、元帳ハードウェアウォレットとMetamaskを接続するためのガイドがあります。

ウォレットの中のEthereumアプリを必ず接続し、Ethereumアプリ設定で「ブラインドサイン」が可能になるようにします。


### ウォレットアドレス {#your-wallet-address}
`Receive`をクリックして、Nightfall資産ページからNightfallウォレットアドレスを取得します。

![](../imgs/tools-wallet/nightfall-wallet-address.png)

## デポジットの作成方法 {#how-to-make-deposits}
Nightfall資産ページで、選択した資産の右側にある`Deposit`ボタンをクリックするか、L2ブリッジページに移動します。

1. 転送モードが`Deposit`に設定されていることをチェックしてください
2. 目的のトークンが選ばれたことをチェックしてください（WETH、MATICなど）。
3. Nightfallウォレットに入金する値を入力し、`Transfer`をクリックしてください
4. ポップアップでトランザクションを確認します
5. `Create Transaction`をクリックしてください

![](../imgs/tools-wallet/deposit-click-transfer.png)

ZKPを計算し、トランザクションを準備するプロセスが開始されます(Metamaskにアカウント残高へのアクセスを許可します)。これが終了したら、`Send Transaction`（Metamaskにコントラクトのやり取りのための追加権限を付与）をクリックしてください。

![](../imgs/tools-wallet/deposit-tx-created-and-ready-to-be-sent.png)

「トランザクション」ページにアクセスして[デポジットを確認](#view-transactions)してください。

### デポジットに関する重要情報 {#important-information-about-deposits}
- ベータ版にある間は、[デポジット金額が制限されます](#note-the-following-deposit-and-withdrawal-restrictions)

## 転送の方法 {#how-to-make-transfers}
Nightfall資産ページで、選択した資産の右側にある`Send`ボタンをクリックしてください。

1. Polygon Nightfall L2に有効なアドレスを入力してください
2. 目的のトークンが選ばれたことをチェックしてください（WETH、MATICなど）。
3. Nightfallウォレットから転送する値を入力し、`Continue`をクリックしてください

![](../imgs/tools-wallet/send-nf.png)

ZKPを計算し、トランザクションを準備するプロセスが開始されます。これが終了したら、`Send Transaction`をクリックしてください。

「トランザクション」ページにアクセスして[転送](#view-transactions)を確認してください。

### 転送に関する重要情報 {#important-information-about-transfers}
Nightfallで使用されている現在のZKP転送回路は、転送量を既存のコミットのいずれかの値と正確に一致させるか、または2つの既存のコミットの任意の線形結合に制限します。

例を使用して転送制限を説明するには、次のコミットメントセットに従ってください：

- セットA：[1、1、1、1、1、1]
- セットB：[2、2、2]
- セットC：[2、4]

3つのセットの合計はすべて6ですが、次の転送だけが使用可能です：

- セットA：0~2の間の任意の転送（両方とも除外）
- セットB：0~4の間の任意の転送（両方とも除外）
- セットC：0~6の間の任意の転送（両方とも除外）

この例を続けるために、AlexがCセットのコミットメントを所有している場合、使用可能な転送には両方の制限値を除き、0~6の任意の金額が含まれます。AlexがBobに3.5を転送することを決めた場合、Alexは2.5のシングルコミットメントを持ち、Bobはブロックが提案されると3.5のコミットメントを受け取ります。

一方、AlexがBobに金額6を転送することを決めた場合、有効なコミットメントの組み合わせがないため、ZKプルーフは失敗します。

これらの値は、預金のようなものではなく、**所有しているコミットメントを表していることに注意することが重要です**。これらのドキュメントの[コミットメント](../protocol/commitments.md)のセクションにある詳細情報を参照してください。

## 引き出しの方法 {#how-to-make-withdrawals}
Nightfall資産ページで、選択した資産の右側にある`Withdraw`ボタンをクリックするか、L2ブリッジページに移動します。

1. 転送モードが`Withdraw`に設定されていることをチェックしてください
2. 目的のトークンが選ばれたことをチェックしてください（WETH、MATICなど）。
3. Nightfallウォレットから引き出す値を入力し、`Transfer`をクリックしてください
4. ポップアップでトランザクションを確認します
5. `Create Transaction`をクリックしてください

ZKPを計算し、トランザクションを準備するプロセスが開始されます。これが終了したら、`Send Transaction`をクリックしてください。

「トランザクション」ページにアクセスして[引き出しを確認](#view-transactions)してください。最終確定期間が1週間が過ぎれば、ユーザーが確定し、引き出し額を請求できるようになります。

### 引き出しに関する重要情報 {#important-information-about-withdrawals}
- 引き出す値は、所有するコミットメントのいずれかの金額と正確に一致する必要があります（[コミットメント](#learn-about-commitments)の詳細）。
- 引き出すは引き出すトランザクションが含まれたブロックが作られた瞬間から**1週間**の最終確定期間があります。この期間が過ぎれば、出金を確定し、自分のEthereumアカウントにファンドを送ってもらうことができます。
- ベータ版の場合、[引き出し金額が制限されます](#note-the-following-deposit-and-withdrawal-restrictions)
- 引き出しはオンチェーントランザクションであり、トランザクションリクエスト時と引き出しが確定した時にガス代を支払います。

![](../imgs/tools-wallet/cooling-off-vs-ready.png)

## トランザクションの表示 {#view-transactions}
「トランザクション」ページでデポジット、転送、引き出しの状況をチェックしてください。各トランザクションは、ブロックを生成するのに十分なトランザクション量があるか、6時間後に処理されることに注意してください。

![](../imgs/tools-wallet/transactions.png)
