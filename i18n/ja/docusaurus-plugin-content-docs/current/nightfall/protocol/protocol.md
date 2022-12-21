---
id: protocol
title: Nightfallプロトコル
sidebar_label: Nightfall Protocol
description: "Nightfallプロセス。"
keywords:
  - docs
  - polygon
  - nightfall
  - protocol
  - chain
  - block
  - structure
  - layer
image: https://matic.network/banners/matic-network-16x9.png
---

少なくとも1人のプロポーザーがシステムに登録し、最小のステークを投稿していると想定しています。

## トランザクション投稿 {#transaction-posting}
新しいトランザクションをポストするには、次の2つのメカニズムがあります：

- [オンチェーン](#on-chain)
- [オフチェーン](#off-chain)

### オンチェーン {#on-chain}
このプロセスは、トランザクタが`submitTransaction`コールを発信して`Shield.sol`トランザクションを作成することから始まります。トランザクターは、トランザクションのためのシールドコントラクトに手数料を支払います。これは、トランザクターが決定するすべてのものになる可能性があります。これは、ブロック内のトランザクションを組み込んだプロポーザーに支払われます。現在のところ、プロポーザーと基礎となるOptimistのインスタンスは、鉱山労働者が行うのとほぼ同じように、ブロックに組み込むためにより高い料金を選択する可能性が高いです。
トランザクションコールによって、その詳細情報を含むブロックチェーンイベントが投稿されます。デポジットの場合、シールドコントラクトは問題のレイヤー1ERCトークンの支払いを受けます。

### オフチェーン {#off-chain}
転送、引き出しは、上記のプロセスを介してオンチェーンで提出されるよりは、直接リッスン提案者に提出されるオプションがあります。このようなオフチェーントランザクションは、トランザクターがデポジット（約45,000ガス）のオンチェーン提出費用を節減することができるが、トランザクターとトランザクターが接続することに選択したプロポーザー間のより大きな信頼が必要です。悪役プロポーザーは、すべてのリスニングプロポーザーにこのようなトランザクションが放送されるわけではないため、オンチェーンで受信したトランザクションよりもオフチェーンで受信した取引を検閲しやすいです。この場合、トランザクターは、冷却期間（1週間）が経過した場合にのみ、トランザクションを信頼できると考えるべきです。

## トランザクションの受理 {#transaction-acceptance}
プロポーザーは、トランザクションを受信すると、さまざまなチェックを実行して、トランザクションが適切に形成されていること、およびパブリック入力ハッシュに対してプルーフが検証されていることを検証します。
すべてのチェックに合格すると、トランザクションはプロポーザーのメンプールに追加され、ブロック内で考慮されます。

## ブロックの組み立てと提出 {#block-assembly-and-submission}
プロポーザーは、シールドコントラクトが彼らを現在の提案者として割り当てるまで待機します。現在のプロポーザーは、自身の内部Optimistインスタンスから、そのメンプールからのトランザクションを含む新しいブロックを受信します。各トランザクションについて、これらのトランザクションがシールドコントラクトに追加される場合に発生する新しいコミットメントMerkle Treeを計算します。

したがって、ブロックには、ブロックに含まれるトランザクションのハッシュと、ブロック内のすべてのトランザクション（コミットメントルート）を処理した後に存在するコミットメントMerkle Treeルートが含まれます。その後、プロポーザーはこのブロックを状態のスマートコントラクトに送信します。

ブロックが提案されると、次の情報がオンチェーンに記録されます：

- データ構造ブロック
```
  struct Block {
    uint48 leafCount; // note this is defined to be the number of leaves BEFORE the commitments in this block are added
    address proposer;
    bytes32 root; // the 'output' commitment root after adding all commitments
    uint256 blockNumberL2;
    bytes32 previousBlockHash;
    bytes32 transactionHashesRoot;
  }
```
- ブロック内のトランザクション
```
    struct Transaction {
        uint112 value;
        uint112 fee;
        TransactionTypes transactionType;
        TokenType tokenType;
        uint64[2] historicRootBlockNumberL2; // number of L2 block containing historic root
        uint64[2] historicRootBlockNumberL2Fee; //number of L2 block containing historic root fee
        bytes32 tokenId;
        bytes32 ercAddress;
        bytes32 recipientAddress;
        bytes32[2] commitments;
        bytes32[2] nullifiers;
        bytes32[1] commitmentFee;
        bytes32[2] nullifiersFee;
        bytes32[2] compressedSecrets;
        uint256[4] proof;
    }
```

## 課題 {#challenges}
ブロックは1週間キュー内でチャレンジ可能になります。その時間、チャレンジングな関数の1つを呼び出すことによって、ブロックの正確性がチャレンジされる可能性があります。実行できる課題は次のとおりです：

- **INVALID_PROOF** - トランザクションで提供されたプルーフが真であることを確認できません。
- **INVALID_PUBLIC_INPUT_HASH** - トランザクションのパブリック入力ハッシュは、パブリック入力の正しいハッシュではありません。
- **HISTORIC_ROOT_EXISTS** - トランザクションプルーフの作成に使用されるコミットメントMerkle Treeのルートは存在しません。
- **DUPLICATE_NULLIFIER** - トランザクションの一部として指定されたヌルイファイヤは、使用済みヌルイファイヤのリストに存在します。
- **HISTORIC_ROOT_INVALID** - ブロック内のトランザクションを処理した結果、更新されたコミットメントルートが正しくありません。
- **DUPLICATE_TRANSACTION** - このブロックに含まれる同一のトランザクションは、すでに以前のブロックに含まれています。
- **TRANSACTION_TYPE_INVALID** - トランザクションタイプ（例:デポジット、転送、引き出し）に基づいてトランザクションが適切に形成されていません。

チャレンジが成功した場合、すなわち、オンチェーン計算によって有効なチャレンジであることが示されると、次のアクションが実行されます：

- 問題のブロックのハッシュとそれ以降のすべてのブロックがキューから削除されます。
- プロポーザーが提出したブロックステークはチャレンジャーに支払われます。
- ブロック内にトランザクションがあるトランザクターは、プロポーザーに支払った手数料と、デポジットトランザクションの場合にシールドコントラクトによって保持されているすべての秘密ファンドで償還されます。

