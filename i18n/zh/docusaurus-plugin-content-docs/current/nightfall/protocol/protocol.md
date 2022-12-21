---
id: protocol
title: Nightfall 协议
sidebar_label: Nightfall Protocol
description: "Nightfall 处理。"
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

我们假设该系统至少有 1 名提案者注册，发布了符合最低要求的权益。

## 交易发布 {#transaction-posting}
发布新交易的机制分为两种：

- [链上发布](#on-chain)
- [链下发布](#off-chain)

### 链上发布 {#on-chain}
该流程以交易者通过在 `Shield.sol` 上调用 `submitTransaction` 创建交易开始。交易者向 Shield 合约支付交易费用，金额由交易者自行决定。这笔费用将付给负责将交易打包进区块的提案者。目前，提案者及相关乐观者实例可选择收取更高的区块纳入费，跟矿工类似。
交易调用会触发区块链事件的发布，包括交易的详细信息。如果这是一笔存入交易，Shield 合约将收取相关的 L1 ERC 代币作为费用。

### 链下发布 {#off-chain}
转账和提现可选择直接向监听的提案者提交交易，而不是通过上面的流程链上提交。这样的链下交易将为交易者节省链上提交存款的成本（约 45k 燃料），但前提是交易者及其所选提案者之间存在较高的信任。不良提案者更容易审查链下收到的交易，因为这些交易并不会向所有监听中的提案者广播。在这种情况下，交易者应该等到冷却期（为期 1 周）结束后再将交易视为可信。

## 接受交易 {#transaction-acceptance}
当提案者收到任何交易时，都会进行一系列检查，以验证交易格式是否正确、是否已针对公开输入的哈希提供了验证证明。如果顺利通过所有检查，交易会被添加到提案者内存池，等待被纳入区块。

## 区块装配和提交 {#block-assembly-and-submission}
提案者等待 Shield 合约指定其为当前提案者。
当前提案者会在自己的内部乐观者实例中收到一个新区块，其中包含来自其内存池的交易。如果要将这些交易添加到 Shield 合约中，提案者将为每一笔交易计算新承诺的 Merkle 树。

因此，区块中将包含相关交易的哈希以及承诺 Merkle 树的根，后者将在处理完所有区块内交易后出现（承诺根）。然后提案者会将该区块发送至状态智能合约。

提案区块后，以下信息将被记录到链上：

- 区块数据结构
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
- 区块中的交易
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

## 挑战 {#challenges}
排队中的区块在为期一周的时间里可接受挑战，期内，人们可通过调用挑战函数来质疑其正确性。可提出的挑战包括：

- **INVALID_PROOF** - 交易中提供的证明不能验证为真；
- **INVALID_PUBLIC_INPUT_HASH** - 交易的公开输入哈希并非该公开输入的正确哈希；
- **HISTORIC_ROOT_EXISTS** - 用于创建该交易证明的承诺 Merkle 树的根从未存在；
- **DUPLICATE_NULLIFIER** - 作为交易的一部分给出的废弃值属于已花费废弃值清单；
- **HISTORIC_ROOT_INVALID** - 处理区块内交易而产生的更新后的承诺根不正确；
- **DUPLICATE_TRANSACTION** - 已有区块中含有与区块中交易完全相同的交易；
- **TRANSACTION_TYPE_INVALID** - 从交易类型（存入、转账、提现）来看，交易的格式不完善。

若挑战成功，也就是链上计算显示挑战有效，则将采取以下操作：

- 所涉区块的哈希和所有后续区块将从队列中移除。
- 提案者提交的区块权益被支付给挑战者。
- 向区块内交易的交易者退还原应支付给提案者的费用；如为存款交易，则任何由 Shield 合约持有的托管资金也会被退还。

