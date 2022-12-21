---
id: secrets
title: Bant İçi Sır Dağıtımı
sidebar_label: In Band Secret Distribution
description: "Sırların şifrelenmesi ve şifrelerinin çözülmesi için bir çözüm."
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

## Genel Bakış {#overview}

Bir alıcının commitment'larını harcamak için gerekli olan gizli bilgileri almasını sağlamak için, gönderici
alıcıya gönderilen commitment'ın gizli bilgilerini (*salt*, *değer*, *token kimliği*, *ercAddress*) şifreler ve
ZKP kullanarak, bunu, alıcının genel anahtarı ile doğru bir şekilde şifrelediğini kanıtlar. [**KEM-DEM**](https://eprint.iacr.org/2006/265.pdf) hibrit şifreleme paradigması kullanılır.

## KEM-DEM Hibrit Şifreleme {#kem-dem-hybrid-encryption}


### Anahtar Oluşturma {#key-creation}

Eliptik eğri (burada Baby Jubjub eğrisi kullanıyoruz) `E`'yi bir sonlu alan `Fp` üzerinde kullanıyoruz; burada `p` büyük bir
asal sayı ve `G` üreteçtir.

Alice rasgele bir geçici asimetrik anahtar çifti    üretir :
$x_e \; \leftarrow\; \{0, 1\}^{256} \qquad Q_e \coloneqq x_eG$

Bu anahtarlar yalnızca bir kez kullanılır ve sadece bu işleme özeldir; bu da bize mükemmel bir ileri yönde gizlilik sağlar.

### Şifreleme {#encryption}

Şifreleme süreci 2 adımdan oluşur: paylaşılan bir gizli bilgiden simetrik bir şifreleme anahtarı elde edilen bir KEM adımı ve şifreleme anahtarı kullanılarak düz metinlerin şifrelendiği bir DEM adımı.

### Anahtar Kapsülleme Yöntemi (Şifreleme) {#key-encapsulation-method-encryption}
Daha önce üretilen asimetrik özel anahtarı kullanarak, standart Diffie-Hellman yoluyla paylaşılan bir gizli bilgi $key_{DH}$'yi elde ederiz. Bu, geçici genel anahtarla birlikte hash edilerek şifreleme anahtarı elde edilir.

$key_{DH} \coloneqq x_eQ_r \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$


burada  
   alıcının genel anahtarıdır  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$


### Veri Kapsülleme Yöntemi (Şifreleme) {#data-encapsulation-method-encryption}
Devre verimliliği için kullanılan şifreleme şifre algoritmasının bir mimc hash olduğu sayaç modunda bir blok şifredir. Geçici anahtarlar her işlem için benzersiz olduğundan, bir nonce dâhil edilmesine gerek yoktur. $i^{th}$ mesajının şifrelemesi aşağıdaki gibidir:

$c_i \coloneqq H_{D}(key_{enc} + i) + p_i$

burada  

$Domain_{D} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-dem'}))$

Gönderici daha sonra alıcıya $(Q_e, \text{ciphertexts})$'i verir. Bunlar zincir içi gönderilen işlem struct'ının bir parçası olarak dâhil edilirler.

### Şifre çözme {#decryption}
Şifre çözmek için alıcı KEM-DEM adımlarının biraz değiştirilmiş bir versiyonunu icra eder.

### Anahtar Kapsülleme Yöntemi (Şifre Çözme) {#key-encapsulation-method-decryption}
$Q_e$ verildiğinde, alıcı aşağıdaki adımları icra ederek şifreleme anahtarını yerel olarak hesaplayabilir.

$$key_{DH} \coloneqq x_eQ_e \qquad key_{enc} \coloneqq H_{K}(key_{DH} \; + \;Q_e)$$

burada  
   geçici genel anahtardır  

$Domain_{K} \coloneqq \text{to\_field}(\text{SHA256}(\text{'nightfall-kem'}))$

### Veri Kapsülleme Yöntemi (Şifre Çözme) {#data-encapsulation-method-decryption}
$key_{enc}$ and an array of ciphertexts, the $i_{th}$ yardımıyla düz metin aşağıdaki formülle geri getirilebilir:

$$p_i \coloneqq c_i - H_{D}(key_{enc} + i)$$

burada  

$Domain_{D} \coloneqq \text{to\_field}(SHA256(\text{'nightfall-dem'}))$


## Şifrelemede kullanılan çeşitli anahtarların türetilmesi ve üretilmesi, commitment'ların sahipliği ve harcama {#derivation-and-generation-of-the-various-keys-involved-in-encryption-ownership-of-commitments-and-spending}

BIP39 kullanarak 12 sözcükten oluşan bir `mnemonic` üretin ve bundan `mnemonicToSeedSync` komutunu çağırarak bir `seed` üretin.
Sonra BIP32 ve BIP44 standartlarını takip ederek bu `seed` ve `path`'e dayalı olarak bir `rootKey` üretin.

```
zkpPrivateKey = mimc(rootKey, 2708019456231621178814538244712057499818649907582893776052749473028258908910)
where 2708019456231621178814538244712057499818649907582893776052749473028258908910 is keccak256(`zkpPrivateKey`) % BN128_GROUP_ORDER

nullifierKey = mimc(rootKey, 7805187439118198468809896822299973897593108379494079213870562208229492109015n)
where 7805187439118198468809896822299973897593108379494079213870562208229492109015n is keccak256(`nullifierKey`) % BN128_GROUP_ORDER

zkpPublicKey = zkpPrivateKey * G
```

`rootKey` veya `mnemonic` tehlikeye düşerse, saldırgan `zkpPrivateKey` ve `nullifierKey`'yi hesaplayabilir.
`zkpPrivateKey` kullanılarak bir commitment'ın gizli bilgileri deşifre edilebilir ve `nullifierKey` kullanılarak commitment harcanabilir.
Dolayısıyla `rootKey` ve `mnemonic` çok güvenli bir şekilde saklanmalıdır.

Bu anahtarları üretmek için `ZkpKeys`'i kullanacak uygulamalar `rootKey`'i Shamir's Secret Sharing kullanarak parçalara bölerek
bunu farklı cihazlarda saklayabilir.

`zkpPrivateKey` ve `nullifierKey`'in de birbirinden ayrı saklanması tavsiye edilir, böylece ikisinden birinin tehlikeye düşmesi durumunda commitment'ların çalınması
önlenmiş olur.

Aşağıdaki şekilde Nightfall'da farklı anahtarları türetme adımları gösterilmektedir
![](../imgs/key-derivation.png)
