---
id: secrets
title: In Band Secret Distribution
sidebar_label: In Band Secret Distribution
description: "用于加密保密信息，并确保其解密的解决方案。"
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

## 概述 {#overview}

要确保接受人收到花费其承诺所需的保密信息，发送者需对发送给接受者的承诺的保密信息（*加密盐*、*价值*、*代币 ID*、*ercAddress*）进行加密，并使用 ZKP 证明他们已使用接受者的公钥对此进行了正确的加密。它采用 [**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf) 混合加密模式。

## KEM-DEM 混合加密 {#kem-dem-hybrid-encryption}


### 密钥创建 {#key-creation}

在有限域 `Fp` 中使用椭圆曲线（在本例中我们使用 Baby Jubjub 曲线）`E`，其中，`p` 是一个数值较大的素数，而 `G` 为生成者。

Alice 生成随机临时非对称密钥对   :
$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

这些密钥仅使用一次，并且对此交易具有唯一性，为我们提供了完美的前向保密性。

### 加密 {#encryption}

加密流程分为两步：其一，KEM，从共享保密信息中导出对称加密密钥；其二，DEM，使用加密密钥对明文进行加密。

### 密钥封装方法（加密） {#key-encapsulation-method-encryption}
使用此前生成的不对称私钥，我们获得了一条共享保密信息，$key_{DH}$，使用标准 Diffie-Hellman。我们对它和临时公钥进行哈希计算，得出加密密钥。

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


其中，  
  为接受者的公钥  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### 数据封装方法（加密） {#data-encapsulation-method-encryption}
为了提高回路的效率，我们使用的加密方式是计数器模式下的区块密码，密码算法为 mimc 哈希。鉴于临时密钥对于每项交易而言都是唯一的，因此没有必要使用 nonce。$i^{th}$ 消息的加密如下：

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

其中，  

$Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

然后，发送者向接受者提供 $(Q_e, \text{ciphertexts})$。这些内容是链上发送的交易结构的一部分。

### 解密 {#decryption}
要解密，接受者需执行略经调整的 KEM-DEM 版本。

### 密钥封装方法（解密） {#key-encapsulation-method-decryption}
给定 $Q_e$，接受者可以通过执行以下步骤，本地计算加密密钥。

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

其中，  
  为临时公钥  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### 数据封装方法（加密） {#data-encapsulation-method-decryption}
利用$key_{enc}$ and an array of ciphertexts, the $i_{th}$，明文可以通过以下方式恢复：

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

其中，  

$Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## 加密、拥有承诺及其花费所涉及的各种密钥的衍生和生成 {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

使用 BIP39 生成由 12 个词组成的 `mnemonic`，并据此通过调用 `mnemonicToSeedSync` 生成 `seed`。然后遵循 BIP32 和 BIP44 标准，基于 `seed` 和 `path` 生成 `rootKey`。

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

如果 `rootKey` 和 `mnemonic` 之一遭攻破，则对手可以计算出 `zkpPrivateKey` 和 `nullifierKey`。`zkpPrivateKey` 可用于解密承诺的保密信息，而 `nullifierKey` 则可用于花费该承诺。因此，必须保证 `rootKey` 和 `mnemonic` 的安全存储。

用 `ZkpKeys` 来生成这些密钥的应用程序可以将 `rootKey` 存储在不同设备中，通过 Shamir Secret Sharing 将其分为几份。

我们还建议您将 `zkpPrivateKey` 和 `nullifierKey` 分开存储，以避免因其中之一遭攻破，而导致承诺失窃。

下图显示了在 Nightfall 中衍生出各种密钥的步骤
![](../imgs/key-derivation.png)
