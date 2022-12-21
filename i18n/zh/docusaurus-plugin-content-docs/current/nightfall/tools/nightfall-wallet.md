---
id: nightfall-wallet
title: Nightfall 钱包
sidebar: Nightfall Wallet
description: "Polygon Nightfall 钱包指南。"
keywords:
  - docs
  - matic
  - polygon
  - nightfall
  - wallet
image: https://matic.network/banners/matic-network-16x9.png

---

Polygon Nightfall 钱包是一种浏览器钱包，可以与Nightfall 主网 beta 版本进行交互。

:::info 使用 Nightfall 钱包存款、转账和提现

### 限制 {#restrictions}

当 Nightfall 达到成熟状态时，以下限制将适用：


| ERC20 代币 | 存入上限 | 提取上限 |
|-------------|-------------|--------------|
| MATIC | 250 枚 MATIC 代币 | 1000 枚 MATIC 代币 |
| WETH | 0.25 枚 WETH | 1 枚 WETH |
| DAI | 250 枚 DAI | 1000 枚 DAI |
| USDT | 250 枚 USDT | 1000 枚 USDT |
| USDC | 250 枚 USDC | 1000 枚 USDC |

:::

:::caution 安全性措施

Nightfall 钱包在 Chrome 浏览器上经过测试。在 Beta 版中，其他浏览器上的里程可能有所不同。

**我们强烈建议您在 Chrome 上使用 Nightfall**。

:::



## 快速入门 {#getting-started}

访问 Polygon Web [主网钱包](https://wallet-beta.polygon.technology)或[测试网钱包](https://wallet.testnet.polygon-nightfall.technology/)，连接您的 Metamask 账户并选择左侧的 Polygon 钱包。如果您在 MetaMask 方面需要帮助，请参阅[Metamask 上的 Polygon 文档](../../develop/metamask/tutorial-metamask.md)

![](../imgs/tools-wallet/polygon-wallet-click-nf.png)

此时，钱包将提示您切换到 Polygon 网络，然后出现 Metamask 弹出窗口，要求您确认切换。

![](../imgs/tools-wallet/polygon-network.png)

接下来，在钱包部分的顶部点击下拉菜单并选择 `Polygon Nightfall`，会出现一个切换至以太坊主网的新请求。请接受，以切换至以太坊主网用 Polygon Nightfall 进行操作。

![](../imgs/tools-wallet/polygon-network-dropdown-nf.png)

如果您使用测试网，钱包 URL 会立即将您转至 Polygon Nightfall 钱包的登陆页。

![](../imgs/tools-wallet/wallet-main-screen.png)

首次访问时，您必须先创建 Nightfall 钱包。会出现一个弹出窗口，帮助您生成助记词，并创建钱包。点击 `Generate Mnemonic`，然后 `Create Wallet`。**请注意，您只能在当前设备上使用此钱包**。

![](../imgs/tools-wallet/generate-mnemonic-create-wallet.png)

:::caution 备份您的承诺和助记词

钱包密钥和交易都存储在浏览器 (IndexedDb) 中。与您初次访问 Nightfall 钱包时设置的助记词一样。

请务必将该助记词保存在安全的地方。这是生成匹配您的 L2 资金的证据的唯一方法。您的承诺也一样：请务必妥善保存，每当您使用另一个浏览器或另一台设备时，都要记得按下`export commitments`。

:::

**如果您丢失了承诺，就会永久性失去资金**


此时，您应该能够看到您的 Metamask 和 Nightfall 钱包地址（右上方）。

**在开始交易之前，请先用几分钟时间完成钱包设置**。

在钱包的左下角，钱包的状态显示为`Syncing Nightfall`。在这种状态下，钱包正在追溯执行交易所需的 ZK 回路和网络状态。

![](../imgs/tools-wallet/wallet-state-syncing.png)

请等待钱包状态变为 `Nightfall Synced`

![](../imgs/tools-wallet/wallet-state-synced.png)


## 如何将账本硬件钱包连接到 Nightfall {#how-to-connect-a-ledger-hardware-wallet-to-nightfall}
请参阅[此处](https://support.ledger.com/hc/en-us/articles/4404366864657-How-to-access-your-Ledger-Ethereum-ETH-account-via-Metamask?docs=true)的指南，了解如何在 Metamask 官方站点中将您的账本硬件钱包连接到 Metamask。

请确保连接钱包中的以太坊应用，并在以太坊应用的设置中启用“盲签名”。


### 钱包地址 {#your-wallet-address}
在 Nightfall 资产页中点击 `Receive`，获取您的 Nightfall 钱包地址。

![](../imgs/tools-wallet/nightfall-wallet-address.png)

## 如何存款 {#how-to-make-deposits}
在 Nightfall 资产页中点击选定资产右侧的 `Deposit` 按钮，或导航至 L2 桥接页。

1. 检查转账模式是否设置为 `Deposit`
2. 检查是否已选中您希望使用的代币（WETH、MATIC 等）
3. 输入您希望存入 Nightfall 钱包的价值，点击 `Transfer`
4. 检查弹窗中的交易
5. 点击 `Create Transaction`

![](../imgs/tools-wallet/deposit-click-transfer.png)

这将触发一项计算 ZKP、准备交易的进程 - 授权 Metamask 访问您的账户余额。该进程结束时，请点击 `Send Transaction`- 授予 Metamask 与合约互动的更多权限。

![](../imgs/tools-wallet/deposit-tx-created-and-ready-to-be-sent.png)

转到交易页，[查看您的存款](#view-transactions)。

### 有关存款的重要信息 {#important-information-about-deposits}
- 在 Beta 版中，[存款金额是有限的](#note-the-following-deposit-and-withdrawal-restrictions)

## 如何进行转账 {#how-to-make-transfers}
在 Nightfall 资产页中点击选定资产右侧的 `Send` 按钮。

1. 输入 Polygon Nightfall L2 上的有效地址
2. 检查是否已选中您希望使用的代币（WETH、MATIC 等）
3. 输入您将从 Nightfall 钱包转出的价值，点击 `Continue`

![](../imgs/tools-wallet/send-nf.png)

这将触发一项进程，计算 ZKP 并准备交易。当该进程结束时，点击 `Send Transaction`。

转到交易页，[查看您的转账](#view-transactions)。

### 有关转账的重要信息 {#important-information-about-transfers}
Nightfall 当前使用的 ZKP 转账回路限制转账金额，它必须完全等同于某个现有承诺的价值，或等于两个现有承诺的任何线性组合。

为了举例说明转账限制，请看以下承诺集合：

- 集合 A：[1, 1, 1, 1, 1, 1]
- 集合 B：[2, 2, 2]
- 集合 C：[2, 4]

虽然这三个集合各自的合计价值均为 6，但您只能进行下列几种转账：

- 集合 A：0 至 2 之间的转账，不包括 0 和 2
- 集合 B：0 至 4 之间的转账，不包括 0 和 4
- 集合 C：0 至 6 之间的转账，不包括 0 和 6

继续本例，如果 Alex 拥有集合 C 中的承诺，可进行的转账额包括 0 至 6 之间的任何数字，不包括 0 和 6。如果 Alex 决定向 Bob 转账 3.5 枚代币，Alex 最终将使用一项价值为 2.5 的承诺，而 Bob 将在区块被提案后收到 3.5 枚代币。

另一方面，如果 Alex 决定向 Bob 转账 6 枚代币，则 ZK 证明将失败，因为不存在有效的承诺组合。

**请注意，这些值代表的是所拥有的承诺**，而不是存款。要了解更多信息，请参见这些文档中的[承诺](../protocol/commitments.md)一节。

## 如何提现 {#how-to-make-withdrawals}
在 Nightfall 资产页中点击选定资产右侧的 `Withdraw` 按钮，或导航至 L2 桥接页。

1. 检查转账模式是否设置为 `Withdraw`
2. 检查是否已选中您希望使用的代币（WETH、MATIC 等）
3. 输入您希望从 Nightfall 钱包中提取的价值，点击 `Transfer`
4. 检查弹窗中的交易
5. 点击 `Create Transaction`

这将触发一项进程，计算 ZKP 并准备交易。当该进程结束时，点击 `Send Transaction`。

转到交易页，[查看您的提现](#view-transactions)。为期一周的完成期结束后，用户将能够完成提现交易并申领提现金额。

### 有关提现的重要信息 {#important-information-about-withdrawals}
- 提现价值必须与拥有的承诺之一金额完全相符（进一步了解[有关承诺](#learn-about-commitments)）
- 从包含提款交易的区块创建之日起，有为期**一周**的时间来完成提款。这段时期过去后，您就可以最终完成提现，将资金发送到以太坊账户。
- 在 Beta 版本中，[提现金额受到限制](#note-the-following-deposit-and-withdrawal-restrictions)
- 提现属于链上交易，需要在交易请求期间和最后完成提现之时支付燃料费。

![](../imgs/tools-wallet/cooling-off-vs-ready.png)

## 查看交易 {#view-transactions}
在交易页上检查存款、转账和提现的状态。请注意，只要交易数足够生成区块，或提交已满 6 小时，所有交易都会得到处理。

![](../imgs/tools-wallet/transactions.png)
