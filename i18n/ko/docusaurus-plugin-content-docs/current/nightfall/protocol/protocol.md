---
id: protocol
title: 나이트폴 프로토콜
sidebar_label: Nightfall Protocol
description: "나이트폴 프로세스"
keywords:
  - docs
  - polygon
  - nightfall
  - protocol
  - chain
  - block
  - structure
  - layer
image: https://matic.network/banners/matic-network-16x9.png
---

최소 1명의 제안자가 시스템에 등록하여 최소 스테이크를 게시한다고 가정합니다.

## 트랜잭션 게시 {#transaction-posting}
새로운 트랜잭션을 게시하는 데는 두 가지 메카니즘이 있습니다.

- [온체인](#on-chain)
- [오프체인](#off-chain)

### 온체인 {#on-chain}
이 프로세스는 `Shield.sol`에서 `submitTransaction`을 호출하여 트랜잭션을 생성하는 거래자로부터 시작됩니다. 거래자는 트랜잭션을 위해 쉴드 계약에 수수료를 지불하며, 금액은 거래자가 결정할 수 있습니다. 이 금액은 트랜잭션을 블록에 통합하는 제안자에게 지급됩니다. 현재 제안자와 기본 옵티미스트 인스턴스는 채굴자와 상당히 유사하게 더 높은 수수료를 선택하여 블록에 통합시킬 가능성이 높습니다.
트랜잭션 호출이 발생하면 세부 정보를 포함한 블록체인 이벤트가 게시됩니다. 입금의 경우, 쉴드 계약은 해당하는 레이어 1 ERC 토큰을 받습니다.

### 오프체인 {#off-chain}
이전 및 출금 트랜잭션에는 위의 프로세스를 통해 온체인으로 제출하지 않고 대기 중인 제안자에게 직접 제출할 수 옵션이 있습니다.
이러한 오프체인 트랜잭션을 선택하는 거래자는 입금에 드는 온체인 제출 비용(~45,000 가스)을 절약할 수 있지만, 연결 대상으로 선택하는 제안자와 거래자 사이에는 더 높은 수준의 신뢰가 요구됩니다. 불량하게 행동하는 제안자는 온체인으로 받는 트랜잭션보다 오프체인으로 받는 트랜잭션을 더 쉽게 검열할 수 있습니다. 이러한 트랜잭션은 대기 중인 모든 제안자에게 브로드캐스트되지 않기 때문입니다. 이 경우 거래자는 쿨링오프 기간(1주일)이 경과한 때에만 트랜잭션을 신뢰할 수 있는 것으로 간주해야 합니다.

## 트랜잭션 수락 {#transaction-acceptance}
제안자는 트랜잭션을 수신하면 다양한 검사를 수행하여 트랜잭션이 제대로 구성되었는지 그리고 증명이 공개 입력 해시를 토대로 검증하는지를 확인합니다.
모든 검사를 통과하면 트랜잭션은 제안자의 멤풀에 추가되고 블록에 포함된 것으로 간주됩니다.

## 블록 어셈블리 및 제출 {#block-assembly-and-submission}
제안자는 쉴드 계약을 통해 현재 제안자로 지정될 때까지 대기합니다.
현재 제안자는 자신의 내부 옵티미스트 인스턴스에서 멤풀의 트랜잭션을 포함하는 새로운 블록을 수신합니다. 각 트랜잭션에 대해 새로운 커밋먼트 머클 트리를 계산합니다. 커밋먼트 머클 트리는 트랜잭션이 쉴드 계약에 추가되는 경우 생성됩니다.

따라서 블록에 포함된 트랜잭션의 해시와 블록 내 모든 트랜잭션을 처리한 후 존재하게 될 커밋먼트 머클 트리 루트(커밋먼트 루트)가 블록에 담깁니다. 이후 제안자는 이 블록을 상태 스마트 계약에 보냅니다.

블록이 제안되면 다음 정보가 온체인으로 기록됩니다.

- 블록 데이터 구조
```
  struct Block {
    uint48 leafCount; // note this is defined to be the number of leaves BEFORE the commitments in this block are added
    address proposer;
    bytes32 root; // the 'output' commitment root after adding all commitments
    uint256 blockNumberL2;
    bytes32 previousBlockHash;
    bytes32 transactionHashesRoot;
  }
```
- 블록 내 트랜잭션
```
    struct Transaction {
        uint112 value;
        uint112 fee;
        TransactionTypes transactionType;
        TokenType tokenType;
        uint64[2] historicRootBlockNumberL2; // number of L2 block containing historic root
        uint64[2] historicRootBlockNumberL2Fee; //number of L2 block containing historic root fee
        bytes32 tokenId;
        bytes32 ercAddress;
        bytes32 recipientAddress;
        bytes32[2] commitments;
        bytes32[2] nullifiers;
        bytes32[1] commitmentFee;
        bytes32[2] nullifiersFee;
        bytes32[2] compressedSecrets;
        uint256[4] proof;
    }
```

## 이의 제기 {#challenges}
블록은 일주일 동안 대기열에서 이의 제기를 받을 수 있습니다. 이 기간 동안에는 이의 제기 함수 중 하나를 호출하여 정확성에 이의를 제기할 수 있습니다. 가능한 이의 제기는 다음과 같습니다.

- **INVALID_PROOF** - 트랜잭션에 제공된 증명이 참으로 확인되지 않습니다.
- **INVALID_PUBLIC_INPUT_HASH** - 트랜잭션의 공개 입력 해시가 공개 입력의 올바른 해시가 아닙니다.
- **HISTORIC_ROOT_EXISTS** - 트랜잭션 증명을 생성하는 데 사용된 커밋먼트 머클 트리의 루트가 존재한 적이 없습니다.
- **DUPLICATE_NULLIFIER** - 트랜잭션의 일부로 제공된 널리파이어가 소비된 널리파이어 목록에 있습니다.
- **HISTORIC_ROOT_INVALID** - 블록 내 트랜잭션 처리로 인해 업데이트된 커밋먼트 루트가 올바르지 않습니다.
- **DUPLICATE_TRANSACTION** - 이 블록에 포함된 트랜잭션과 동일한 것이 이미 이전 블록에 포함되었습니다.
- **TRANSACTION_TYPE_INVALID** - 트랜잭션 유형(예: 입금, 이전, 출금)에 따라 트랜잭션이 제대로 형성되지 않았습니다.

이의 제기에 성공하면(즉, 온체인 계산을 통해 유효한 이의 제기로 입증되는 경우) 다음 조치가 수행됩니다.

- 대기열에서 해당 블록의 해시와 모든 후속 블록이 제거됩니다.
- 제안자가 제출한 블록 스테이크가 이의 제기자에게 지급됩니다.
- 블록에 트랜잭션을 보유한 거래자는 제안자에게 지급한 수수료를 환급받습니다. 입금 트랜잭션의 경우 쉴드 계약이 보관한 모든 에스크로 자금이 포함됩니다.

