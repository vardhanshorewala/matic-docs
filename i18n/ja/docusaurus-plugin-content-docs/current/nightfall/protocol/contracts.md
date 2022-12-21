---
id: contracts
title: スマートコントラクト
sidebar_label: Smart Contracts
description: "シールド、プロポーザー、課題、MerkleTreeの計算。"
keywords:
  - docs
  - polygon
  - nightfall
  - smart
  - contracts
  - shield
image: https://matic.network/banners/matic-network-16x9.png
---

コントラクトでは、各Nightfallアクターがネットワークで動作するために従う必要があるルールを定義します。
スマートコントラクトは、次のものを含みます：

- [Shield.sol](#shield)
- [Proposers.sol](#proposers)
- [Challenges.sol](#challenges)
- [MerkleTree_Computations.sol](#merkletree_computations)

## シールド {#shield}
このコントラクトにより、ユーザーはプロポーザーによる処理のためのトランザクションを送信できます。デポジットトランザクションの場合はお支払いいただきます。
また、シールドコントラクトの状態（コミットメントルートリストとヌールファイアリスト）の更新を誰でもリクエストできます。
状態が更新されると、更新中のすべての退会が処理されます。

ブロックチェーンに転送を投稿したり、トランザクションを撤回したりする必要はありません。これは単に提案者がトランザクションを受け取り、レイヤー2ブロックに組み込むためのメッセージボードとして機能しているだけです。

Nightfallは実際のERCコントラクトと相互作用するため、次のチェックはプライベートにできません：

- **デポジット/出金**中、ERCトークンアドレスは有効です。
- **デポジット**中、ユーザーは残高を持つか、トークンを所有してコミットメントを作成します。

## プロポーザー {#proposers}
コントラクトには、提案者の登録、登録解除、支払い、回転、および新しいレイヤー2ブロックをブロックチェーンに提案する機能が含まれます。
Nightfallの最初のバージョンでは、Polygonによって操作されるシングルのブートプロポーザーのみが受け入れられます。次のバージョンでは、複数の提案者が許可されるこの制限が解除されます。

## 課題 {#challenges}
この機能を使用すると、ブロックが正しくないとしてチャレンジされることができます。

## MerkleTree_Stateless {#merkletree_stateless}
ブロックの課題をオンチェーン上で計算するために`Challenges.sol`が使用する元の`MerkleTree.sol`のステートレス（純粋な機能）バージョン。

## 他のコントラクト {#other-contracts}
- `Utils.sol` - 複数の契約で使用される機能、またはインラインのままにするとコードの可読性に影響する機能をまとめて収集します。
- `Config.sol` - Node.js設定ファイルのような定数を保持します。
- `Structures.sol` - グローバル構造、列挙、イベント、マッピング、および状態変数を定義します。これらを簡単に見つけることができます。

## アップグレード性 {#upgradability}
少なくとも初期には、Polygonは展開後にNightfall契約をアップグレードする機能を保持しています。
これを行うには、TruffleのOpenzeppelin[アップグレードプラグイン](https://docs.openzeppelin.com/upgrades-plugins/1.x/)を使用します。

Polygonは、[ディストリ](https://github.com/EYBlockchain/nightfall_3/tree/master/nightfall-deployer)ビュータモジュールを使用して契約をアップグレードします。
`deployer`には、移行フォルダに4つの移行が保存されています。
最初の3つの移行は、Polygon Nightfallコントラクトスイートの「通常」展開を実行します。ただし、すべてのコントラクト（ライブラリではなく）がプロキシを使用して展開されていることを確認し、後でアップグレードできるようにします。4回目の移行は、コントラクトのアップグレードに使用されます。
