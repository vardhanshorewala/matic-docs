---
id: circuits
title: 回路和交易
sidebar_label: Circuits and Transactions
description: "Nightfall 上的回路类型"
keywords:
  - docs
  - polygon
  - nightfall
  - circuits
  - deposit
  - transfer
image: https://matic.network/banners/matic-network-16x9.png
---

正确的交易必须遵循由“回路”定义的规则。回路大致分为三类，每类交易都对应着一类回路：

- [存入](#deposit)
- [转账](#transfer)
- [提取](#withdraw)

每项交易都包含一个 ZK 证明，须符合回路中规定的约束条件。用户使用钱包
或通过客户端服务创建这一证明。
只有在以下所有命题均为真的情况下，才能生成证明：

- 新[承诺](./commitments#what-are-commitments)有效
- 旧[承诺](./commitments#what-are-commitments)有效，且由发送者拥有
- [废弃值] (./commitments#what-are-nullifiers) 有效
- Merkle 树路径/根有效
- 包含承诺的密文有效


## 存入 {#deposit}
存款是指将公开可见的 ERC 代币转换为价值或代币 ID 都与原始代币相同的代币承诺，该承诺中还包含承诺所有者的 Nightfall 公钥。

存款的 ZK 证明用于证明证明者已创建有效承诺$Z_A$ with a public key $pk_A$。

然后回路将检查 $Z_A$ == H(@ | ɑ | $pk_A$| σ)
存款交易的公开信息包括已铸入新承诺的地址，以及所使用的 ERC 代币的地址和价值。

![](../imgs/deposit.png)

## 转账 {#transfer}
转账实现同一资产的两项承诺在双方之间传递，即废弃此前的承诺，然后再创建最多两项新承诺：
- 其中一项将发送给接受者，其价值等于转账额
- 另一项承诺的价值等于价值变动（用掉的承诺价值之和减去转账的价值），由发送方拥有。

转账 ZK 证明用于证明证明者已废弃最多两个 Merkle 树中存在的旧承诺，创建了一个新承诺，并为接收者加密其信息。

在两种情况下，公布的信息都将是：某个以太坊地址已废弃承诺池中由发送人拥有的承诺，并已创建新承诺。而有关新所有人、哪些承诺已花费，或转账额的信息则将保持私密性。

第一张图介绍了废弃现有承诺，并将信息添加到`transaction`数据结构中的步骤。

![](../imgs/transfer_a.png)

第二张图介绍了生成和加密新创建的承诺所需的步骤。

![](../imgs/transfer_b.png)

## 提取 {#withdraw}
提现是指废弃现有 Nightfall 承诺，并将其转换为公开可见的 ERC 代币的操作。后者的价值和代币 ID 均与已销毁的承诺相同。提取是与存入相反的操作。与转账类似，提现接受最多两项承诺作为输入。

提现 ZK 证明用于证明证明者已废弃最多两项存在于 Merkle 树中的旧承诺。

提现流程中发布的信息包括撤回承诺的地址和被提现的代币的价值/代币 ID 和地址。

![](../imgs/withdraw.png)

### 冷却期 {#cooling-off-period}

提现需要经历为其一周的`COOLING OFF`期才能完成。这是因为 Nightfall 具有乐观性质，在某些挑战者提交欺诈证明之前，它一直假设新区块是正确的。资金将先被持有长达一周的时间，然后才能被提取到 L1。

# 费用 {#fees}

提案者负责将新交易汇总到 L2 区块中，来换取费用。支付给提案者的费用分为两类，具体取决于交易：
- 存入交易直接在 L1 中用以太币付费。
- 转账和提现交易在 L2 中用 MATIC 支付费用。
