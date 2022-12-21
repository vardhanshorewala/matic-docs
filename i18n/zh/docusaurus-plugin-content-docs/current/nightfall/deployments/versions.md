---
id: versions
title: 历史记录
sidebar_label: History of changes
description: "部署的版本"
keywords:
  - docs
  - polygon
  - nightfall
  - changelog
image: https://matic.network/banners/matic-network-16x9.png
---


## Beta 1.0 {#beta-1-0}
Beta 1.0 已于 2022 年 5 月 17 日发布。它包括使用 Nightfall 概念验证的基本机制。
它支持单一`Proposer`和初次`coarse`交易实施。它还提供初级版本的用户钱包。部署版本见[此处](https://github.com/EYBlockchain/nightfall_3/commit/bc3e475de3e2877f14430f9599e5b38ea960765b)

## Beta 2.0 {#beta-2-0}
部署版本见[此处](https://github.com/EYBlockchain/nightfall_3/commit/4c2af01ac95af5ea6f5b40071d73a1624f06ba46)
已做出的改进如下：
- **收费**

供提案者收取交易费用的功能。此功能将激励产生多个提案者。
- **挑战者部署**

网络现已包括负责监督提案者区块的挑战者。
- **建立交易回路**

在生成任何交易的 ZKP 时，更灵活、性能更强大。`transfer`和`withdrawal`均可接受最多两个承诺和返回更改。
在性能方面，经过优化，验证交易所花费的时间现已有所缩短。

| 操作 | 此前的约束条件 | 此后的约束条件 |
|-----------|--------------------|------------------|
| 存入 | 84,766 | 1277 |
| 转账 | 499,119 | 67,694 |
| 提取 | 168,883 | 53,348 |

一部分优化是通过转用 Poseidon 算法实现的

- **保密信息加密**

我们已从 El-Gamal 转向 [KEM-DEM](../protocol/secrets) 加密流程。后者具有若干优点：
- 简化加密/解密处理
- 减少约束条件和链上燃料成本。

- **挑战者部署**

