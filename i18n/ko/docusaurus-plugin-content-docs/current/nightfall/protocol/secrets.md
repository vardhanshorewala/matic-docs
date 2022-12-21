---
id: secrets
title: 밴드 내 비밀 배포
sidebar_label: In Band Secret Distribution
description: "비밀을 암호화하고 복호화를 보장하는 솔루션"
keywords:
  - docs
  - polygon
  - nightfall
  - secret
  - encryption
  - key
image: https://matic.network/banners/matic-network-16x9.png
---
import katex from 'katex';

## 개요 {#overview}

수신자가 커밋먼트를 소비하는 데 필요한 비밀 정보를 수신할 수 있도록 발신자는
수신자에게 전송할 커밋먼트의 비밀(*솔트*, *값*, *tokenId*, *ercAddress*)을 암호화하고
수신자의 공개 키로 이를 올바르게 암호화했음을 ZKP를 사용하여 증명합니다. [**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf) 하이브리드 암호화 패러다임을 사용합니다.

## KEM-DEM 하이브리드 암호화 {#kem-dem-hybrid-encryption}


### 키 생성 {#key-creation}

유한 필드 `Fp`에 대해 타원 곡선(여기에서는 Baby Jubjub 커브 사용) `E`를 사용합니다. `p`는
큰 소수이고 `G`는 생성기입니다.

Alice는 임의의 임시 비대칭 키 쌍   를 생성합니다.
$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

이 키는 한 번만 사용되고 이 트랜잭션에 고유하므로 완전 순방향 비밀성을 제공합니다.

### 암호화 {#encryption}

이 암호화 프로세스는 2단계로 진행됩니다. 즉, 공유된 비밀로부터 대칭 암호화 키를 도출하는 KEM 단계와 암호화 키를 사용하여 평문을 암호화하는 DEM 단계입니다.

### 키 캡슐화 방법(암호화) {#key-encapsulation-method-encryption}
이전에 생성된 비대칭 개인 키와 표준 Diffie-Hellman을 사용하여 공유된 비밀 $key_{DH}$를 획득합니다. 암호화 키를 얻기 위해 이것을 임시 공개 키와 함께 해싱합니다.

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


주:  
  : 수신자의 공개 키  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### 데이터 캡슐화 방법(암호화) {#data-encapsulation-method-encryption}
서킷 효율성을 위해 카운터 모드의 블록 암호가 사용됩니다. 여기에서 암호 알고리즘은 mimc 해시입니다. 임시 키는 각 트랜잭션에 고유하므로 난스를 포함시킬 필요가 없습니다. $i^{th}$ 메시지의 암호화는 다음과 같습니다.

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

주:  

$Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

그런 다음 발신자는 수신자에게 $(Q_e, \text{ciphertexts})$를 제공합니다. 온체인으로 전송되는 트랜잭션 구조의 일부로 포함됩니다.

### 복호화 {#decryption}
복호화를 위해 수신자는 약간 변형된 버전의 KEM-DEM 단계를 수행합니다.

### 키 캡슐화 방법(복호화) {#key-encapsulation-method-decryption}
$Q_e$를 토대로 수신자는 다음 단계를 수행하여 로컬에서 암호화 키를 계산할 수 있습니다.

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

주:  
  : 임시 공개 키  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### 데이터 캡슐화 방법(복호화) {#data-encapsulation-method-decryption}
$key_{enc}$ and an array of ciphertexts, the $i_{th}$ 그리고 다음을 통해 평문을 복구할 수 있습니다.

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

주:  

$Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## 암호화, 커밋먼트 소유권, 소비와 관련된 다양한 키의 추출 및 생성 {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

BIP39를 사용하여 12개 단어의 `mnemonic`을 생성하고 `mnemonicToSeedSync`를 호출하여 이로부터 `seed`를 생성합니다.
그런 다음 BIP32 및 BIP44의 표준을 따라 이 `seed` 및 `path`를 토대로 `rootKey`를 생성합니다.

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

`rootKey` 또는 `mnemonic`이 손상되면 공격자가 `zkpPrivateKey` 및 `nullifierKey`를 계산할 수 있습니다.
`zkpPrivateKey`는 커밋먼트의 비밀을 복호화하는 데 사용될 수 있고 `nullifierKey`는 커밋먼트를 소비하는 데 사용될 수 있습니다.
그러므로 `rootKey`와 `mnemonic`은 매우 안전하게 보관해야 합니다.

`ZkpKeys`를 사용하여 이러한 키를 생성하는 앱은 Shamir의 비밀 공유 기법을 사용하여 조각들로 분할하여 각기 다른 장치에 `rootKey`를
보관할 수 있습니다.

또한, `zkpPrivateKey` 및 `nullifierKey`를 분리하여 저장하는 것을 권장합니다. 둘 중 하나가 손상되는 경우
커밋먼트의 도난을 방지할 수 있습니다.

아래 그림은 나이트폴에서 다양한 키를 도출하는 단계를 보여줍니다.
![](../imgs/key-derivation.png)
