---
id: wallet-bridge-faq
title: 錢包 <> 橋常見問題
description: 在 Polygon 上建置您的下一個區塊鏈應用程式。
keywords:
  - docs
  - matic
  - wallet
image: https://matic.network/banners/matic-network-16x9.png
---
import useBaseUrl from '@docusaurus/useBaseUrl';

## 我可以在哪裡使用 Matic Web 錢包？ {#where-can-i-use-the-matic-web-wallet}
[https://wallet.polygon.technology/](https://wallet.polygon.technology/)

## 如何找到代幣合約？ {#how-do-i-find-the-token-contract}

請參閱[新增自訂代幣](../faq/adding-a-custom-token)一文

## 目前支援哪些錢包？ {#which-wallets-are-currently-supported}

- Metamask
- Coinbase Wallet
- Wallet Connect

我們很快會新增更多錢包。

## 等離子體與 PoS 有何˙不同？ {#how-is-plasma-different-from-pos}

等離子體可提供額外的安全性。 
請參閱：[https://docs.polygon.technology/docs/develop/ethereum-polygon/getting-started](https://docs.polygon.technology/docs/develop/ethereum-polygon/getting-started)

## 等離子體上只能使用哪些代幣？ {#what-tokens-are-only-available-on-plasma}

Polygon 代幣

## 如何儲值到 Polygon 錢包？如何提取？ {#how-do-i-deposit-to-polygon-wallet-and-also-withdraw}

這些部落格和影片是完美地入門指南，可協助您了解如何儲值和提取： 

文件：[https://docs.polygon.technology/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/#depositing-funds-from-ethereum-to-matic](https://docs.polygon.technology/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/#depositing-funds-from-ethereum-to-matic)

影片：[https://www.youtube.com/playlist?list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9](https://www.youtube.com/playlist?list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9)

## 如何切換到 Metamask 中的 Polygon 主網？ {#how-to-switch-to-polygon-mainnet-in-metamask}

假設您已經在您的 Metamask 錢包中針對 Polygon 主網新增網路和自訂 RPC，您可以採取的切換方式如下：

1. 開啟您的 Metamask 錢包，然後按一下網路下拉式清單，如圖所示將其展開：

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-1.png")} width="30%" height="30%" />

1. 視窗展開後，您就可以選取 Polygon 主網以進行切換：

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-2.png")} width="357" height="600" />

您現在已經切換到 Polygon 主網了。

若要尋找有關如何將網路新增到 Metamask 的指示，您可以參閱此連結： [https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-metamask/](https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-metamask/)

## 如何在 Walletlink 中選擇 Polygon 主網？ {#how-to-choose-polygon-mainnet-in-walletlink}

請按照[這裡](https://docs.polygon.technology/docs/develop/metamask/config-polygon-on-wallets#configure-polygon-on-walletlink)提供的指南進行

## 我已儲值 WETH，但我沒有在 Metamask 上看到它。該怎麼辦？ {#i-have-deposited-weth-but-i-don-t-see-it-on-metamask-what-do-i-do}

您必須手動將 WETH 的自訂代幣地址新增到 Metamask。

開啟 Metamask 並向下捲動以按一下 **Import tokens**（匯入代幣）。

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-3.png")} width="357" height="600" />


然後，新增相關的合約地址、符號和小數點有效位數。 若要尋找合約地址（在此例中為 PoS-WETH），請前往此連結： [https://docs.polygon.technology/docs/develop/network-details/mapped-tokens/](https://docs.polygon.technology/docs/develop/network-details/mapped-tokens/)。 您必須新增子系代幣地址才能在 Polygon 主網上查看餘額。 WETH 的小數點有效位數為 18（一般來說，大多數代幣的小數點有效位數為 18）。

填寫所有欄位後，您就可以按一下 **Add Custom Token**（新增自訂代幣），系統將隨即新增您的代幣。

<img src={useBaseUrl("img/wallet-bridge/wallet-faq-4.png")} width="357" height="600" />


## 是否可以將我的代幣從 Polygon 傳送到任何其他錢包/交易所？ {#can-i-send-my-tokens-from-polygon-to-any-other-wallet-exchange}

您無法將代幣從 Polygon UI 直接傳送到交易所/錢包。 您必須先從 Polygon 提取到以太坊，然後將其傳送到您的交易所地址（除非您的交易所/錢包系統明確支援該網路）。

## 我不慎將資金直接傳送到交易所/錢包了。 是否可以請您協助解決？ {#i-made-a-mistake-of-sending-funds-to-an-exchange-wallet-directly-can-you-help}

很抱歉，我們無法協助您解決這類情況。請勿將資金直接傳送到僅支援以太坊的交易所。您必須先從 Polygon 提取到以太坊，然後再將其傳送到您的交易所地址。

## 我的交易擱置太久了，該怎麼辦？ {#my-transaction-is-pending-for-too-long-what-can-i-do}

由於提交交易時設定了較低的燃料價格，區塊鏈上的交易可能會中斷。 當燃料價格因以太坊上的壅塞而突然激增時，交易可能也會中斷。 還有一個可能性是，您可能已經從您的錢包取消交易或取代交易。 在所有這些情況下，錢包 Web 會顯示交易進行中的訊息，而這會導致您需要等候更久的時間。

如果您的交易卡住一個小時以上，將會顯示「Try Again」（再試一次）按鈕。 這很好，這表示您可以提示網路為您重試交易。 您接下來可以做的是，按一下「Try Again」（再試一次）按鈕以重試同一個交易。 如果您的儲值交易卡住了，您的儲值程序將重新啟動，而如果您的提取交易卡住了，您將能從您成功完成上一個不驟的位置繼續進行提取。

萬一您在使用「Try Again」（再試一次）按鈕繼續時遇到問題，而且您使用的是 Metamask 錢包，您可能需要檢查是否有很多排入佇列的交易，導致您的 Ｍetamask 活動區段堵塞。 在這種情況下，重新安裝 Metamask 錢包並繼續進行交易可能會有所幫助。 或者，您也可以嘗試從個別的瀏覽器啟動交易。

觀看以下影片可讓您更清楚了解如何使用「Try Again」（再試一次）功能

[https://youtu.be/0b4yjR_naEQ](https://youtu.be/0b4yjR_naEQ)

## Polygon 上的支援交易所清單有哪些？ {#what-are-the-list-of-supported-exchanges-on-polygon}

以下是目前支援 Polygon 的中心化交易所清單，以及這些交易所支援的代幣。

AscendEX - USDC、EASY、MATIC

MXC - MATIC、QUICK、PlotX、Dfyn

Okcoin -  ETH、USDT、LINK、MKR、USDC、DAI、USDK、COMP、YFI、SNX、YFII 和 UNI。 （代幣只能從 Okcoin 移轉到 Polygon 鏈。 目前不支援將代幣從 Polygon 轉移到 Okcoin）

Okex - BAL、BAT、CEL、COMP、CRV、DAI、ETH、GHST、GUSD、LINK、MKR、PAX、SNX、SUSHI、TUSD、UNI、USDC-ERC20、USDT-ERC20、USDK、wBTC、YFI、YFII、ZRX（代幣只能從 Okex 移轉到 Polygon 鏈。 目前不支援將代幣從 Polygon 轉移到 Okex）

Bitforex - MATIC

若將代幣傳送到上述清單中未明確提及的任何其他交易所，可能會導致資金遺失。 若要將資金提取到任何不支援 Polygon 的交易所，您必須先將代幣提取到以太坊，然後再使用您的以太坊錢包將其傳送到交易所。 這部影片示範了如何將資金從 Polygon 提取到以太坊： [https://www.youtube.com/watch?v=DgpHY95qrbQ&list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9&index=5](https://www.youtube.com/watch?v=DgpHY95qrbQ&list=PLslsfan1R_z0Epvnqsj29V1LBAh99dzu9&index=5)

或者，您也可以按照[這裡](https://docs.matic.today/docs/develop/wallets/matic-web-wallet/web-wallet-v2-guide/)的這份指南進行。

## 我無法登入，該怎麼辦？ {#i-am-not-able-to-login-what-do-i-do}

[https://docs.polygon.technology/docs/validate/delegator-faq/#my-metamask-is-stuck-at-confirming-after-login-what-do-i-do-or-nothing-happens-when-i-try-to-login](https://docs.polygon.technology/docs/validate/delegator-faq/#my-metamask-is-stuck-at-confirming-after-login-what-do-i-do-or-nothing-happens-when-i-try-to-login)

## Polygon 是否支援硬體錢包？ {#does-polygon-support-hardware-wallets}
是，支援硬體錢包。

## 我可以如何使用我的 Polygon 錢包？ {#what-can-i-do-with-my-polygon-wallet}

- 將資金傳送到 Polygon 上的任何帳戶。
- 將資金從以太坊儲值到 Polygon（使用橋）。
- 將資金從 Polygon 提取回以太坊（亦是使用橋）。

## 我在清單中看不到我的代幣。 我該聯絡誰？ {#my-token-is-not-visible-in-the-list-who-should-i-contact}

請聯絡 Discord 或 Telegram 上的 Polygon 團隊，以列出您的代幣。 在此之前，請確保您的代幣已對應。 若未對應，請前往以下位置提出要求： [https://mapper.polygon.technology/](https://mapper.polygon.technology/)

## 有哪些可以遵循的最佳做法？ {#what-are-some-best-practices-to-follow}

- 當您想要將資金從 Polygon 傳送到以太坊時，請使用提取功能。 請勿使用傳送功能。 這會導致資金遺失。
- 若只要參與質押，請勿儲值到 Polygon 主網。
- 請勿變更 Metamask 的燃料上限。

## 如果儲值已確認，但餘額未更新，該怎麼辦？ {#what-do-i-do-if-the-deposit-is-confirmed-but-the-balance-is-not-getting-updated}

完成儲值交易需要 22 到 30 分鐘的時間。 請等候一段時間，然後按一下「Refresh Balance」（重新整理餘額）。

## 如果沒有執行檢查點，該怎麼辦？ {#what-should-i-do-if-the-checkpoint-is-not-happening}

根據以太坊上的網路壅塞情形，檢查點有時候需要超過 45 分鐘到 1 小時的時間，建議您先等候一段時間，然後再提交票證。

## 是否可以取消提取交易？ {#is-it-possible-to-cancel-a-withdraw-transaction}

否，您必須完成後續不驟。 如果目前的燃料價格太高，請等到價格下降之後再嘗試。

## 為何 PoS 上不支援 MATIC 代幣？ {#why-is-the-matic-token-is-not-supported-on-pos}

MATIC 是 Polygon 的原生代幣，且在 Polygon 上具有合約地址 - 0x0000000000000000000000000000000000001010。 它也可用於支付燃料的費用。 對應 PoS 橋上的 MATIC 代幣會導致 MATIC 在 Polygon 鏈上具有額外的合約地址。 這會與現有的合約地址發生衝突，因為這個新代幣地址無法用於支付燃料的費用，且必須保留為 Polygon 鏈上的一般 ERC20 代幣。 因此，為了避免這種混淆，決定僅將 MATIC 保留在等離子體上。

## 如何對應代幣？ {#how-do-i-map-tokens}

請前往以下位置提出對應要求： [https://mapper.polygon.technology/](https://mapper.polygon.technology/)

## 如果交易耗時過久或如果燃料價格太高，該怎麼辦？ {#what-do-i-do-if-the-transaction-is-taking-too-long-or-if-the-gas-price-is-too-high}

交易時間和燃料價格會根據網路壅塞情形而有所不同。 如果支付了較高的燃料價格，就會以較快的速度確認交易。

## 是否可以變更燃料上限或燃料價格？ {#can-i-change-the-gas-limit-or-the-gas-price}

燃料上限是根據合約中呼叫的函數的特定要求由應用程式預估和設定。此值不應編輯。 只能變更燃料價格來提高或降低交易費用。

## 如果交易已取消，但 Web 錢包顯示交易已完成，該怎麼辦？ {#what-should-i-do-if-the-transaction-was-cancelled-but-the-web-wallet-shows-transaction-is-completed}

請聯絡我們的支援團隊。

## 我可在哪裡提交支援票證？ {#where-do-i-raise-a-support-ticket}
https://support.polygon.technology/support/home

## 燃料價格超過我要提取的金額。 {#the-gas-price-is-more-than-the-amount-i-seek-to-withdraw}

透過等離子體橋進行的提取交易共分為 3 個步驟，其中一個步驟在 Polygon 主網上進行，而兩個步驟則是在以太坊主網上完成。 在 PoS 橋上，提取交易會在兩個步驟中進行：在 Polygon 網路上燒毀代幣，以及在以太坊網路上提交證明。 在 Polygon 主網上，費用非常低廉，您看到的大部分交易費用是由以太坊挖礦者所控管的以太坊網路上的燃料價格。 可想而知，此費用不在我們的掌控範圍內，而且我們對價格點不太有影響力。 最後一點，如果您的代幣已燒毀，您可能必須繼續進行提取，因為無論如何，我們都無法逆轉此程序。


## 是否可以取消我的提取交易？ {#can-i-cancel-my-withdrawal-transaction}

很抱歉，一旦初始化此程序，Polygon 就無法取消提取作業，且代幣會成功燒毀。 系統會建立燒毀雜湊，並且會立即進行交易的下一個階段。 如果燒毀交易仍處於擱置狀態，您可能可以透過以下指南加速取消作業

[Metamask](https://metamask.zendesk.com/hc/en-us/articles/360015489251-How-to-Speed-Up-or-Cancel-a-Pending-Transaction) <br />
[Walletlink](https://www.techdreams.org/crypto-currency/how-to-cancel-a-pending-ethereum-transaction-on-coinbase-wallet/10159-20210412)


## 我的交易卡住了。 {#my-transaction-is-stuck}

我們列出了使用者可能會遇到的一些常見錯誤。 您可以在錯誤的影像下方找到解決方案。 萬一畫面上顯示不同的錯誤，請[提交支援票證](https://support.polygon.technology/support/home)，讓我們的團隊進行疑難排解。

  - ### 常見錯誤 {#common-errors}
a. 提取卡在「Initialised」（初始化）階段。

    <img src={useBaseUrl("img/wallet-bridge/plasma-progress-stuck.png")} width="357" height="800"/>

    當交易遭到取代且錢包 Ｗeb 應用程式無法偵測到取代的交易雜湊時，通常就會發生這種情況。 請按照 [https://withdraw.polygon.technology/](https://withdraw.polygon.technology/) 上的指示進行，然後完成您的提取作業。

  b. RPC 錯誤

    <img src={useBaseUrl("img/wallet-bridge/checkpoint-rpc-error.png")} width="357" height="600"/>   

    您目前遇到的 RPC 錯誤可能是因為 RPC 超載。

    請嘗試變更您的 RPC，然後繼續進行交易。 如需詳細資訊，請前往此連結 [這裡](https://docs.polygon.technology/docs/develop/network-details/network#matic-mainnet)。

  c.

  <img src={useBaseUrl("img/wallet-bridge/checkpoint-stumbled-error.png")} width="357" height="600"/>

  這通常是會自動解決的間歇性錯誤。 萬一您仍在重新啟動此步驟時收到同樣的錯誤，請務必[提交支援票證](https://support.polygon.technology/)（包含所有相關資訊），以針對此錯誤進行進一步的疑難排解。

## 我不慎將資金直接從 Polygon 錢包傳送到交易所/錢包了。 是否可以請您協助解決？ {#i-made-the-mistake-of-sending-funds-to-an-exchange-wallet-directly-from-polygon-wallet-can-you-help}

很抱歉，令人遺憾的是，如果您已將代幣從 Polygon 網路傳送到不支援的交易所/錢包，我們可能無法協助您。

以下是交易所在這種情況下需要執行的事項（雖然不確定支援專員有多大的彈性能夠執行此操作）。 假設交易所支援專員可存取帳戶的私密金鑰，那麼就可以將資金從其 Polygon 上的帳戶轉移到您（使用者）在 Polygon 上的的地址。

請務必注意，您不應將資金直接傳送到僅支援以太坊的交易所。 正確的程序是，您必須先從 Polygon 提取到以太坊，然後再將其傳送到交易所地址。

## 畫面上顯示餘額不足錯誤。 {#i-m-shown-an-insufficient-balance-error}

Polygon 網路上的提取和儲值費用非常低廉。 要理解的是，您可以在以太坊主網上取得一些 ETH 餘額來清除餘額不足錯誤。 這樣通常就會消除餘額不足的問題。

如果這是 Polygon 主網上的交易，我們會要求您必須有足夠數量的 Matic 代幣。

## 如何橋接各個鏈上的資產？ {#how-do-i-bridge-assets-across-chains}

[https://wallet.polygon.technology/bridge/](https://wallet.polygon.technology/bridge/) (ETH <-> Polygon) <br/>
[https://xpollinate.io/](https://xpollinate.io/) (BSC <-> Polygon <-> xDai) <br/>
[https://exchange.chainswap.com/](https://exchange.chainswap.com/) (ETH <-> Polygon/BSC) <br/>
[https://anyswap.exchange/bridge](https://anyswap.exchange/bridge) (ETH <-> Polygon <-> BSC/xDai) <br/>
[https://app.0.exchange/#/home](https://app.0.exchange/#/home)(ETH <-> Polygon <-> Avalanche <-> BSC)

附帶一提，我們不為任何外部服務背書，請務必隨時自行研究

## 我已轉移到錯誤的地址。 我該如何擷取資金？ {#i-made-a-transfer-to-the-wrong-address-how-do-i-retrieve-the-funds}

很抱歉，沒有任何解決方法。 只有該特定地址的私密金鑰擁有者才能移轉這些資產。


## 我的交易沒有顯示在瀏覽器上。 該怎麼辦？ {#my-transactions-are-not-visible-on-the-explorer-what-should-i-do}

這可能是與 Polygonscan 有關的編製索引問題。 若要進一步釐清，請聯絡[支援團隊](https://support.polygon.technology/support/home)。
您也可以嘗試這些區塊瀏覽器

[https://polygon-explorer-mainnet.chainstacklabs.com](https://polygon-explorer-mainnet.chainstacklabs.com/) <br />
[https://explorer-mainnet.maticvigil.com](https://explorer-mainnet.maticvigil.com/) <br />
[https://explorer.matic.network](https://explorer.matic.network/) <br />
[https://backup-explorer.matic.network](https://backup-explorer.matic.network/)


## 我在以太坊上啟動了儲值，但它仍顯示為擱置中。 該怎麼辦？ {#i-initiated-a-deposit-on-ethereum-but-it-still-shows-as-pending-what-should-i-do}

您提供的燃料可能太低。 您應等候一段時間，如果沒有順利完成挖礦，請重新執行交易。 如果需要其他協助，請聯絡[支援團隊](https://support.polygon.technology/support/home)，並提供您的錢包地址、交易雜湊（若有）和相關螢幕擷取畫面。


## 我遇到與 OpenSea 或任何其他使用 Polygon 橋之應用程式有關的代幣提取問題。 {#i-have-a-token-withdrawal-issue-with-opensea-or-any-other-application-which-uses-polygon-bridge}

如果您遇到提取交易卡住的問題，Polygon 透過 https://polygon-withdraw.matic.network/ 提供了提取橋，以協助您在擁有燒毀雜湊時開始著手進行。 透過此工具，您可以快速上線並順利解決問題。 關於您在 OpenSea 和其他 DApp 之交易的其他問題，將須交由應用程式團隊處理。


## 我可以直接在哪裡獲得 MATIC 代幣？ {#where-can-i-get-matic-tokens-directly}

您可以透過任何中心化（[Binance](https://www.binance.com/en)、[Coinbase](https://www.coinbase.com/) 等處）或去中心化（[Uniswap](https://uniswap.org/)、[QuickSwap](https://quickswap.exchange/#/swap)）交易所購買 MATIC 代幣。 您也可以研究並嘗試一些入金 (on-ramp)，例如 [Transak](https://transak.com/)、[Ramp](https://ramp.network/)。
您購買 MATIC 幣的目的也應取決於您要購買的來源位置及網路。 如果您是打算進行質押挖礦或委派，建議您在以太坊主網上擁有 MATIC。如果您是打算在 Polygon 主網上進行交易，您應在 Polygon 主網上持有 MATIC 並使用它來進行交易。


## 我沒有收到交易雜湊，而且我的儲值沒有順利完成？ 發生了什麼情況？ {#i-m-not-getting-a-transaction-hash-and-my-deposits-aren-t-going-through-what-is-happening}

您可能有先前擱置的交易，請先取消或加速完成這些交易。 以太坊中的交易只能一個接一個進行。


## 它顯示 Polygon 不收取任何提取費用，但我們要在交易過程中支付費用。 {#it-shows-polygon-does-not-charge-any-amount-for-a-withdrawal-but-we-are-to-pay-during-the-transaction}

透過等離子體橋進行的提取交易共分為 3 個步驟，其中一個步驟在 Polygon 主網上進行，而兩個步驟則是在以太坊主網上完成。 在 PoS 橋上，提取交易會在兩個步驟中進行：在 Polygon 網路上燒毀代幣，以及在以太坊網路上提交證明。 在所有情況下，在 Polygon 主網上進行的代幣燒毀會是一筆很小的費用。 在以太坊主網上進行的其餘步驟必須根據目前燃料價格用以太幣支付，您可以在[這裡](https://ethgasstation.info/)確認該價格。


## 如何聯絡部署在 Polygon 網路上的主要應用程式？ {#how-do-i-contact-major-applications-deployed-on-the-polygon-network}

Curve  [https://discord.gg/JnUFrsDF](https://discord.gg/JnUFrsDF) <br />
SushiSwap  [https://discord.gg/ApbE4Eau](https://discord.gg/ApbE4Eau) <br />
CREAM  [https://discord.gg/js8JpmFB](https://discord.gg/js8JpmFB) <br />
AAVE  [https://discord.gg/YYtp7N5d](https://discord.gg/YYtp7N5d) <br />
FuruCombo  [https://discord.gg/wJJ7PXAd](https://discord.gg/wJJ7PXAd) <br />
QuickSwap  [http://t.me/QuickSwapDEX](http://t.me/QuickSwapDEX) <br />

Beefy Finance - [https://discord.gg/egkEEAkC](https://discord.gg/egkEEAkC)


## Polygon 網路上支援的硬體錢包清單。 {#list-of-hardware-wallets-supported-on-polygon-network}

因此，Polygon 網路將支援與 Metamask 相容的所有硬體錢包。 如需詳細資訊，請前往 Metamask 中的此[連結](https://metamask.zendesk.com/hc/en-us/articles/360020394612-How-to-connect-a-Trezor-or-Ledger-Hardware-Wallet)。


## 我遇到詐騙了。 我該如何擷取我的代幣？ {#i-have-been-scammed-how-will-i-retrieve-my-tokens}

很抱歉，遺失的貨幣沒有任何復原程序。 在進行交易之前，請務必檢查，並在開始前和完成前再次仔細檢查。 請注意，Polygon 網路和我們的官方廣告並不會參與任何贈品發佈或代幣加倍活動，而且我們絕對不會代表組織與您聯繫。 請忽略所有試圖接近您的此類舉動，它們很可能是詐騙。 我們的所有通訊都是透過
官方廣告。


## 以太坊有 Goerli 做為其測試網路。 Polygon 網路是否有測試網路？ {#so-ethereum-has-goerli-as-its-test-network-does-polygon-network-have-a-test-network}

以太坊網路有 Goerli 做為其測試網路，Polygon 主網則有 Mumbai 做為其測試網路。 此測試網路上的所有交易都會在 Mumbai 瀏覽器上編製索引。


## 如何加速我在 Metamask 上的交易。 {#how-can-speed-up-my-transaction-on-metamask}

若要透過 Metamask 加速交易，請前往此[連結](https://metamask.zendesk.com/hc/en-us/articles/360015489251-How-to-Speed-Up-or-Cancel-a-Pending-Transaction)


## 建立票證時，哪些是我應提供的所有資訊？ {#what-all-information-should-i-provide-when-i-create-a-ticket}

- 錢包地址
- 交易雜湊
- 打算執行的確切動作及結果（非常具體）
- 動作的螢幕擷取畫面或螢幕錄製

## 我嘗試進行儲值，但交易在「Approve」（核准）步驟中停止了。 {#i-was-trying-to-make-a-deposit-but-the-transaction-stopped-at-the-approve-step}

如果交易仍在 **Approve**（核准）步驟，則表示尚未完成。 若要完成此步驟，您必須支付燃料費用，然後應該就會順利完成了。

## 我的提取交易的燃料費用太高了。 {#the-gas-fee-for-my-withdrawal-transaction-is-too-high}

Polygon 網路上的燃料費用總是很低，但以太坊主網費用則是不一樣的情形。
如果您已經開始交易，請切勿取消該交易。相反地，您可以等待燃料費用降低，或將更多以太幣新增到您的帳戶中。

## 我的錢包中有一些未經授權的交易。 我的錢包是否遭到駭客入侵？ {#there-are-some-unauthorized-transactions-in-my-wallet-is-my-wallet-hacked}

很抱歉，網路無法還原不想要的交易。
請務必謹慎保管您的私密金鑰，並且**切勿與任何人分享**。
如果您仍有一些剩餘的資金，請立即將其轉移到新的錢包。

## Polygon 錢包顯示「Oops our Server Stumbled」（糟糕！我們的伺服器出錯了）錯誤訊息。 {#polygon-wallet-shows-an-oops-our-server-stumbled-error-message}

該訊息可能表示我們的伺服器已故障。 不過，如果一切運作正常，建議您使用其他瀏覽器。
如果您嘗試進行提取，您也可以嘗試 [Polygon 提取工具](https://polygon-withdraw.matic.network/)。 其中您可以連接您的錢包、貼上您的交易雜湊，然後繼續進行交易。

## Polygon 錢包顯示「User denied transaction signature」（使用者已拒絕交易簽名）錯誤訊息。 {#polygon-wallet-shows-user-denied-transaction-signature-error-message}

會發生這種情況通常是因為使用者已取消或拒絕透過 MetaMask 簽署交易。 出現 MetaMask 錢包提示時，請按一下「Approve」（核准），而不是「Cancel」（取消），以繼續簽署交易。

## 我沒有收到我轉移到交易所的代幣 {#i-did-not-receive-the-tokens-i-transferred-to-an-exchange}
您已將貨幣轉移到 Binance（Coinbase、Kucoin 或任何其他交易所），但沒有在交易所收到這些貨幣。 如果您的情況是這樣，請務必了解，我們目前不提供與交易所的直接連線。 大多數交易實際上會先經過以太坊主網，然後再抵達交易所。
請聯絡交易所的支援團隊。

## 我的 MetaMask 錢包沒有與 Polygon 錢包連線 {#my-metamask-wallet-is-not-connecting-with-polygon-wallet}

發生這種情況的可能原因有很多。 建議您**再試一次**、**使用其他瀏覽器**，或如果所有這些措施都沒有幫助，請**聯絡我們的支援團隊**。

## 如何獲得可支付燃料費用的 MATIC 代幣？ {#how-can-i-get-matic-tokens-to-pay-for-gas-fees}

我們提供將助您一臂之力的[燃料交換](https://wallet.polygon.technology/gas-swap/)服務。 您選擇完成交易所需的 MATIC 數量，而且您可以將其換成以太幣或 USDT 等其他代幣。 值得注意的是，有一筆**免收礦工費交易**。

## 代幣交換的速度太緩慢。 {#token-swap-is-too-slow}

如果您嘗試交換代幣但耗時過久，您可以嘗試在另一個不同的瀏覽器上執行同樣的交易。 如果這樣做沒有效，而且仍遇到錯誤，請傳送螢幕擷取畫面給我們的支援團隊。
