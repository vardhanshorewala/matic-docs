---
id: technical-faqs
title: 技術常見問題
description: 在 Polygon 上建置您的下一個區塊鏈應用程式。
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

### 1. Heimdall 和 Bor 金鑰儲存區的私密金鑰是否相同？ {#1-are-the-private-keys-same-for-heimdall-and-bor-keystore}
是，用來產生驗證者金鑰和 Bor 金鑰儲存區的私密金鑰是相同的。 此實例中使用的私密金鑰是您錢包的 ETH 地址，這是儲存您 Polygon 測試網代幣的位置。

### 2. 常用命令清單 {#2-list-of-common-commands}

我們目前有易於深入探討的 Linux 套件清單。 為了提高便利性，我們會持續定期更新此清單。

**適用於 Linux 套件**

#### A. 可找到 Heimdall Genesis 檔案的位置 {#a-where-to-find-heimdall-genesis-file}

`$CONFIGPATH/heimdall/config/genesis.json`

#### B. 可找到 heimdall-config.toml 的位置 {#b-where-to-find-heimdall-config-toml}

`/etc/heimdall/config/heimdall-config.toml`

#### C. 可找到 config.toml 的位置 {#c-where-to-find-config-toml}

`/etc/heimdall/config/config.toml`

#### D. 可找到 heimdall-seeds.txt 的位置 {#d-where-to-find-heimdall-seeds-txt}

`$CONFIGPATH/heimdall/heimdall-seeds.txt`

#### E. 啟動 Heimdall {#e-start-heimdall}

`$ sudo service heimdalld start`

#### F. 啟動 Heimdall rest-server {#f-start-heimdall-rest-server}

`$ sudo service heimdalld-rest-server start`

#### G. 啟動 Heimdall bridge-server {#g-start-heimdall-bridge-server}

`$ sudo service heimdalld-bridge start`

#### H. Heimdall 日誌 {#h-heimdall-logs}

`/var/log/matic-logs/`

#### I. 可找到 Bor Genesis 檔案的位置 {#i-where-to-find-bor-genesis-file}

`$CONFIGPATH/bor/genesis.json`

#### J. 啟動 Bor {#j-start-bor}

`sudo service bor start`

#### K. 檢查 Heimdall 日誌 {#k-check-heimdall-logs}

`tail -f heimdalld.log`

#### L. 檢查 Heimdall rest-server {#l-check-heimdall-rest-server}

`tail -f heimdalld-rest-server.log`

#### M. 檢查 Heimdall 橋日誌 {#m-check-heimdall-bridge-logs}

`tail -f heimdalld-bridge.log`

#### N. 檢查 Bor 日誌 {#n-check-bor-logs}

`tail -f bor.log`

#### O. 刪除 Bor 程序 {#o-kill-bor-process}

**適用於 Linux**：

1. `ps -aux | grep bor`。 取得 Bor 的 PID，然後執行以下命令。
2. `sudo kill -9 PID`

**適用於二元函數**：

前往 `CS-2003/bor`，然後執行 `bash stop.sh`

### 3. 錯誤：無法解除鎖定帳戶 (0x...) 沒有指定地址或檔案的金鑰 {#3-error-failed-to-unlock-account-0x-no-key-for-given-address-or-file}

發生此錯誤是因為 password.txt 檔案的路徑不正確。 您可以按照以下步驟修正此問題：

發生此錯誤是因為 password.txt 和 Keystore 檔案的路徑不正確。 您可以按照以下步驟修正此問題：

1. 將 Bor 金鑰儲存區檔案複製到

    /etc/bor/dataDir/keystore

2. 並將 password.txt 複製到

    /etc/bor/dataDir/

3. 確認您已在 `/etc/bor/metadata` 中新增正確的地址

適用於二元函數：

1. 將 Bor 金鑰儲存區檔案複製到：

`~/.bor/keystore/`

2. 並將 password.txt 複製到

`~/.bor/password.txt`


### 4. 錯誤：錯誤的 Block.Header.AppHash。 預期 xxxx {#4-error-wrong-block-header-apphash-expected-xxxx}

當 Heimdall 服務卡在區塊上時，通常就會發生此錯誤；Heimdall 上沒有可用的逆轉方法。

若要解決此問題，您必須完全重設 Heimdall：

```bash
    sudo service heimdalld stop

    heimdalld unsafe-reset-all
```

然後，您應再次從快照進行同步：

```bash
    wget -c <Snapshot URL>

    tar -xzvf <snapshot file> -C <HEIMDALL_DATA_DIRECTORY>

```

然後，再次啟動 Heimdall 服務。


### 5. 該從哪個位置建立 API 金鑰？ {#5-from-where-do-i-create-the-api-key}

您可以存取此連結：[https://infura.io/register](https://infura.io/register)。 請務必在設定帳戶和專案後，複製 Ropsten（而不是主網）的 API 金鑰。

系統會依預設選取主網。

### 6. Heimdall 無法運作。 我收到「Panic」（緊急）錯誤 {#6-heimdall-isn-t-working-i-m-getting-a-panic-error}

**實際錯誤**：我的 Heimdalld 無法運作。 在日誌中，第一行為：
緊急：未知的 db_backend leveldb，預期 goleveldb、memdb 或 fsdb

將 config.toml 中的設定變更為 `goleveldb`


### 7. 如何刪除 Heimdall 和 Bor 的殘餘項目？ {#7-how-do-i-delete-remnants-of-heimdall-and-bor}

若要刪除 Heimdall 和 Bor 的殘餘項目，您可以執行以下命令
Bor：

適用於 Linux 套件：

```$ sudo dpkg -i matic-bor```

並刪除 Bor 目錄：

```$ sudo rm -rf /etc/bor```

適用於二元函數：

```$ sudo rm -rf /etc/bor```

和

```$ sudo rm /etc/heimdall```


### 8. 可以同時有多少個作用中的驗證者？ {#8-how-many-validators-can-be-active-concurrently}

一次最多會有 100 個作用中的驗證者。 如果在活動中途達到上限，我們也會引入更多參與者。 請注意，作用中驗證者大多是正常運作時間較高的人。 將會強制要求具有高停機時間的參與者離開。

### 9. 應質押多少數量？ {#9-how-much-should-i-stake}

「stake-amount」和「heimdall-fee-amount」- 應為多少？

質押數量至少需要 10 個 Matic 代幣，而 Heimdall 費用應大於 10 個。例如，如果您的質押數量為 400 個，則 Heimdall 費用應為 20 個。建議將 Heimdall 費用保持在 20 個。

不過，請注意，質押數量和 heimdal-fee-amount 中輸入的值應以 18 位小數輸入

例如：

    heimdallcli stake --staked-amount 400000000000000000000  --fee-amount 1000000000000000000 --validator 0xf8d1127780b89f167cb4578935e89b8ea1de774f


### 10. 已選定讓我成為驗證者，但我的 ETH 地址不正確。 該怎麼辦？ {#10-i-was-selected-to-become-a-validator-but-my-eth-address-was-incorrect-what-do-i-do}

如果您可存取您之前提交的 ETH 地址，您就可以將測試代幣從該帳戶轉移到目前帳戶。 然後，您可以發起設定節點程序。

如果您無法存取該 ETH 地址，我們將不會另行轉移您的代幣。 您可以再次在表單中使用正確的 ETH 地址重新註冊。

### 11. 我收到啟動橋的錯誤 {#11-i-m-getting-an-error-starting-the-bridge}

**錯誤**：「start」為未知物件，請嘗試「bridge help」（橋說明）。是否仍可忽略此錯誤？

檢查「哪個橋」- 如果是 `/usr/sbin/bridge`，則表示您沒有執行正確的「橋」程式。

請嘗試 `~/go/bin/bridge`，而不是 `(or $GOBIN/bridge)`


### 12. 我收到 dpkg 錯誤 {#12-i-m-getting-dpkg-error}

**錯誤**：「dpkg: error processing archive matic-heimdall_1.0.0_amd64.deb (--install): trying to overwrite '/heimdalld-rest-server.service', which is also in package matic-node 1.0.0」

這會發生主要是因為您機器上先前安裝的 Matic。 若要解決此錯誤，您可以執行：

`sudo dpkg -r matic-node`


### 13. 我不清楚在產生驗證者金鑰時應新增哪個私密金鑰？ {#13-i-m-not-clear-on-which-private-key-should-i-add-when-i-generate-validator-key}

要使用的私密金鑰是您錢包的 ETH 地址，其中會儲存您的 Polygon 測試網代幣。您可以使用一個綁定到表單上提交的地址的公開/私密金鑰組，來完成設定程序。


### 14. 有可以知道 Heimdall 是否已同步的方法嗎？ {#14-is-there-a-way-to-know-if-heimdall-is-synced}

您可以執行以下命令來進行檢查：

```$ curl [http://localhost:26657/status](http://localhost:26657/status)```

檢查 catching_up 的值。 若為 False，則表示節點已完全同步。


### 15. 如果有人成為了前 10 大質押者，他最終會如何獲得其 MATIC 獎勵？ {#15-what-if-someone-become-a-top-10-staker-how-he-will-receive-his-matic-reward-at-the-end}

階段 1 獎勵並非基於質押。 請參閱 https://blog.matic.network/counter-stake-stage-1-stake-on-the-beach-full-details-matic-network/ 以了解獎勵詳細資訊。 具有高質押的參與者不會自動符合此階段的獎勵資格。


### 16. 我應使用哪個 Heimdall 版本？ {#16-what-should-be-my-heimdall-version}

若要檢查您的 Heimdall 版本，您可以執行：

```heimdalld version```

階段 1 的正確 Heimdall 版本應為 `heimdalld version is beta-1.1-rc1-213-g2bfd1ac`


### 17. 我應在質押數量和費用金額中新增哪些值？ {#17-what-values-should-i-add-in-the-stake-amount-and-fee-amount}

質押數量至少需要 10 個 Matic 代幣，而 Heimdall 費用應大於 10 個。例如，如果您的質押數量為 400 個，則 Heimdall 費用應為 20 個。建議將 Heimdall 費用保持在 20 個。

不過，請注意，質押數量和 heimdal-fee-amount 中輸入的值應以 18 位小數輸入

例如：

    heimdallcli stake --staked-amount 400000000000000000000  --fee-amount 1000000000000000000 --validator 0xf8d1127780b89f167cb4578935e89b8ea1de774f


### 18. `~.heimsdall` 與 `/etc/heimsdall?` 有何差異？

`~/.heimsdall` 是您使用二元函數安裝方法時的 Ｈeimdall 目錄。`/etc/heimdall` 適用於 Linux 套件安裝方法。


### 19. 當我進行質押交易時，我收到「Gas Exceeded」（已超出燃料）錯誤 {#19-when-i-make-the-stake-transaction-i-m-getting-gas-exceeded-error}

發生此錯誤可能是因為質押或費用金額格式。 質押命令期間輸入的值必須有 18 位的小數。

不過，請注意，質押數量和 heimdal-fee-amount 中輸入的值應以 18 位小數輸入

例如：

    heimdallcli stake --staked-amount 400000000000000000000  --fee-amount 1000000000000000000 --validator 0xf8d1127780b89f167cb4578935e89b8ea1de774f


### 20. 我何時會有機會成為驗證者？ {#20-when-will-i-get-a-chance-to-become-a-validator}

我們正在階段 1 活動的整個過程中逐步新增驗證者。 我們將逐步發佈新的外部驗證者清單。 此清單將在 Discord 頻道上公佈。


### 21. 我可以在哪裡找到 Heimdall 帳戶資訊位置？ {#21-where-can-i-find-heimdall-account-info-location}

適用於二元函數：

    ~/.heimdalld/config folder

適用於 Linux 套件：

    /etc/heimdall/config


### 22. 我應在哪個檔案中新增 API 金鑰？ {#22-which-file-do-i-add-the-api-key-in}

建立 API 金鑰後，您必須在 `heimdall-config.toml` 檔案中新增 API 金鑰。


### 23. 我應在哪個檔案中新增 persistent_peers？ {#23-which-file-do-i-add-the-persistent_peers}

您可以在以下檔案中新增 persistent_peers：

    ~/.heimdalld/config/config.toml


### 24.「您是否已在未重設應用程式資料的情況下重設 Tendermint？」 {#24-did-you-reset-tendermint-without-resetting-your-application-s-data}

在這種情況下，您可以重設 Heimdall 設定資料，然後再次嘗試執行安裝。

    $ heimdalld unsafe-reset-all
    $ rm -rf $HEIMDALLDIR/bridge


### 25. 錯誤：無法解集設定錯誤 1 錯誤解碼 {#25-error-unable-to-unmarshall-config-error-1-error-s-decoding}

錯誤：`* '' has invalid keys: clerk_polling_interval, matic_token, span_polling_interval, stake_manager_contract, stakinginfo_contract`

發生此錯誤大多是因為有錯字，或缺少某些部分，或仍有殘餘項目的舊設定檔。您必須清除所有殘餘項目，然後再次嘗試進行設定。

### 26. 如何停止 Heimdall 和 Bor 服務 {#26-to-stop-heimdall-and-bor-services}

**適用於 Linux 套件**：

停止 Heimdall：`sudo service heimdalld stop`

停止 Bor：`sudo service bor stop` 或

1. `ps -aux | grep bor`。 取得 Bor 的 PID，然後執行以下命令。
2. `sudo kill -9 PID`

**適用於二元函數**：

停止 Heimdall：`pkill heimdalld`

停止橋：`pkill heimdalld-bridge`

停止 Bor：前往 CS-2001/bor，然後執行 `bash stop.sh`

### 27. 如何移除 Heimdall 和 Bor 目錄 {#27-to-remove-heimdall-and-bor-directories}

**適用於 Linux 套件**：
刪除 Heimdall：`sudo rm -rf /etc/heimdall/*`

刪除 Bor：`sudo rm -rf /etc/bor/*`

**適用於二元函數**：

刪除 Heimdall：`sudo rm -rf ~/.heimdalld/`

刪除 Bor：`sudo rm -rf ~/.bor`

### 28. 當您收到「錯誤的 Block.Header.AppHash。」錯誤時，該怎麼辦？ {#28-what-to-do-when-you-get-wrong-block-header-apphash-error}

發生此錯誤通常是因為 Infura 要求耗盡。 當您在 Polygon 上設定節點時，您可將 Infura 金鑰新增到設定檔 (Heimdall)。 根據預設，您每天可以有 100000 個要求，如果超過此上限，您就會遇到這類問題。 若要解決此錯誤，您可以建立新的 API 金鑰，然後將其新增到 `config.toml` 檔案。