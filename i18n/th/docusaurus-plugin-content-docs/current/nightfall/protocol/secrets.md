---
id: secrets
title: ในการกระจายความลับของแบนด์
sidebar_label: In Band Secret Distribution
description: "โซลูชันในการเข้ารหัสความลับและรับรองการถอดรหัสลับ"
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

## ภาพรวม {#overview}

เพื่อให้แน่ใจว่าผู้รับได้รับข้อมูลลับที่จำเป็นในการใช้จ่ายตามข้อผูกมัด ผู้ส่งจะเข้ารหัสความลับ  (*salt*, *value*, *tokenId*, *ercAddress*) ของข้อผูกมัดที่ส่งไปยังผู้รับ และพิสูจน์โดยใช้ ZKP ว่าพวกเขาเข้ารหัสอย่างถูกต้องด้วยกุญแจสาธารณะของผู้รับใช้กระบวนทัศน์การเข้ารหัสแบบไฮบริดของ [**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf)

## การเข้ารหัสแบบไฮบริด KEM-DEM {#kem-dem-hybrid-encryption}


### การสร้างคีย์ {#key-creation}

`p`ใช้การเข้ารหัสแบบโค้งรูปไข่ (ในที่นี้เราใช้การเข้ารหัสแบบเส้นโค้ง Baby Jubjub) `E`บนสนามจำกัด`Fp`ซึ่งเป็นจำนวนเฉพาะขนาดใหญ่และ`G`เป็นตัวเจเนอร์เรเตอร์

อลิซสร้างคู่คีย์แบบอสมมาตรชั่วคราวแบบสุ่ม  :$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

คีย์เหล่านี้ใช้เพียงครั้งเดียวและเฉพาะสำหรับธุรกรรมนี้ทำให้เราเก็บความลับในการส่งต่อที่สมบูรณ์แบบ

### การเข้ารหัส {#encryption}

กระบวนการเข้ารหัสประกอบด้วย 2 ขั้นตอน: ขั้นตอน KEM เพื่อรับคีย์การเข้ารหัสแบบสมมาตรจากความลับที่ใช้ร่วมกัน และขั้นตอน DEM เพื่อเข้ารหัสข้อความธรรมดาโดยใช้คีย์เข้ารหัส

### วิธีการห่อหุ้มคีย์ (การเข้ารหัส) {#key-encapsulation-method-encryption}
ด้วยการใช้คีย์ส่วนตัวแบบอสมมาตรที่สร้างไว้ก่อนหน้านี้ เราได้รับความลับที่ใช้ร่วมกัน $key_{DH}$โดยใช้มาตรฐาน Diffie-Hellmanซึ่งจะถูกแฮชควบคู่ไปกับคีย์สาธารณะชั่วคราวเพื่อรับคีย์การเข้ารหัส

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


ซึ่ง    เป็นกุญแจสาธารณะของผู้รับ  $Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### วิธีการห่อหุ้มข้อมูล (การเข้ารหัส) {#data-encapsulation-method-encryption}
เพื่อประสิทธิภาพของวงจร การเข้ารหัสที่ใช้คือรหัสบล็อกในโหมดตัวนับโดยที่อัลกอริธึมการเข้ารหัสคือแฮช mimcเนื่องจากคีย์ชั่วคราวจะไม่ซ้ำกันสำหรับแต่ละธุรกรรม จึงไม่จำเป็นต้องรวม nonceการเข้ารหัสของ$i^{th}$ข้อความมีดังนี้:

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

โดยที่    $Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

ผู้ส่งจึงให้ผู้รับด้วย$(Q_e, \text{ciphertexts})$สิ่งเหล่านี้รวมอยู่ในโครงสร้างธุรกรรมที่ส่งบนห่วงโซ่

### การถอดรหัส {#decryption}
ในการถอดรหัส ผู้รับจะดำเนินการตามขั้นตอน KEM-DEM เวอร์ชันที่แก้ไขเล็กน้อย

### วิธีการห่อหุ้มคีย์ (ถอดรหัส) {#key-encapsulation-method-decryption}
ถ้าให้$Q_e$ ผู้รับสามารถคำนวณคีย์การเข้ารหัสภายในเครื่องได้โดยทำตามขั้นตอนต่อไปนี้

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

ซึ่ง    เป็นกุญแจสาธารณะชั่วคราว  $Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### วิธีการห่อหุ้มข้อมูล (ถอดรหัส) {#data-encapsulation-method-decryption}
ด้วย$key_{enc}$ and an array of ciphertexts, the $i_{th}$ข้อความธรรมดาสามารถกู้คืนได้ดังต่อไปนี้:

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

โดยที่    $Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## การได้มาและการสร้างคีย์ต่างๆ ที่เกี่ยวข้องกับการเข้ารหัส การเป็นเจ้าของข้อผูกมัดและการใช้จ่าย {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

ใช้ BIP39 สร้างคำ 12 คำ`mnemonic`และจากนี้สร้าง`seed`โดยการโทร`mnemonicToSeedSync`จากนั้นปฏิบัติตามมาตรฐานของ BIP32 และ BIP44 ให้สร้าง`rootKey`ตาม`seed`และ`path`

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

หากไม่ว่า`rootKey`หรือ`mnemonic`ถูกประนีประนอม จากนั้น ฝ่ายตรงข้ามสามารถคำนวณ`zkpPrivateKey`และ`nullifierKey`ได้`zkpPrivateKey`สามารถใช้เพื่อถอดรหัสความลับของข้อผูกมัด ในขณะที่`nullifierKey`สามารถใช้เพื่อทำตามข้อผูกมัดได้ดังนั้น `rootKey`และ`mnemonic`จะต้องถูกจัดเก็บอย่างปลอดภัยมากๆ

แอปที่จะใช้`ZkpKeys`ในการสร้างคีย์เหล่านี้สามารถจัดเก็บ`rootKey`ในอุปกรณ์ต่าง ๆ โดยแยกแบ่งออกเป็นการแชร์โดยใช้ Shamir Secret Sharing

ขอแนะนำให้จัดเก็บ`zkpPrivateKey`และ`nullifierKey`แยกไว้ต่างหากเพื่อหลีกเลี่ยงการโจรกรรมข้อผูกมัดในกรณีที่มีข้อผูกมัดข้อใดข้อหนึ่ง

รูปด้านล่างแสดงขั้นตอนในการรับคีย์ต่างๆ ใน Nightfall![](../imgs/key-derivation.png)
