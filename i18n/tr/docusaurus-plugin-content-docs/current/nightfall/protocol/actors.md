---
id: actors
title: Aktörler
sidebar_label: Actors
description: "Nightfall'da Aktör Türleri"
keywords:
  - docs
  - polygon
  - nightfall
  - transactor
  - proposer
  - challenger
  - liquidity
  - provider
image: https://matic.network/banners/matic-network-16x9.png
---

Ağda rol oynayan dört aktör vardır:

- [İşlemciler](#transactor)
- [Teklifçiler](#proposer)
- [Sorgulayıcılar](#challenger)

## İşlemci {#transactor}
Bir işlemci hizmetin düzenli müşterisidir. İşlemciler mahremiyet altında Yatırma, Aktarma ve Çekme işlemleri yapmak isterler.
Bu müşteriler işlemleri üretmek için gerekli ZK Kanıtlarını oluşturmak üzere tipik olarak web cüzdanı veya dedike bir sunucu (İstemci) kullanacaklardır.

## Teklifçi {#proposer}
Bir Teklifçi müşterilerden gelen işlemleri toplar ve Shield sözleşmesinin durumuna
yeni güncellemeler teklif eder.
Durum derken, spesifik olarak bir ZKP İşlemiyle ilişkili depolama değişkenlerini, yani
 nullifier'ları ve commitment köklerini kastediyoruz.
Güncelleme teklifleri bir Katman 2 Bloğuna roll up edilen (yani toplanan) birkaç işlem içerir. Bloktaki tüm işlemler işlendikten sonra oluşacak son durumun yalnızca bir hash'i
zincirde depolanır.
. İşlemler 1 haftalık bir süreden sonra kesinleşir.

Herkes Teklifçi olabilir ama bir miktar stake göndermeleri gerekir. Stake iyi davranışı teşvik etme amacı güder.
Teklifçiler doğru Bloklar sağlayarak, işlemcilerden ücretler toplayarak para kazanır. Teklifçiler geleneksel bir blok zincirindeki Madencilere benzetilebilir.


## Sorgulayıcı {#challenger}
Bir Sorgulayıcı teklif edilen blokların doğruluğunu, bloğun gönderilmesinden sonra bir hafta içinde inceler. Herkes Sorgulayıcı olabilir.
Sorgulayıcılar, bloklarını oluştururken teklifçiler tarafından gönderilen stake'i, başarıyla bir sorgulama gönderdiklerinde alırlar.


## Notlar {#notes}
Polygon’un referans uygulamasında, hem Teklifçi hem de Sorgulayıcı bazı işlevleri Optimist adı verilen ortak bir modüle devrederler.
Bu Optimist modülü çeşitli Teklifçi ve Sorgulayıcılara blokların üretilmesi ve sorgulanması
(Teklifçi ve Sorgulayıcıların bu işlemleri imzalamaları gerekecektir), blok zinciri olaylarıyla senkronize etme vb. gibi birtakım hizmetler sağlar.

Yukarıda açıklanan Aktörler dışında, İstemci adı verilen bir aktör daha vardır. Bir İstemci, kullanıcı işlemlerini toplayan, ZK Kanıtlarını kullanıcılar adına oluşturan, işlemleri Teklifçiye gönderen, Blok Zinciri olaylarını dinleyen vb. bir güvenli hizmet olarak çalışır. Kısaca söylersek, İstemci ağır kanıt hesaplama işini devretmek isteyen ve birbirine güvenen bir kullanıcılar grubu için güvenilir bir üstlenici olarak iş görür.

İstemcinin alternatifi, Polygon tarafından sağlanan bir sunucusuz hizmet olan web tarayıcı cüzdanını kullanmaktır. Bu cüzdan tüm işlem faaliyetlerini tek bir kullanıcı için mahremiyeti koruyarak yönetir.
