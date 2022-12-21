---
id: contracts
title: 智能合约
sidebar_label: Smart Contracts
description: "Shield、提案者、挑战和 Merkle 树计算。"
keywords:
  - docs
  - polygon
  - nightfall
  - smart
  - contracts
  - shield
image: https://matic.network/banners/matic-network-16x9.png
---

合约定义了每个 Nightfall 参与者在网络中操作时需要遵守的规则。智能合约包括：

- [Shield.sol](#shield)
- [Proposers.sol](#proposers)
- [Challenges.sol](#challenges)
- [MerkleTree_Computations.sol](#merkletree_computations)

## Shield {#shield}
这种合约让用户提交交易，供提案者处理。如果是一笔存入交易，它将收取付款。
它还可供任何人请求更新 Shield 合约的状态（承诺根和废弃值清单）。
当状态更新时，该更新中的任何提现都将得到处理。

在区块链上发布转账或提现交易不是必须的：区块链充当的仅仅是留言板的角色，供提案者取得交易并将其打包到第 2 层区块中。

由于 Nightfall 会与实际的 ERC 合约进行交互，以下几类检查不能享有私密性：

- **存款/提现**流程中，有关 ERC 代币地址有效性的检查。
- **存款**流程中，有关用户是否有足够余额，或拥有可用于创建承诺的代币的检查。

## 提案者 {#proposers}
合约中包含注册、取消注册、支付和轮换提案者的功能，以及向区块链发布新 L2 区块的功能。第一版 Nightfall 仅接受由 Polygon 负责管理的单一启动提案者。在后面的版本中，这一限制将被取消，允许多个提案者。

## 挑战 {#challenges}
该功能允许人们挑战区块的正确性。

## MerkleTree_Stateless {#merkletree_stateless}
原始 `MerkleTree.sol`的无状态（纯功能性）版本，供 `Challenges.sol` 使用，帮助计算链上区块挑战。

## 其他合约 {#other-contracts}
- `Utils.sol` - 用于收集功能，这些功能抑或会在多个合约中使用，抑或会影响代码的可读性（若保留在系统内）。
- `Config.sol` - 用于保存常量，类似于 Node.js 配置文件。
- `Structures.sol` - 用于定义全局结构、枚举、事件、映射和状态变量。让这些内容更易于查找。

## 可升级性 {#upgradability}
至少在一开始，Polygon 保留在部署后升级 Nightfall 合约的能力。
我们使用适用于 Truffle 的 Openzeppelin [升级插件](https://docs.openzeppelin.com/upgrades-plugins/1.x/)进行此操作。

Polygon 使用[部署者](https://github.com/EYBlockchain/nightfall_3/tree/master/nightfall-deployer)模块来升级合约。
`deployer`在迁移文件夹中存有 4 个迁移。
前三个迁移执行 Polygon Nightfall 合约套件的“正常”部署。但是，它们确实确保所有合约（但不等于所有库）都使用代理进行部署，从而确保它们日后能够升级。第四个迁移用于升级合约。
