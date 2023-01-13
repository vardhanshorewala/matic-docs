---
id: general-faq
title: 一般常見問題
description: Polygon 網路上的常見問題。
keywords:
  - docs
  - matic
  - polygon
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

## 什麼是 Polygon 網路？ {#what-is-polygon-network}

Polygon 網路是一種第 2 層擴展解決方案，其實現擴展的方法為利用側鏈進行鏈下運算，同時透過權益證明 (PoS) 驗證者確保資產安全性和去中心化。

另請參閱[什麼是 Polygon](/docs/home/polygon-basics/what-is-polygon)。

## 什麼是權益證明 (PoS)？ {#what-is-proof-of-stake-pos}

權益證明是一種系統，其中區塊鏈網路以實現分佈式共識做為目標。 凡是擁有足夠代幣數量的人，就可以鎖定其加密貨幣，而且經濟獎勵措施有賴於去中心化網路的共同價值。質押其加密貨幣的個人可透過就同樣的交易進行投票來驗證交易，而在檢查點的一個區塊或一組區塊中的一個交易或一組交易獲得足夠的票數時，就會達成共識。 門檻會在每一票附帶的質押上使用權重。 例如，在 Polygon 中，當至少 ⅔ +1 的總計質押投票給此項目時，會將 Polygon 區塊的檢查點提交到以太坊網路來達成共識。

另請參閱[什麼是權益證明](/docs/home/polygon-basics/what-is-proof-of-stake)。

## 權益證明可在 Polygon 架構中發揮什麼作用？ {#what-role-does-proof-of-stake-play-in-the-polygon-architecture}

Polygon 架構中的權益證明層具有以下 2 種用途：

* 做為獎勵措施層，維持等離子體鏈的活躍性，主要可緩解資料無法使用的棘手問題。
* 針對等離子體未包含的狀態轉換，實作權益證明安全性保證。

## Polygon PoS 與其他類似系統有何不同？ {#how-is-polygon-pos-different-from-other-similar-systems}

它的不同之處在於具有雙重用途：透過等離子體預測，為包含狀態狀換的等離子體鏈提供資料可用性保證，並為 EVM 中的通用智慧合約提供權益證明驗證。

Polygon 架構也會將區塊生產和驗證程序區分為 2 個不同的層。 顧名思義，身為區塊生產者的驗證者會在 Polygon 鏈上建立區塊，以便更快速地（< 2 秒）進行部分確認，而一旦檢查點以特定時間間隔在主鏈上提交，就會獲得最終確認，時間間隔可能會因以太坊壅塞或 Polygon 交易數量等多項因素而有所不同。 在理想的情況下，時間間隔應大約為 15 分鐘到 1 小時。

檢查點基本上就是間隔之間產生的所有區塊的 Merkle 根。驗證者可發揮多種作用，包括在區塊生產者層建立區塊、簽署所有檢查點以參與達成共識，以及在做為提議者時提交檢查點。 驗證者變成區塊生產者或提議者的概率是基於其在整體池中的質押率。

## 建議提議者包含所有簽名 {#encouraging-the-proposer-to-include-all-signatures}

為了充分利用提議者獎金，提議者需要在檢查點中包含所有簽名。 由於協定需要總計質押的 2/3+1 權重，即使有 80% 的票數，仍會接受檢查點。不過，在這種情況下，提議者只會獲得計算出的 80% 的獎金。

## 如何提交支援票證或參與 Polygon 文件製作？ {#how-can-i-raise-a-support-ticket-or-contribute-to-polygon-documentation}
如果您認為我們的文件有需要修正的內容，或您甚至希望在這裡新增新的資訊，您可以[在 Github 儲存庫上提出問題](https://github.com/maticnetwork/matic.js/issues)。 儲存庫上的[讀我檔案](https://github.com/maticnetwork/matic-docs/blob/master/README.md)也會提供您一些建議，讓您了解如何參與我們的文件製作。

如果您仍需要協助，您可以隨時聯絡**我們的支援團隊**。
