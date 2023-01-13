---
id: adding-a-custom-token
title: 新增自訂代幣
sidebar_label: Adding a Custom Token
description: 在 Polygon 上建置您的下一個區塊鏈應用程式。
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

**Add Custom Token**（新增自訂代幣）功能可讓您明確地新增任何代幣，並將其與 Polygon Wallet Suite 搭配使用。 您必須依據代幣的合約地址（根或子系）搜尋代幣：

* **root**（根）是以太坊上的代幣合約
* **child**（子系）是 Polygon 上的合約

### 專家提示：如何找到代幣合約？ {#pro-tip-how-do-i-find-the-token-contract}

您可以依據代幣名稱在 [Coingecko](http://coingecko.com) 或 [Coinmarketcap](https://coinmarketcap.com/) 上搜尋代幣，其中您將能在以太坊鏈（適用於 ERC 20 代幣）及 Polygon 等其他支援後續鏈上查看其地址。 其他鏈上的代幣地址可能不會更新，但您肯定可以將根地址用於所有用途。

因此，選取代幣時，您將能依據以下項目進行搜尋：
* 代幣符號
* 代幣名稱
* 合約

運作方式如下：

<img src={useBaseUrl("img/wallet-bridge/001.png")} height="420px"/>

1. 將合約地址新增為自訂代幣，以輕鬆地將任何代幣新增到您的清單（我們支援

Polygon 或以太坊上的合約地址）：

<img src={useBaseUrl("img/wallet-bridge/002.png")} height="600px"/>

2. 擷取代幣資訊後，您將會看到一個包含所有代幣資訊的確認畫面。 然後，您可以將其新增為自訂代幣，這會以本機形式儲存在您的系統中。建議您再次重新驗證代幣合約，因為有很多複製或詐騙代幣：

<img src={useBaseUrl("img/wallet-bridge/003.png")} height="600px"/>

<img src={useBaseUrl("img/wallet-bridge/004.png")} height="600px"/>

3. 現在，會在選取代幣時顯示您的新增代幣：

<img src={useBaseUrl("img/wallet-bridge/005.png")} height="600px"/>

4. 您可以直接從 **Manage**（管理）畫面的代幣索引標籤新增代幣：

<img src={useBaseUrl("img/wallet-bridge/006.png")} height="600px"/>
