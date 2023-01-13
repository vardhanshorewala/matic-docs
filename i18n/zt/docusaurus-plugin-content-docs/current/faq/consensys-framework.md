---
id: consensys-framework
title: ConsenSys 擴展架構
sidebar_label: Consensys Scaling Framework
description: 在 Polygon 上建置您的下一個區塊鏈應用程式。
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

此架構源自於 ConsenSys [判斷任何擴展解決方案的四個問題](https://consensys.net/?p=19015&preview=true&_thumbnail_id=19017)

## 由誰操作？ {#who-operates-it}
主網以太坊上的挖礦者節點會解決工作證明並建立新區塊，藉此推動或「操作」網路使其向前發展。L2 解決方案在其網路上需要類似的「操作者」角色，這等同於以太坊主網的挖礦者身分，可以推動 L2 網路向前發展。 不過，其中有一些差異。 例如，除了像挖礦者一樣處理和授權交易，L2 操作者還會讓使用者方便進入和退出 L2 層本身。

### - 需要哪些人員或項目才能操作 Polygon 權益證明網路？ {#who-or-what-is-required-to-operate-the-polygon-proof-of-stake-network}

Polygon PoS 提交鏈仰賴一組驗證者來保護網路。 驗證者角色旨在執行完整的節點；產生區塊、驗證和參與共識，以及在以太坊主鏈上提交檢查點。若要成為驗證者，必須使用位於以太坊主鏈上的質押挖礦管理合約來質押其 MATIC 代幣。

如需詳細資訊，請參閱 https://docs.polygon.technology/docs/validate/validator/introduction#overview

### - 他們如何成為 Polygon PoS 網路中的操作者？ 他們需要遵守哪些規則？ {#how-do-they-become-operators-in-the-polygon-pos-network-what-rules-do-they-abide-by}

若要成為驗證者，必須使用位於以太坊主鏈上的質押挖礦
管理合約來質押其 MATIC 代幣。

獎勵會在每個檢查點按其質押比例分配給所有質押者，但獲得額外獎金的提議者例外。 合約中會更新使用者獎勵餘額，以便在領取獎勵時
做為參考。

質押會面臨大幅削減的風險（萬一驗證者節點提交
雙重簽署等惡意動作），驗證者停機時間也會影響
該檢查點的連結委派者。

如需詳細資訊，請參閱
https://docs.polygon.technology/docs/validate/validator/introduction#end-to-end-flow-for-a-matic-validator 及 https://docs.polygon.technology/docs/validate/validator/responsibilities/#responsibilities-of-validator


### - Polygon PoS 使用者必須對操作者做出哪些信任假設？ {#what-trust-assumptions-must-the-polygon-pos-users-make-about-the-operator}

Polygon PoS 提交鏈仰賴一組驗證者來保護網路。 驗證者角色旨在執行完整的節點；產生區塊、驗證和參與共識，以及在主鏈上提交檢查點。 若要成為驗證者，必須使用位於主鏈上的質押挖礦管理合約來質押其 MATIC 代幣。
只要 ⅔ 的權重驗證者質押是可信的，該鏈就會準確地進行。

### - 操作者負責哪些工作？ 他們擁有哪些權力？ {#what-are-the-operators-responsible-for-what-power-do-they-have}

驗證者角色旨在執行完整的節點；產生區塊、驗證和參與共識，以及在主鏈上提交檢查點。

假設 ⅔ 的權重質押驗證者不可信，驗證者有權停止該鏈的進度、重新排序區塊等等。 他們無權變更狀態、使用者資產餘額等等。

### - 成為 Polygon PoS 操作者的動機是什麼？ {#what-are-the-motivations-to-become-an-operator-of-the-polygon-pos}

驗證者將其 MATIC 代幣質押為抵押品，以致力於網路安全性並做為使用其服務的交換，以及獲得獎勵。

如需詳細資訊，請參閱 https://docs.polygon.technology/docs/validate/economics#what-is-the-incentive。

## 資料的情況如何？ {#how-s-the-data}
根據定義，第 2 層技術必須在第 1 層（以太坊主網）上建立增量資料檢查點。 那麼，我們的顧慮是這些週期性第 1 層簽入之間的間隙時間。 具體來說，如何在離開第 1 層安全港的情況下產生、存放及管理第 2 層資料？這是我們最關切的問題，因為這是使用者距離公用主網的不可靠安全性最遠的時候。

### - Polygon PoS 的鎖定狀況是什麼？ {#what-are-the-lock-up-conditions-for-polygon-pos}

在大多數代幣設計模式中，代幣是在以太坊上鑄造，而且可以傳送到 Polygon PoS。 若要將這種代幣從以太坊移轉到 Polygon PoS，使用者必須鎖定以太坊的合約中的資金，然後就會在 Polygon PoS 上鑄造對應的代幣。

這種橋轉送機制是由 Polygon PoS 驗證者執行，必須有 ⅔ 的驗證者同意以太坊上的鎖定代幣事件，才能在 Polygon PoS 上鑄造對應的代幣數量。

將資產提取回以太坊是由 2 個步驟組成的程序，必須先在 Polygon PoS 提交鏈上燒毀資產代幣，然後必須在以太坊鏈上提交此燒毀交易的證明。


如需詳細資訊，請參閱 https://docs.polygon.technology/docs/develop/ethereum-polygon/pos/getting-started#steps-to-use-the-pos-bridge

### - 這些資金多久後可以在 Polygon PoS 上使用？ {#how-soon-are-those-funds-available-on-the-polygon-pos}

大約 22 到 30 分鐘。 這是透過一種稱為 `state sync` 的訊息傳遞機制執行。 您可以在這裡找到更多詳細資訊：https://docs.polygon.technology/docs/pos/state-sync/state-sync/

Polygon PoS 是否為在沒有 L1 鎖定情況下進入的使用者提供支援（亦即在讓使用者直接上線到 Polygon 的情況下，使用者則會希望退出到以太坊主網）？

是，您可以使用特殊橋機制來完成此操作。 當使用者希望退出到以太坊時，會開始進行鑄造，而不是使用從特殊合約解除鎖定代幣的一般方法。

您可以在這裡閱讀相關資訊：https://docs.polygon.technology/docs/develop/ethereum-polygon/pos/mintable-assets

### - 使用者如何對無效的 Polygon PoS 交易提出異議？ 如何證明有效的 Polygon PoS 交易？ {#how-would-a-user-dispute-an-invalid-polygon-pos-transaction-prove-a-valid-polygon-pos-transaction}

目前沒有方法在鏈上對無效的 Polygon PoS 交易提出異議。 不過，Polygon PoS 鏈的驗證者會將定期檢查點提交到以太坊 - 您可以在這裡查看更多詳細資訊：https://docs.polygon.technology/docs/pos/heimdall/modules/checkpoint/
您可以驗證以太坊的 Polygon PoS 鏈上的交易，方法是建構 Merkle 樹證明，並根據在 Polygon PoS 交易和收據 Merkle 樹根的以太坊上發生的定期檢查點進行驗證。

一旦 Polygon 使用者想要退出，鎖定的第 1 層資金（加上或減去任何 L2 收益或損失）多久後可在 L1 上重新使用？

大約 1 到 3 個小時（視檢查點頻率而定）(https://docs.polygon.technology/docs/pos/heimdall/modules/checkpoint/)。 此頻率主要是驗證者願意在 ETH 燃料費用上花費之成本的函數，以提交檢查點。

### - 您是否預期第 1 層上會有流動性供應商，願意立即向現有 Polygon PoS 使用者提供可重新兌換的  L1 資金？ {#do-you-anticipate-there-being-liquidity-providers-on-layer-1-willing-to-provide-immediately-redeemable-l1-funds-to-existing-polygon-pos-users}

已經有一些玩家（例如 https://connext.network/（已上線）和 https://biconomy.io/）正在或將提供此服務。還有其他各種玩家也會很快上線。

## 堆疊的情況如何？ {#how-s-the-stack}
堆疊比較至關重要，可突顯第 2 層擁有的項目，或突顯尚未從以太坊主網變更的項目。

### - Polygon PoS 堆疊會與以太坊主網堆疊共用多少？ {#how-much-does-the-polygon-pos-stack-share-with-the-ethereum-mainnet-stack}

如果您是以太坊開發者，表示您已經是 Polygon PoS 開發者。 您熟悉的所有工具均可在 Polygon PoS 上享有立即可用的支援：Truffle、Remix、Web3js 等眾多工具。

相對於以太坊，Polygon PoS 的 EVM 介面中沒有重大變更。

### -  Polygon PoS 與以太坊主網堆疊有何不同之處？這會帶來哪些風險/獎勵？ {#where-does-the-polygon-pos-differ-from-ethereum-mainnet-stack-and-what-risks-rewards-does-that-introduce}

沒有任何重大變更。

## 為最糟的情況做好準備 {#preparing-for-the-worst}
Polygon PoS 系統如何針對以下情況做好準備：

### -  大規模使用者退出？ {#a-mass-exit-of-users}

只要 ⅔ 的驗證者是可信的，鏈上的資金就是安全的。 萬一這種假設無效，在這種情況下，鏈可能會停止，或是可能會進行重新排序。 將需要社交共識，以從先前的狀態重新啟動鏈 - 包括透過可用來執行此操作之檢查點提交的 Polygon PoS 狀態快照。

### - 試圖對 Polygon 共識進行博弈的 Polygon 參與者。 例如，形成同業聯盟？ {#polygon-participants-attempting-to-game-the-polygon-consensus-for-example-by-forming-a-cartel}

需要有社交共識，然後才能移除這些驗證者並使用一組全新驗證者將其重新啟動，藉此從先前的狀態重新啟動鏈，包括透過可用來執行此操作之檢查點提交的 Polygon PoS 狀態快照。


### - 在其系統的關鍵環節中發現的錯誤或惡意探索？ {#a-bug-or-exploit-discovered-in-a-critical-part-of-its-system}

在建置系統時，已注意重複使用經過實戰測試的元件。 不過，如果系統的關鍵環節中有錯誤或惡意探索，透過社交共識將鏈還原到先前狀態是主要的解決方案途徑。
