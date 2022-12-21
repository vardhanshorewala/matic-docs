---
id: secrets
title: Phân phối bí mật In Band
sidebar_label: In Band Secret Distribution
description: "Một giải pháp để mã hóa các bí mật và đảm bảo quá trình giải mã."
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

## Tổng quan {#overview}

Để đảm bảo người nhận sẽ nhận được thông tin bí mật cần thiết để sử dụng cam kết, người gửi mã hóa các bí mật (*salt*, *giá trị*, *tokenId*, *ercAddress*) của cam kết được gửi đến người nhận và chứng minh bằng cách sử dụng ZKP mà họ đã mã hóa theo cách phù hợp với khóa công khai của người nhận. Mẫu mã hóa kết hợp [**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf) được sử dụng.

## Mã hóa kết hợp KEM-DEM {#kem-dem-hybrid-encryption}


### Tạo khóa {#key-creation}

Dùng đường cong Elliptic (ở đây chúng tôi sử dụng đường cong Baby Jubjub) `E`trên một trường hữu hạn `Fp`khi `p`là một số nguyên tố lớn và `G`là trình tạo.

Alice tạo ra một cặp khóa bất đối xứng ngắn hạn ngẫu nhiên   :
$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

Các khóa này chỉ được sử dụng một lần và là duy nhất cho giao dịch này, là cách thức hoàn hảo để giữ bí mật.

### Mã hóa {#encryption}

Quy trình mã hóa bao gồm 2 bước: một bước KEM để lấy khóa mã hóa đối xứng từ bí mật được chia sẻ và một bước DM để mã hóa các văn bản thuần túy bằng khóa mã hóa.

### Phương pháp đóng kín khóa (Mã hóa) {#key-encapsulation-method-encryption}
Bằng cách sử dụng khóa riêng tư bất đối xứng được tạo trước đó, chúng ta có được một bí mật chung, $key_{DH}$, sử dụng Diffie-Hellman tiêu chuẩn. Nó sẽ được băm, bên cạnh khóa công khai ngắn hạn để có được khóa mã hóa.

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


trong đó  
   là khóa công khai của người nhận  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### Phương pháp đóng kín dữ liệu (Mã hóa) {#data-encapsulation-method-encryption}
Để đạt hiệu quả của mạch, mã hóa được sử dụng là một mật mã khối ở chế độ bộ đếm khi thuật toán mật mã là một hàm băm mimc. Do khóa ngắn hạn là duy nhất với từng giao dịch, không cần đưa vào một nonce nữa. Mã hóa của thông báo $i^{th}$ cụ thể như sau:

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

trong đó  

$Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

Người gửi sau đó sẽ cung cấp $(Q_e, \text{ciphertexts})$ cho người nhận. Những mục này là một phần của cấu trúc giao dịch được gửi trên chuỗi.

### Giải mã {#decryption}
Để giải mã, người nhận thực hiện phiên bản gồm các bước KEM-DM với một chút thay đổi.

### Phương pháp đóng kín khóa (Giải mã) {#key-encapsulation-method-decryption}
Với $Q_e$ đã cho, người nhận có thể tính toán khóa mã hóa cục bộ bằng cách thực hiện các bước sau.

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

trong đó  
   là khóa công khai ngắn hạn  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### Phương pháp đóng kín dữ liệu (Giải mã) {#data-encapsulation-method-decryption}
Với $key_{enc}$ and an array of ciphertexts, the $i_{th}$, có thể khôi phục văn bản thuần túy như sau:

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

trong đó  

$Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## Nguồn gốc và quá trình tạo các khóa khác nhau liên quan đến mã hóa, sở hữu cam kết và chi tiêu {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

Sử dụng BIP39 tạo 12 từ `mnemonic` và từ này tạo ra một `seed` bằng cách gọi `mnemonicToSeedSync`. Sau đó, tuân theo các tiêu chuẩn BIP32 và BIP44, tạo một `rootKey` dựa trên `seed`và `path` này.

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

Nếu `rootKey`hoặc `mnemonic`bị xâm phạm, đối thủ có thể tính toán `zkpPrivateKey`và `nullifierKey`. Có thể sử dụng `zkpPrivateKey`để giải mã bí mật của cam kết, đồng thời sử dụng `nullifierKey`để chi tiêu cam kết. Do đó `rootKey`và `mnemonic` phải được lưu trữ rất an toàn.

Các ứng dụng dùng `ZkpKeys`để tạo khóa này có thể lưu trữ `rootKey` trong các thiết bị khác nhau bằng cách phân chia thành các phần nhờ Shamir Secret Sharing.

Bạn cũng nên lưu trữ `zkpPrivateKey` và `nullifierKey` riêng biệt để tránh bị trộm cam kết trong trường hợp một trong số đó bị xâm phạm.

Hình bên dưới minh họa các bước để lấy các khóa khác nhau trong Nightfall![](../imgs/key-derivation.png)
