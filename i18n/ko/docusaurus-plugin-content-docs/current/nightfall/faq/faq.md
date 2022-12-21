---
id: faq
title: FAQ
sidebar_label: FAQ
description: 나이트폴 관련 자주 묻는 질문
keywords:
  - docs
  - polygon
  - nightfall
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip

이 목록에 질문이 없으면 <ins>**[Polygon 나이트폴 Discord 서버](https://discord.com/invite/pZkC3JV2bR)**</ins>에서 질문을 제출하십시오.

:::

## 스마트 계약은 어디에서 찾을 수 있습니까? {#where-can-i-find-the-smart-contracts}

Polygon 나이트폴 계약은 [테스트넷 Goerli](../deployments/testnet.md)와 [Mainnet](../deployments/mainnet.md)에 배포되었습니다.

## Polygon 나이트폴의 보안 감사는 어떤 상태입니까? {#what-s-the-state-of-polygon-nightfall-s-security-audit}
현재 Polygon 나이트폴은 3분기에 완료될 예정인 보안 감사를 받고 있습니다. 그동안 프로토콜에 몇 가지 제한이 추가되었습니다.

- 단일 제안자 운영 및 Polygon의 관리
- [입출금 제한 금액](../tools/nightfall-wallet.md#deposit-and-withdraw-restrictions)

## 나이트폴 지갑은 어떻게 설정합니까? {#how-do-i-set-up-my-nightfall-wallet}
Polygon 나이트폴 지갑을 시작하는 방법과 관련하여 모든 세부 정보를 담고 있는 완전한 지갑 지침서를 [여기](../tools/nightfall-wallet.md)에서 확인해 보십시오.

## Ledger 하드웨어 지갑을 나이트폴 지갑에 연결하려면 어떻게 해야 합니까? {#how-do-i-connect-a-ledger-hardware-wallet-to-nightfall-wallet}
[Ledger 하드웨어 지갑을 메타 마스크와 연결하는 방법](../tools/nightfall-wallet.md#how-to-connect-a-ledger-hardware-wallet-to-nightfall)에 대해 설명하는 지갑 지침서의 섹션을 참조하십시오.

## Polygon 나이트폴 네트워크에서 시작부터 완료까지 이전에 소요되는 시간은 얼마나 됩니까? {#how-long-do-transfers-take-on-polygon-nightfall-network-from-start-to-finish}
현재 제안자는 사용자로부터 트랜잭션을 받아 최대 32개의 트랜잭션으로 구성된 블록을 생성합니다. 블록을 구축하기에 충분한 트랜잭션이 수집되면 바로 트랜잭션이 처리됩니다.

또한, 6시간마다 최소 하나의 블록이 제안될 수 있도록 블록 생성 기간에 상한이 있습니다(제안자가 수집하는 트랜잭션의 수와 관계없음).

## 누구와 거래할 수 있습니까? {#who-can-i-transact-with}
Polygon 나이트폴 내에서 자산을 이전하려는 경우 `Destination Wallet Address`만 있으면 됩니다. 자금 수신을 위해 [지갑 주소를 공유하는 방법](../tools/nightfall-wallet.md#your-wallet-address)을 알아보려면 지갑 지침서를 참조하십시오.

## 커밋먼트는 어디에 백업됩니까? {#where-are-commitments-backed-up}

비밀 키가 귀하를 벗어나지 않도록 영지식 증명은 브라우저에서 계산되며 지갑은 IndexedDb에서 귀하가 소유한 모든 커밋먼트를 추적합니다. 이 데이터에 대한 액세스 권한을 가진 사람은 귀하가 어떤 커밋먼트를 소유하고 있는지 알아낼 수 있지만, 귀하의 키 없이 이를 훔칠 수는 없습니다. 키는 니모닉을 입력할 때만 복호화됩니다. 따라서 신뢰하는 기계에서만 지갑을 사용해야 합니다.

현재 이 데이터는 어디로도 내보낼 수 없습니다. 따라서 다른 기계에서 브라우저를 사용하는 경우에는 IndexedDB 콘텐츠를 이전하지 않는 한 귀하의 커밋먼트에 액세스할 수 없습니다. 당사는 지갑을 통해 커밋먼트를 내보내고 가져올 수 있는 메카니즘을 제공합니다.

## 트랜잭션 프라이버시 {#privacy-of-transactions}
입금 및 출금 트랜잭션은 비공개가 아님을 이해하는 것이 중요합니다. 비공개가 아닌 레이어 1과 상호 작용을 하기 때문입니다. 즉, 모든 사람이 레이어 2 커밋먼트의 생성 여부와 포함 금액을 알고 있습니다. 마찬가지로, 레이어 2 커밋먼트를 파기하고 토큰을 레이어 1으로 반환하면, 누가 얼마나 그것을 수신했는지를 모든 사람이 알 수 있습니다.

프라이버시는 전적으로 레이어 2 이내의 이전에서 비롯됩니다. 이더리움 블록체인의 관점에서 이는 완전히 비공개입니다. 블록 제안자에게 이전 트랜잭션을 보낼 때 IP 주소가 유출되는 유일한 데이터입니다. 초기 베타의 경우 Polygon은 가장 적합한 제안자만을 운영합니다.


## 출금 방법 {#how-to-withdraw-funds}
자금은 Polygon 나이트폴 지갑을 통해 출금할 수 있습니다. 출금에는 출금 트랜잭션이 포함된 블록이 생성된 시점부터 **일주일**의 최종화 기간이 있습니다. 이 기간이 지나면 출금을 최종화하여 이더리움 계정으로 자금을 보낼 수 있습니다.

## 나이트폴에서 트랜잭션 비용은 얼마입니까? {#how-much-will-transactions-cost-on-nightfall}
상이한 비용을 부담하는 두 가지 유형의 트랜잭션이 있습니다.

- 온체인 트랜잭션: 이 트랜잭션은 스마트 계약으로 전송되며 채굴될 이더리움에 대해 가스 요금을 지불해야 합니다. 어떤 제안자든 이 트랜잭션을 수신하여 블록에 포함시킬 수 있습니다. 현재 `deposit`과 `finalize withdrawal`이 온체인 트랜잭션입니다.
- 오프체인 트랜잭션: 이 트랜잭션은 제안자에게 직접 전송됩니다. 현재 모든 `transfer` 및 `withdrawals`가 오프체인 트랜잭션으로 구성됩니다.

## 나이트폴 네트워크에서는 어떤 토큰을 사용할 수 있습니까? {#which-tokens-can-i-use-on-nightfall-network}
나이트폴에서는 다음 토큰이 작동합니다.

- 매틱
- WETH
- DAI
- USDC

## 나이트폴을 사용하려면 매틱 토큰이 필요합니까? {#do-i-need-matic-tokens-to-use-nightfall}
예. `transfers` 및 `withdrawals`의 지불을 위해 나이트폴에 일부 매틱 토큰을 입금해야 합니다.

## 어디에서 버그 보고서를 제출하거나 나이트폴에 문의하여 추가 지원을 받을 수 있습니까? {#where-can-i-submit-a-bug-report-or-contact-nightfall-for-additional-help}
가장 좋은 방법은 [Polygon 나이트폴 Discord 서버](https://discord.com/invite/pZkC3JV2bR)에 가입하여 질문을 제출하는 것입니다.
