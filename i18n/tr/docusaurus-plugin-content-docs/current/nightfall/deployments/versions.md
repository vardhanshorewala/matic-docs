---
id: versions
title: Geçmiş
sidebar_label: History of changes
description: "Devreye alınan sürümler"
keywords:
  - docs
  - polygon
  - nightfall
  - changelog
image: https://matic.network/banners/matic-network-16x9.png
---


## Beta 1.0 {#beta-1-0}
Beta 1.0, 17 Mayıs 2022'de kullanıma sunuldu. Bu sürüm Nightfall proof of concept'i (kavram kanıtı) devreye almak için temel mekanizmayı içeriyordu. Tek bir `Proposer` (teklifçi) ve işlemlerin ilk `coarse` (kabataslak) uygulamasını destekliyordu. Ayrıca bir kullanıcı cüzdanının
bir ön sürümünü sağlıyordu. Devreye alınan sürüm [burada](https://github.com/EYBlockchain/nightfall_3/commit/bc3e475de3e2877f14430f9599e5b38ea960765b) bulunabilir

## Beta 2.0 {#beta-2-0}
Devreye alınan sürüm [burada](https://github.com/EYBlockchain/nightfall_3/commit/4c2af01ac95af5ea6f5b40071d73a1624f06ba46) bulunabilir
Bu sürümde birkaç iyileştirme yapılmıştır:
- **Ücretlerin Toplanması**

Teklifçilere işlemler için ücretler toplama imkânı sağlanması. Bu özellik çoklu teklifçiyi teşvik edecektir.
- **Sorgulayıcı Devreye Alma**

Ağda şimdi teklifçinin bloklarını izleyen bir sorgulayıcı (challenger) yer alıyor.
- **Devreler (Circuits) İşlemleri**

İşlemlerin ZKP'si (sıfır bilgi kanıtı) üretilirken daha fazla esneklik ve daha iyi performans.  Hem `transfer` hem de `withdrawal` iki taneye kadar commitment kabul eder ve değişikliği döndürür.
Performans bakımından artık işlemler optimize edilmiştir, böylece kanıtlama daha kısa süre alır.

| Operasyonlar | Öncesindeki kısıtlamalar | Sonrasındaki kısıtlamalar |
|-----------|--------------------|------------------|
| Fon Yatırma | 84.766 | 1277 |
| Transfer | 499.119 | 67.694 |
| Fon çekme | 168.883 | 53.348 |

Optimizasyonun bir kısmı Poseidon'a geçilerek mümkün olmuştur

- **Gizli dizi şifreleme**

El-Gamal'dan [KEM-DEM](../protocol/secrets) şifreleme sürecine geçişimiz, aşağıdaki gibi birçok fayda sağladı:
- Şifreleme / şifre çözme işleminin basitleşmesi
- Kısıtlamalarda ve zincir içi gaz maliyetlerinde azalma.

- **Sorgulayıcının devreye alınması**

