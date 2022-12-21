---
id: overview
title: 概述
sidebar_label: Overview
description: Nightfall 概述
keywords:
  - docs
  - polygon
  - nightfall
  - privacy
  - rollup
  - zk
image: https://matic.network/banners/matic-network-16x9.png
---

Polygon 相信，在不久的未来，许多企业会通过执行业务逻辑和管理商品和服务交换的智能合同来进行交互。

Polygon 与[安永](https://blockchain.ey.com/)联手推出名为 Polygon Nightfall 的以隐私为侧重点的公有第 2 层汇总解决方案，以期为希望使用以太坊的企业提供可及性和隐私性支持。

## 面向企业的 ZK-证明协议 {#a-zk-proof-protocol-for-enterprises}

Poligon Nightfall 是一整套 Polygon 可扩展性解决方案的一部分，包括
[Polygon Hermez](https://polygon.technology/solutions/polygon-hermez/)、
[Polygon Miden](https://polygon.technology/solutions/polygon-miden/)
和[ Polygon Zero](https://polygon.technology/solutions/polygon-zero/)。
Nightfall 主要区别在于它是以隐私为重点的汇总，旨在针对企业用例，通过乐观汇总和零知识 (ZK) 加密等概念的结合，实现具有隐私性、可扩展的交易。

Nightfall 在实现扩容的同时还解决了企业当前在利用区块链时面临的一项主要障碍：交易缺乏隐私性。Nightfall 通过添加隐私层，使关键交易参数（如价值和目的地）无法追溯。这两个功能激发了私营企业的兴趣，它们将 Nightfall 视为一种以可持续的价格执行其业务逻辑，并在去中心化的网络中协调供应链的方式，与此同时还能保持安全和隐私。

## Nightfall 的几大支柱 {#nightfall-s-pillars}

Polygon Nightfall 的主要价值主张是在去中心化的网络中实现安全、私有、低成本的数据传输。

![](../imgs/overview.png)

## 隐私 {#privacy}

Polygon Nightfall 利用 ZK 证明来发送私人化的交易。用户可以生成交易的 ZK 证明，无需泄露交易目的地和交易价值等关键交易参数。更多有关 Nightfall 隐私组件的详细信息，请参见[协议](../protocol/protocol.md)指南。

## 安全性 {#security}

> Nightfall 目前正在接受安全性审核，预计将于 2022 年 6 月中旬完成。审核流程完成后，我们将于此处公布结果。

> 作为一个处于启动期的全新网络，Nightfall 实施了过渡性安全性措施，旨在保护系统，目的是将它们移除，并实现完全的去中心化。

Polygon Nightfall 属于第 2 层建构，因为它通过借用以太坊作为公链的安全性对其加以利用。Nightfall 依靠某些假设来保证资产追回。这些假设以围绕 ZK-SNARKS 的几项设计和构建为基础，利用了哈希算法和签名算法等密码学原语。最后，Nightfall 将运营规则纳入各种智能合约，以保证运营者不会阻止用户交易，以便用户随时随地对资产进行提取。

综上，Nightfall 的运行基于以下几点安全性假设：

1. 以太坊的安全性假设。
2. Groth16 假设（指数知识假设）。
3. 某些来自密码学原语的假设，如哈希算法（Poseidon）和签名算法。
4. 安全性假设依靠正确的设计实施。

## 效率 {#efficiency}

区块提案者从不同用户处收集交易，并将其批量打包进 L2 区块。
典型的 L2 区块大小包含约 32 个交易。

存入、转账和提现所需的燃料成本预计分别为 9000、1200 和 9500。这一成本用于存储每笔交易 574 个字节的调用数据，加上一些固定调用数据和用于处理 L2 区块的计算。[EIP 4488](https://eips.ethereum.org/EIPS/eip-4488) 提案推出后，
成本至多可降低 80 %。

## 不可否认的转账 {#non-deniable-transfers}

作为 ZK 证明的一部分，Nightfall 会对处理承诺转移所需的保密信息（代币地址、价值、ID 和加密盐）进行加密。这使用户不得不使用接受者已知的密钥对保密信息进行加密。密钥是 ZK 证明的一部分，接受者依赖于合理的否认，因为发送者能够证明使用了正确的加密密钥。

## 去中心化 {#decentralization}

验证者与[挑战者](docs/nightfall/protocol/actors)都是 Nightfall 的有机组成部分。他们确保交易和 L2 区块以及时和正确的方式生产。基于权益证明 (PoS) 的共识机制被用来选择网络的下一个[提案者](docs/nightfall/protocol/actors)。一方面，挑战者负责监督网络正确运行，在检测到错误的区块时，提出挑战，并扣押由提案者提出的权益。


## 前瞻性 {#future-proof}
得益于 Nightfall 的乐观汇总实施，我们未来有可能纳入新交易，但不以牺牲现有交易为代价，而是仅仅定义和注册实施 ZK 交易的新型回路。

## 参考资料 {#references}

1. [多维度的 ZK 扩容方法](https://messari.io/article/polygon-a-multi-sided-approach-to-zk-scaling)
2. [Paul Brody 对 Nightfall 的设想](https://www.linkedin.com/pulse/say-hello-nightfall-paul-brody-1f/)
