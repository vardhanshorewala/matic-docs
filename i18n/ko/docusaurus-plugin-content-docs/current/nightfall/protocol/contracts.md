---
id: contracts
title: 스마트 계약
sidebar_label: Smart Contracts
description: "쉴드, 제안자, 챌린지, 머클 트리 계산"
keywords:
  - docs
  - polygon
  - nightfall
  - smart
  - contracts
  - shield
image: https://matic.network/banners/matic-network-16x9.png
---

계약은 네트워크에서 작동하기 위해 각 나이트폴 행위자가 따라야 하는 규칙을 정의합니다.
스마트 계약에는 다음이 포함됩니다.

- [Shield.sol](#shield)
- [Proposers.sol](#proposers)
- [Challenges.sol](#challenges)
- [MerkleTree_Computations.sol](#merkletree_computations)

## 쉴드 {#shield}
이 계약을 통해 사용자는 제안자가 처리할 트랜잭션을 제출할 수 있습니다. 입금 트랜잭션의 경우 지불이 수반됩니다.
또한, 누구든지 쉴드 계약(커밋먼트 루트 및 널리파이어 목록) 상태의 업데이트를 요청할 수 있습니다.
상태가 업데이트되면 업데이트의 모든 출금이 처리됩니다.

기본적으로 블록체인에 이전 또는 출금 트랜잭션을 게시할 필요는 없습니다.
이것은 제안자가 트랜잭션을 선택하여 레이어 2 블록에 통합할 수 있도록 단순히 메시지 보드의 역할을 합니다.

나이트폴은 실제 ERC 계약과 상호 작용하기 때문에 다음 확인 작업은 비공개로 처리될 수 없습니다.

- **입금/출금** 동안 ERC 토큰 주소가 유효합니다.
- **입금** 동안 사용자가 커밋먼트를 생성할 수 있는 잔액 또는 토큰을 소유하고 있습니다.

## 제안자 {#proposers}
계약에는 제안자의 등록/등록 취소/교체 및 제안자에 대한 지불을 처리하고 새로운 레이어 2 블록을 블록체인에 제안할 수 있는 기능이 포함되어 있습니다.
나이트폴의 첫 번째 버전은 Polygon에서 운영하는 단일 부트 제안자만 허용합니다. 앞으로의 버전에서는 이 제한이 해제되어 복수의 제안자가 허용될 것입니다.

## 챌린지 {#challenges}
부정확한 것으로 블록에 이의를 제기할 수 있는 기능입니다.

## MerkleTree_Stateless {#merkletree_stateless}
최초 `MerkleTree.sol`의 스테이트리스(순수 함수) 버전으로, 온체인에서 블록 챌린지 계산을 지원하기 위해 `Challenges.sol`에 의해 사용됩니다.

## 기타 계약 {#other-contracts}
- `Utils.sol` - 복수의 계약에서 사용되거나 인라인 상태로 두면 코드 가독성에 영향을 미칠 수 있는 기능을 함께 수집합니다.
- `Config.sol` - Node.js 구성 파일과 유사한 상수를 보관합니다.
- `Structures.sol` - 글로벌 구조, enum, 이벤트, 매핑, 상태 변수를 정의합니다. 이 계약을 통해 이러한 것들을 더 쉽게 찾을 수 있습니다.

## 업그레이드 가능성 {#upgradability}
적어도 초기에 Polygon은 배포 뒤 나이트폴 계약을 업그레이드할 수 있는 권한을 보유합니다.
당사는 Openzeppelin의 트러플용 [업그레이드 플러그인](https://docs.openzeppelin.com/upgrades-plugins/1.x/)을 사용하여 이 작업을 수행합니다.

Polygon은 [배포자](https://github.com/EYBlockchain/nightfall_3/tree/master/nightfall-deployer) 모듈을 사용하여 계약을 업그레이드합니다.
`deployer`의 마이그레이션 폴더에는 4개의 마이그레이션이 저장되어 있습니다.
첫 세 가지 마이그레이션은 Polygon 나이트폴 계약 세트의 '정상' 배포를 수행합니다. 그러나
나중에 업그레이드될 수 있도록 모든 계약(라이브러리는 아님)을 프록시와 함께
배포합니다. 네 번째 마이그레이션은 계약을 업그레이드하는 데 사용됩니다.
