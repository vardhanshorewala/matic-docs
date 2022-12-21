---
id: secrets
title: インバンドシークレット配信
sidebar_label: In Band Secret Distribution
description: "秘密を暗号化し、その復号化を確実にするソリューション。"
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

## 概要 {#overview}

受信者がコミットメントを消費するために必要な秘密情報を確実に受信するために、送信者は受信者に送信されたコミットメントの秘密（*塩*、*値*、*トークンID*、*ercアドレス*）を暗号化し、受信者のパブリック鍵でこれを正しく暗号化したことをZKPを使用して証明します。[**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf)ハイブリッド暗号化パラダイムが使用されます。

## KEM-DEMハイブリッド暗号化 {#kem-dem-hybrid-encryption}


### 鍵作成 {#key-creation}

`p`大きな素数と発電`Fp`機である有限フィールド`E`上で楕円曲線（ここではBaby Jubjub`G`曲線を使用）を使用します。

Aliceはランダムな一時的な非対称キーペアを生成します  ：
$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

これらの鍵は1回だけ使用され、このトランザクション固有のものであり、完全な転送秘密を提供します。

### 暗号化 {#encryption}

暗号化プロセスには、共有秘密から対称暗号鍵を取得するKEMステップと、暗号鍵を使用してプレーンテキストを暗号化するDEMステップの2つのステップが含まれます。

### 鍵カプセルメソッド（暗号化） {#key-encapsulation-method-encryption}
以前に生成された非対称秘密鍵を使用して、標準のDiffie-Hellmanを使用して共有秘密$key_{DH}$を取得します。これは、暗号鍵を取得するために、一時的なパブリック鍵とともにハッシュされます。

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


場所  
  受信者のパブリック鍵  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### データカプセルメソッド（暗号化） {#data-encapsulation-method-encryption}
回路効率のために、使用される暗号化は、暗号アルゴリズムがmimcハッシュであるカウンタモードのブロック暗号です。エフェメラルキーが各トランザクションに固有である場合、ナンスを含める必要はありません。$i^{th}$メッセージの暗号化は次のとおりです：

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

場所  

$Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

次に、送信者は受信者に$(Q_e, \text{ciphertexts})$を提供します。これらは、オンチェーンで送信されるトランザクション構造の一部として含まれます。

### 復号 {#decryption}
復号化するために、受信者はKEM-DEMステップのわずかに変更されたバージョンを実行します。

### 鍵カプセルメソッド（復号） {#key-encapsulation-method-decryption}
$Q_e$を指定すると、受信者は次の手順を実行することにより、暗号鍵をローカルで計算できます。

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

場所  
  一時的なパブリック鍵  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### データカプセルメソッド（復号） {#data-encapsulation-method-decryption}
$key_{enc}$ and an array of ciphertexts, the $i_{th}$プレーンテキストは次のとおりで回復できます：

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

場所  

$Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## 暗号化、コミットメントの所有権、および支出に関連するさまざまな鍵の導出と生成 {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

BIP39を使用して12ワード`mnemonic`を生成し、これから`mnemonicToSeedSync`をコールして`seed`を生成します。
次に、BIP32およびBIP44の標準に従って、この`seed`および`path`に基づいて`rootKey`を生成します。

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

`rootKey`または`mnemonic`のいずれかが危険にさらされた場合、相手は`zkpPrivateKey`と`nullifierKey`を計算できます。
`zkpPrivateKey`はコミットメントの秘密を復号化するために使用できますが、`nullifierKey`はコミットメントを使用するために使用できます。
したがって、`rootKey`と`mnemonic`は非常に安全に保管する必要があります。

これらのキーを生成するために`ZkpKeys`を使用するアプリケーションはShamir秘密共有を使用してBを共有に分割することによって、`rootKey`Bを異なるデバイスに保存することができます。

また、`zkpPrivateKey`と`nullifierKey`を別々に保管し、これらのいずれかが侵害された場合のコミットメントの盗難を避けることを推奨します。

次の図は、Nightfallでさまざまなキーを取得する手順を示しています
![](../imgs/key-derivation.png)
