---
id: faq
title: よくある質問
sidebar_label: FAQ
description: Nightfallに関するよくある質問
keywords:
  - docs
  - polygon
  - nightfall
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip

このリストに質問が見つからない場合は、<ins>**[Polygon Nightfallディスコードサ](https://discord.com/invite/pZkC3JV2bR)**</ins>ーバーに質問を送信してください。

:::

## スマートコントラクトはどこで入手できますか? {#where-can-i-find-the-smart-contracts}

Polygon Nightfallコントラクトは[、テストネットのGoerli](../deployments/testnet.md)と[メインネット](../deployments/mainnet.md)に展開されています。

## Polygon Nightfallのセキュリティ監査はどのような状態ですか? {#what-s-the-state-of-polygon-nightfall-s-security-audit}
Polygon Nightfallは現在、第3四半期中に完了する予定のセキュリティ監査を受けています。一方、プロトコルにはいくつかの制約事項が追加されています：

- Polygonによって実行および管理されるシングルのプロポーザー
- [入出金額の制限](../tools/nightfall-wallet.md#deposit-and-withdraw-restrictions)

## Nightfallウォレットはどのように設定すればよいですか？ {#how-do-i-set-up-my-nightfall-wallet}
[ここに](../tools/nightfall-wallet.md)、Polygon Nightfallウォレットの使い方に関するすべての詳細なウォレットチュートリアルがあります。

## 元帳ハードウェアウォレットをNightfallウォレットに接続するにはどうすればよいですか？ {#how-do-i-connect-a-ledger-hardware-wallet-to-nightfall-wallet}
ウォレットチュートリアルには、[元帳ハードウェアウォレットとMetamaskを接続する方法](../tools/nightfall-wallet.md#how-to-connect-a-ledger-hardware-wallet-to-nightfall)を説明するセクションがあります。

## Polygon Nightfallネットワークの転送には、最初から最後までどのくらい時間がかかりますか？ {#how-long-do-transfers-take-on-polygon-nightfall-network-from-start-to-finish}
現在のプロポーザーは、ユーザーからのトランザクションを受け取り、最大32のトランザクションのブロックを作成します。ブロックを構築するのに十分なトランザクションが集められ次第、取引が処理されます。

また、ブロック生成期間には上制限があり、少なくとも6時間ごとに1つのブロックが提案されます（プロポーザーによって収集されたトランザクションの数に関係なく）。

## 誰と取引できますか？ {#who-can-i-transact-with}
Polygon Nightfall内で資産を転送するには、`Destination Wallet Address`のみが必要です。ファンドを受け取るために[ウォレットアドレスを共有する方法](../tools/nightfall-wallet.md#your-wallet-address)については、ウォレットチュートリアルを参照してください。

## コミットメントのバックアップ先はどこですか? {#where-are-commitments-backed-up}

ゼロ·ナレッジの証明はブラウザで計算されるので、秘密キーはユーザの手元に残され、ウォレットはユーザが所有しているすべてのコミットメントをIndexedDbで追跡します。このデータにアクセスできる人なら誰でも、所有しているコミットメントを見つけることができます。ただし、鍵なしではコミットメントを盗むことはできません。鍵が復号化されるのは、ニーモニックを入力した場合だけです。そのため、ウォレットは信頼できる機械だけで使うべきです。

現在のところ、このデータはどこにもエクスポートされません。そのため、別のマシンでブラウザを使用している場合は、IndexedDBの内容を転送しない限り、コミットメントにアクセスできません。我々は、ウォレットを介してコミットメントをエクスポートおよびインポートするためのメカニズムを提供します。

## トランザクションのプライバシー {#privacy-of-transactions}
入出金取引はプライベートではないということを理解することが重要です。これは、レイヤー1とやり取り、レイヤー1はプライベートではないためです。つまり、レイヤー2のコミットメントを作成するかどうか、およびそのコミットメントに含まれる量は誰もが知っているということです。同様に、レイヤー2のコミットメントを破棄してトークンをレイヤー1に戻した場合、誰がどの程度受信したかは誰でも同様です。

プライバシーは、完全にレイヤー2内の転送に起因します。Ethereumのブロックチェーンの観点から見れば、これらは完全にプライベートです。ブロックプロポーザーに転送トランザクションを送信するときに、データが漏洩するのはIPアドレスだけです。初期のベータ版では、Polygonは唯一のプロポーザーを実行します。


## ファンドを引き出す方法は？ {#how-to-withdraw-funds}
Polygon Nightfallウォレットでファンドを引き出すことができます。出金は出金取引が含まれたブロックが作られた瞬間から**1週間の**最終確定期間があります。この期間が過ぎれば、出金を確定し、自分のEthereumアカウントにファンドを送ってもらうことができます。

## Nightfallでの取引にはいくらかかりますか? {#how-much-will-transactions-cost-on-nightfall}
異なるコストを負担する取引には、次の2種類があります：

- オンチェーントランザクション: このような取引はスマートコントラクトに送られ、Ethereumのガス代を採掘しなければならない。プロポーザーは誰でもこのトランザクションを受けてブロックに入れることができます。現在、`deposit`と`finalize withdrawal`はオンチェーントランザクションです。
- オフチェーントランザクション：これらのトランザクションは、プロポーザーに直接送信されます。現在、`transfer`と`withdrawals`はすべてオフチェーントランザクションとして設定されています。

## Nightfallネットワークではどのトークンを使用できますか？ {#which-tokens-can-i-use-on-nightfall-network}
Nightfallでは、次のトークンが動作します：

- Matic
- WETH
- DAI
- USDC

## Nightfallを使用するにはMATICトークンが必要ですか? {#do-i-need-matic-tokens-to-use-nightfall}
はい。`transfers`と`withdrawals`を支払うには、MATICトークンをNightfallにデポジットする必要があります。

## バグレポートを送信するか、Nightfallに連絡して追加のヘルプを入手するには、どこですればよいですか? {#where-can-i-submit-a-bug-report-or-contact-nightfall-for-additional-help}
最良の方法は、[Polygon Nightfallディスコードサーバー](https://discord.com/invite/pZkC3JV2bR)に参加して質問を送信することです。
