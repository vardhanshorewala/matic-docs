---
id: secrets
title:
sidebar_label: In Band Secret Distribution
description: ""
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

## Resumen {#overview}



##  {#kem-dem-hybrid-encryption}


###  {#key-creation}







###  {#encryption}



###  {#key-encapsulation-method-encryption}


$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$





###  {#data-encapsulation-method-encryption}


$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$





###  {#decryption}


###  {#key-encapsulation-method-decryption}


$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$



###  {#data-encapsulation-method-decryption}


$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$




##  {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}



```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```








