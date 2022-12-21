---
id: overview
title: 概要
sidebar_label: Overview
description: Nightfallの概要
keywords:
  - docs
  - polygon
  - nightfall
  - privacy
  - rollup
  - zk
image: https://matic.network/banners/matic-network-16x9.png
---

Polygonは近い将来、多くの企業がビジネスロジックを実行し、商品とサービスの取引を管理するためのスマート契約を通じて相互作用するビジョンを信じています。

Polygonは[Ernst&Young](https://blockchain.ey.com/)と共同で、Ethereumの利用を希望する企業のためのアクセシビリティとプライバシーを可能にするPolygon Nightfallという、プライバシーに焦点を当てたパブリックなレイヤー2ロールアップソリューションを提供しています。

## エンタープライズのためのZKプルーフプロトコル {#a-zk-proof-protocol-for-enterprises}

Polygon Nightfallは、[Polygon Hermez](https://polygon.technology/solutions/polygon-hermez/)、[Polygon Miden](https://polygon.technology/solutions/polygon-miden/)、および[Polygon Zero](https://polygon.technology/solutions/polygon-zero/)を含む、Polygonのスケーラビリティソリューションスイートの一部です。
重要な違いは、Nightfallが楽観的なロールアップとゼロナレッジ(ZK)暗号化の概念を組み合わせてプライベートで拡張可能なトランザクションを提供することで、企業のユースケースに合わせて設計されたプライバシーに焦点を当てたロールアップであることです。

Nightfallはスケーラビリティを可能にする一方、ブロックチェーンを利用する際に今日企業が直面している主要な障壁である取引のプライバシーの欠如も除去する予定です。Nightfallは、重要なトランザクションパラメータ（値や宛先など）がトレースバックできないように、プライバシーのレイヤーを追加します。この2つの機能は、Nightfallをビジネスロジックを実行し、持続可能な価格で分散型ネットワーク内のサプライチェーンと調整する方法として、セキュリティとプライバシーを維持するプライベート企業の関心を高めています。

## Nightfallの柱 {#nightfall-s-pillars}

PolygonNightfallの主な価値提案は、分散型ネットワーク内のデータの安全でプライベートで低コストな転送を可能にすることです。

![](../imgs/overview.png)

## プライバシー {#privacy}

Polygon NightfallはZK証明を使用してプライベートトランザクションを送信します。ユーザは、トランザクションの宛先や値などの主要なトランザクションパラメータを明らかにすることなく、トランザクションのZKプルーフを生成することができます。Nightfallのプライバシーコンポーネントの詳細については、[プロトコル](../protocol/protocol.md)ガイドを参照してください。

## セキュリティ
 {#security}

> Nightfallは現在セキュリティ監査が進行中であり、2022年6月中旬頃に完了するものと予想されます。
> 監査プロセスが完了すると、結果がここに表示されます。

> Nightfallは、ブートストラップ期間を持つ新しいネットワークとして、システムを保護するための一時的なセキュリティ対策があり、システムを削除して完全に分散型したままにします。

Polygon Nightfallは強力なパブリックブロックチェーンでセキュリティを借りてEthereumを活用するため、レイヤー2構築です。Nightfallは、資産のリカバリを保証する特定の前提条件に依存します。これらの前提条件は、ハッシュやシグニチャなどの特定の暗号化プリミティブを使用するZK-SNARKSを中心とするいくつかの設計およびアーキテクチャの決定に基づいています。最後に、Nightfallは運営者がユーザーのトランザクションを遮断せず、ユーザーがいつでも資産を引き出すことができるようにするために、異なるスマートコントラクトに運営規則を組み込みました。

要約すると、Nightfallは次のセキュリティ前提条件を作成します：

1. イーサリアムのセキュリティ前提。
2. Groth16の前提条件（指数前提条件の知識）。
3. ハッシュ（Poseidon）や署名などの原始からの特定の暗号仮定。
4. 正しい設計と実装に依存するソフトウェアセキュリティ前提条件。

## 効率 {#efficiency}

ブロックプロポーザーは、さまざまなユーザからトランザクションを収集し、それらをまとめてL2ブロックに配置します。
一般的なL2ブロックサイズには、約32のトランザクションが含まれます。

デポジット、振替、出金の予想ガス料金は9000、1200、9500です。このコストは、1トランザクションあたりのコールデータ574バイトと、L2ブロックを処理するための固定コールデータと計算によるものです。EIP4488以降のコストは[最大80%](https://eips.ethereum.org/EIPS/eip-4488)削減されます。

## 拒否できない転送 {#non-deniable-transfers}

転送トランザクションZKプルーフの一部として、Nightfallには、転送されたコミットを処理するために必要な秘密（トークンアドレス、値、ID、およびソルト）の暗号化が含まれます。これにより、ユーザは受信者に既知の鍵を使用して秘密を暗号化する必要があります。鍵はZKプルーフの一部であるため、レシーバは正しい暗号鍵が使用されたことを証明できるため、受信者はもっともらしい拒否性に依存します。

## 分散化 {#decentralization}

バリデータと[チャレンジャー](docs/nightfall/protocol/actors)は、Nightfallの不可欠な部分です。これにより、トランザクションとL2ブロックがタイムリーかつ正確に生成されます。ネットワークの次のプロポーザーを選択するために、プルーフオブステーク（PoS）ベースの[コンセンサスメカニズム](docs/nightfall/protocol/actors)が使用されます。一方、チャレンジャーは、不正なブロックが検出された場合に問題を提起し、プロポーザーが進行した持分を維持することで、ネットワークの正しい動作を監視します。


## 将来のプルーフ {#future-proof}
NightfallのOptimisticロールアップ実装が提供する柔軟性のおかげで、ZKでトランザクションを実装した新しい回路タイプを定義して登録するだけで、既存のトランザクションを損なうことなく、将来的に新しいトランザクションを含めることができます。

## 参照 {#references}

1. [ZKスケーリングに対する多角的なアプローチ](https://messari.io/article/polygon-a-multi-sided-approach-to-zk-scaling)
2. [Nightfallに関するPaul's Brodyの見解](https://www.linkedin.com/pulse/say-hello-nightfall-paul-brody-1f/)
