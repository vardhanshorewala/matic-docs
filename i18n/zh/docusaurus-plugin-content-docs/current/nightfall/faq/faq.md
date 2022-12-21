---
id: faq
title: 常见问题解答
sidebar_label: FAQ
description: 有关 Nightfall 的常见问题
keywords:
  - docs
  - polygon
  - nightfall
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip

如果您没有在此清单中找到您的问题，请在 <ins>**[Polygon Nightfall Discord 服务器](https://discord.com/invite/pZkC3JV2bR)**</ins>上提交您的问题。

:::

## 哪里能找到智能合约？ {#where-can-i-find-the-smart-contracts}

Polygon Nightfall 合约已部署在[测试网 Goerli](../deployments/testnet.md) 和[主网](../deployments/mainnet.md)上。

## Polygon Nightfall 安全性审计目前处于什么状态？ {#what-s-the-state-of-polygon-nightfall-s-security-audit}
Polygon Nightfall 目前正在进行安全性审计，计划将在第三季度内完成。与此同时，协议中增加了若干限制条件：

- 单一提案者运行，并且由 Polygon 负责管理
- [限制存入额和提现额](../tools/nightfall-wallet.md#deposit-and-withdraw-restrictions)

## 如何设置 Nightfall 钱包？ {#how-do-i-set-up-my-nightfall-wallet}
有关钱包的完整教程请参见[此处](../tools/nightfall-wallet.md)，包括如何开始使用 Polygon Nightfall 钱包的所有详细信息。

## 我该如何将账本硬件钱包连接到 Nightfall 钱包？ {#how-do-i-connect-a-ledger-hardware-wallet-to-nightfall-wallet}
钱包教程中有一节，专门介绍了[如何将账本硬件钱包连接到 Metamask](../tools/nightfall-wallet.md#how-to-connect-a-ledger-hardware-wallet-to-nightfall)。

## Polygon Nightfall 网络上的转账，从开始到完成需要花费多长时间？ {#how-long-do-transfers-take-on-polygon-nightfall-network-from-start-to-finish}
当前提案者获取用户交易，制作成最多包含 32 笔交易的区块。一旦收集到足够创建区块的交易，交易便会得到处理。

此外，区块的生成期设有上限，因此每 6 小时都至少会有一个区块得到提案（无论提案者收集到多少笔交易）。

## 我能和谁进行交易？ {#who-can-i-transact-with}
要在 Polygon Nightfall 内部转移资产，您只需要`Destination Wallet Address`。请参阅钱包教程，了解[如何共享钱包地址](../tools/nightfall-wallet.md#your-wallet-address)，以收取资金。

## 承诺在哪里进行备份？ {#where-are-commitments-backed-up}

零知识证明是通过浏览器计算的，因此您的密钥在您那里，钱包会在其 IndexedDb 中记录您拥有的所有承诺。任何有权访问此数据的人都能看到您拥有哪些承诺，不过他们没有密钥，因此无法窃取您的承诺。只有当您输入助记词时，密钥才会被解密。因此，您应该只在自己信任的设备上使用钱包。

目前该数据不能随意导出。因此，如果您在另一台设备上使用浏览器，将无法访问您的承诺，除非先转移 IndexedDB 内容。我们提供一种可供您通过钱包导出和导入承诺的机制。

## 交易隐私 {#privacy-of-transactions}
理解存入和提取交易的非隐私性质非常重要。这是因为这类交易需要与第 1 层进行交互，而第 1 层不具有隐私性。这意味着如果您创建第 2 层承诺，那么所有人都会知道这件事及其金额。与此类似，如果您通过销毁第 2 层承诺的方式，将一枚代币转回第 1 层，则所有人都会知道是谁收到了这笔转账、金额是多少。

隐私是完全通过第 2 层的内部转账实现的。从以太坊区块链的角度来看，这些交易具备完全的隐私性。唯一被泄露的数据是您在将转账交易发送到区块提案者时使用的地址。早期 Beta 版本的提案者仅由 Polygon 负责运营。


## 如何提取资金？ {#how-to-withdraw-funds}
资金可以通过 Polygon Nightfall 钱包提取。从包含提款交易的区块创建之日起，有为期**一周**的时间来完成提现。这段时期过去后，您就可以最终完成提现，将资金发送到以太坊账户。

## Nightfall 的交易成本是多少？ {#how-much-will-transactions-cost-on-nightfall}
交易分为两类，成本有所不同：

- 链上交易：这类交易被发送到智能合约，需要在以太坊上支付燃料费才能开采。任何提案者都可以将这类交易放入区块。目前，`deposit`和`finalize withdrawal`属于链上交易。
- 链下交易：这些交易被直接发送给提案者。现在，所有的`transfer`和`withdrawals`都被配置为链下交易。

## 我可以在 Nightfall 网络上使用哪些代币？ {#which-tokens-can-i-use-on-nightfall-network}
可用于 Nightfall 的代币如下：

- MATIC
- WETH
- DAI
- USDC

## 我是否需要 Matic 代币，才能使用 Nightfall？ {#do-i-need-matic-tokens-to-use-nightfall}
是的。您需要在 Nightfall 上存入一些 Matic 代币，才能支付`transfers`和`withdrawals`。

## 我可以在哪里提交错误报告，或者联系 Night Fall 以获得更多帮助？ {#where-can-i-submit-a-bug-report-or-contact-nightfall-for-additional-help}
我们建议您最好加入 [Polygon Nightfall Discord 服务器](https://discord.com/invite/pZkC3JV2bR)，然后提交您的问题。
