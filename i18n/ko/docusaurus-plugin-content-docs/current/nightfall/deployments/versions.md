---
id: versions
title: 히스토리
sidebar_label: History of changes
description: "배포 버전"
keywords:
  - docs
  - polygon
  - nightfall
  - changelog
image: https://matic.network/banners/matic-network-16x9.png
---


## 베타 1.0 {#beta-1-0}
베타 1.0은 2022년 5월 17일에 릴리스되었습니다. 여기에는 나이트폴 개념 증명을 배포하기 위한 기본 메카니즘이 포함되었습니다.
단일 `Proposer`와 트랜잭션의 첫 번째 `coarse` 구현을 지원했습니다. 또한 사용자 지갑의
예비 버전을 제공했습니다.
배포 버전은 [여기](https://github.com/EYBlockchain/nightfall_3/commit/bc3e475de3e2877f14430f9599e5b38ea960765b)에서 확인할 수 있습니다.

## 베타 2.0 {#beta-2-0}
배포 버전은 [여기](https://github.com/EYBlockchain/nightfall_3/commit/4c2af01ac95af5ea6f5b40071d73a1624f06ba46)에서 확인할 수 있습니다.
몇 가지 개선이 이루어졌습니다.
- **수수료 징수**

제안자가 수집하는 거래에 대해 수수료를 징수할 수 있는 능력. 이 기능은 여러 제안자에게 인센티브를 제공할 것입니다.
- **챌린저 배포**

이제 네트워크에는 제안자의 블록을 모니터링하는 챌린저가 포함되어 있습니다.
- **서킷 트랜잭션**

모든 트랜잭션의 ZKP를 생성할 때 유연성과 성능이 향상됩니다.  `transfer` 및 `withdrawal` 모두 최대 2개의 커밋먼트 및 반환 변경을 수락합니다.
성능 측면에서는 이제 트랜잭션이 최적화되어 증명 시간을 단축할 수 있습니다.

| 작업 | 이전 제약 | 이후 제약 |
|-----------|--------------------|------------------|
| 입금 | 84,766 | 1277 |
| 이전 | 499,119 | 67,694 |
| 출금 | 168,883 | 53,348 |

일부 최적화는 포세이돈으로 전환함으로써 가능했습니다.

- **비밀 암호화**

El-Gamal에서 [KEM-DEM](../protocol/secrets) 암호화 프로세스로 이전하여 몇 가지 혜택을 얻었습니다.
- 암호화/복호화 프로세스 단순화
- 제약 및 온체인 가스 비용의 감소

- **챌린저 배포**

