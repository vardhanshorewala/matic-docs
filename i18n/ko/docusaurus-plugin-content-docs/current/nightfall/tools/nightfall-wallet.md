---
id: nightfall-wallet
title: 나이트폴 지갑
sidebar: Nightfall Wallet
description: "Polygon 나이트폴 지갑 가이드입니다."
keywords:
  - docs
  - matic
  - polygon
  - nightfall
  - wallet
image: https://matic.network/banners/matic-network-16x9.png

---

Polygon 나이트폴 지갑은 나이트폴 메인넷 베타 릴리스와 상호 작용할 수 있는
브라우저 지갑입니다.

:::info 나이트폴 지갑을 사용하여 입금, 이전 및 출금하기

### 제한 사항 {#restrictions}

나이트폴이 성숙 상태에 이르면 다음과 같은 제한 사항이 적용됩니다.


| ERC20 토큰 | 최대 입금 | 최대 출금 |
|-------------|-------------|--------------|
| 매틱 | 250매틱 | 1000매틱 |
| WETH | 0.25WETH | 1WETH |
| DAI | 250DAI | 1000DAI |
| USDT | 250USDT | 1000USDT |
| USDC | 250USDC | 1000USDC |

:::

:::caution 보안 조치

나이트폴 지갑은 Chrome 브라우저에서 테스트됩니다. 베타 기간에는 다른 브라우저의 경우 마일리지가
다르게 나타날 수 있습니다.

**나이트폴은 Chrome에서 사용하실 것을 강력히 권장합니다**.

:::



## 시작하기 {#getting-started}

Polygon 웹 [메인넷 지갑](https://wallet-beta.polygon.technology) 또는
[테스트넷 지갑](https://wallet.testnet.polygon-nightfall.technology/)을 방문하여 메타 마스크
계정을 연결하고 왼쪽에서 Polygon 지갑을 선택합니다. 메타 마스크와 관련해 도움이 필요한 경우,
[메타 마스크에 대한 Polygon 문서](../../develop/metamask/tutorial-metamask.md)를 참조해 주세요.

![](../imgs/tools-wallet/polygon-wallet-click-nf.png)

이제 지갑은 Polygon 네트워크로 전환하라는 메시지를 표시하고 메타 마스크 팝업이
나타나 전환을 확인하도록 요청합니다.

![](../imgs/tools-wallet/polygon-network.png)

그런 다음 지갑의 상단 섹션에서 드롭다운 메뉴를 클릭하여 `Polygon Nightfall`을 선택하면
이더리움 메인넷으로 전환하라는 새로운 요청이 나타납니다. Polygon 나이트폴로 작동할 수 있도록 요청을 수락해
이더리움 메인넷으로 전환해 주세요.

![](../imgs/tools-wallet/polygon-network-dropdown-nf.png)

테스트넷에서 작업하는 경우, 지갑 URL이 즉시 Polygon 나이트폴 지갑의 랜딩 페이지로 안내합니다.

![](../imgs/tools-wallet/wallet-main-screen.png)

첫 방문인 경우에는 나이트폴 지갑을 생성해야 합니다. 니모닉과 지갑을 차례로 생성하기 위한 팝업이 나타납니다. `Generate Mnemonic`을 클릭한 다음 `Create Wallet`을 클릭하세요. **이 지갑은 현재 장치에서만 사용할 수 있음을 참고해 주세요**.

![](../imgs/tools-wallet/generate-mnemonic-create-wallet.png)

:::caution 커밋 및 니모닉 백업하기

지갑 키와 트랜잭션은 브라우저(IndexedDb)에 보관됩니다. 나이트폴 지갑을 처음 액세스할 때 설정하는 니모닉과 동일합니다.

이 니모닉은 반드시 안전한 곳에 보관하세요. L2에서 자금과 호환 가능한 증명을 생성할 수 있는 유일한 방법입니다. 커밋에서도 마찬가지입니다. 다른 브라우저나 시스템을 사용할 때마다 `export commitments`를 클릭하여 반드시 안전하게 보관해야 합니다.

:::

**커밋을 잃어버리면 자금을 영원히 잃게 됩니다.**


이제 메타 마스크와 나이트폴 지갑 주소가 모두 보입니다(오른쪽 상단).

**트랜잭션을 시작하기 전에 지갑 설정이 완료되도록 몇 분 더 기다려 주세요**.

지갑의 왼쪽 하단 구석에 지갑 상태가 `Syncing Nightfall`로 표시됩니다. 이 상태에서 지갑은 트랜잭션을 수행하는 데 필요한
ZK 회로와 네트워크 상태를 가져옵니다.

![](../imgs/tools-wallet/wallet-state-syncing.png)

지갑 상태가 `Nightfall Synced`로 바뀔 때까지 기다려 주세요.

![](../imgs/tools-wallet/wallet-state-synced.png)


## 원장 하드웨어 지갑을 나이트폴에 연결하는 방법 {#how-to-connect-a-ledger-hardware-wallet-to-nightfall}
원장 하드웨어 지갑을 공식 메타 마스크 사이트의 메타 마스크와 연결하는 방법에 대한 가이드는 [여기](https://support.ledger.com/hc/en-us/articles/4404366864657-How-to-access-your-Ledger-Ethereum-ETH-account-via-Metamask?docs=true)에서 확인할 수 있습니다.

반드시 지갑의 이더리움 앱을 연결하고 이더리움 앱 설정에서 "블라인드 서명(blind signing)"을 활성화해 주세요.


### 지갑 주소 {#your-wallet-address}
`Receive`를 클릭하여 나이트폴 자산 페이지에서 나이트폴 지갑 주소를 가져올 수 있습니다.

![](../imgs/tools-wallet/nightfall-wallet-address.png)

## 입금하는 방법 {#how-to-make-deposits}
나이트폴 자산 페이지에서 선택한 자산의 오른쪽에 표시되는 `Deposit` 버튼을 클릭하거나 L2 브리지 페이지로 이동합니다.

1. 이전 모드가 `Deposit`으로 설정되어 있는지 확인합니다.
2. 원하는 토큰이 선택되었는지 확인합니다(WETH, 매틱 등).
3. 나이트폴 지갑에 입금할 값을 입력하고 `Transfer`를 클릭합니다.
4. 팝업에 표시된 트랜잭션을 검토합니다.
5. `Create Transaction`을 클릭합니다.

![](../imgs/tools-wallet/deposit-click-transfer.png)

ZKP를 계산하고 트랜잭션을 준비하는 프로세스가 시작되어 메타 마스크에 계정 잔액을 액세스할 수 있는 권한을 부여합니다. 이 작업이 끝나면 `Send Transaction`을 클릭하여 메타 마스크에 계약 상호 작용을 위한 추가 권한을 부여하세요.

![](../imgs/tools-wallet/deposit-tx-created-and-ready-to-be-sent.png)

트랜잭션 페이지로 가서 [입금 결과를 확인](#view-transactions)합니다.

### 입금에 대한 중요 정보 {#important-information-about-deposits}
- 베타 단계에서는 [입금 금액이 제한됩니다](#note-the-following-deposit-and-withdrawal-restrictions).

## 이전하는 방법 {#how-to-make-transfers}
나이트폴 자산 페이지에서 선택한 자산의 오른쪽에 표시되는 `Send` 버튼을 클릭합니다.

1. Polygon 나이트폴 L2에 존재하는 유효한 주소를 입력합니다.
2. 원하는 토큰이 선택되었는지 확인합니다(WETH, 매틱 등).
3. 나이트폴 지갑에서 이전할 값을 입력하고 `Continue`를 클릭합니다.

![](../imgs/tools-wallet/send-nf.png)

ZKP를 계산하고 트랜잭션을 준비하는 프로세스가 시작됩니다. 이 작업이 끝나면 `Send Transaction`을 클릭합니다.

트랜잭션 페이지로 가서 [이전 결과를 확인](#view-transactions)합니다.

### 이전에 대한 중요 정보 {#important-information-about-transfers}
현재 나이트폴에서 사용되는 ZKP 이전 회로는 기존 커밋 중 하나와 정확히 일치하는 금액으로
또는 기존 두 개 커밋의 선형 결합으로 이전 금액을 제한합니다.

이전 금액 제한을 설명하기 위해 다음의 커밋 세트를 이용한 예가 나와 있습니다.

- 세트 A: [1, 1, 1, 1, 1, 1]
- 세트 B: [2, 2, 2]
- 세트 C: [2, 4]

세 개 세트 모두 각 총합은 6이지만, 다음의 이전만 가능합니다.

- 세트 A: 0과 2 사이의 모든 이전(0과 2는 제외)
- 세트 B: 0과 4 사이의 모든 이전(0과 4는 제외)
- 세트 C: 0과 6 사이의 모든 이전(0과 6은 제외)

계속 이 예시를 이용해 설명하자면, 만약 알렉스가 세트 C의 커밋을 보유한 경우, 가능한 이전에는 0과 6 사이의 모든 금액이 포함되며 제한 값인 0과 6은 제외됩니다. 알렉스가 로버트에게 3.5를 이전하기로 결정하면 알렉스는 결국 2.5의 단일 커밋을 갖게 되고 로버트는 블록이 제안되면 3.5의 커밋을 받게 됩니다.

만약 알렉스가 로버트에게 6이라는 금액을 이전하기로 결정할 경우에는 유효한 커밋 결합이 없어 ZK 증명이 실패하게 됩니다.

**여기서 명심할 중요한 사항은 이러한 값이 소유한 커밋을 나타내며** 예시 입금액이 아니라는 것입니다. 이러한 문서의 [커밋](../protocol/commitments.md) 섹션에 보다 자세한 내용이 나와 있습니다.

## 출금하는 방법 {#how-to-make-withdrawals}
나이트폴 자산 페이지에서 선택한 자산의 오른쪽에 표시되는 `Withdraw` 버튼을 클릭하거나 L2 브리지 페이지로 이동합니다.

1. 이전 모드가 `Withdraw`로 설정되어 있는지 확인합니다.
2. 원하는 토큰이 선택되었는지 확인합니다(WETH, 매틱 등).
3. 나이트폴 지갑에서 출금할 값을 입력하고 `Transfer`를 클릭합니다.
4. 팝업에 표시된 트랜잭션을 검토합니다.
5. `Create Transaction`을 클릭합니다.

ZKP를 계산하고 트랜잭션을 준비하는 프로세스가 시작됩니다. 이 작업이 끝나면 `Send Transaction`을 클릭합니다.

트랜잭션 페이지로 가서 [출금 결과를 확인](#view-transactions)합니다. 일주일의 최종화 기간이 끝나면 사용자는
최종화하고 출금 금액을 청구할 수 있습니다.

### 출금에 대한 중요 정보 {#important-information-about-withdrawals}
- 출금 값은 소유한 커밋 중 하나의 금액과 정확히 일치해야 합니다([커밋에 대한](#learn-about-commitments) 보다 자세한 내용 확인).
- 출금에는 출금 트랜잭션이 포함된 블록이 생성된 시점부터 **일주일**의 최종화 기간이 있습니다. 이 기간이 지나면 출금을 최종화하여 이더리움 계정으로 자금을 보낼 수 있습니다.
- 베타 단계에서는 [출금 금액이 제한됩니다](#note-the-following-deposit-and-withdrawal-restrictions).
- 출금은 온체인 트랜잭션이며, 트랜잭션이 요청될 때와 출금이 최종화될 때 가스 요금을 지불합니다.

![](../imgs/tools-wallet/cooling-off-vs-ready.png)

## 트랜잭션 보기 {#view-transactions}
트랜잭션 페이지에서 입금, 이전 및 출금의 상태를 확인할 수 있습니다. 각 트랜잭션은 블록을 생성하기에 충분한 트랜잭션이 모이는 즉시 또는 6시간 후에 처리됩니다.

![](../imgs/tools-wallet/transactions.png)
