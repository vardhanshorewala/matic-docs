---
id: circuits
title: Devreler ve İşlemler
sidebar_label: Circuits and Transactions
description: "Nightfall'daki Devre Türleri"
keywords:
  - docs
  - polygon
  - nightfall
  - circuits
  - deposit
  - transfer
image: https://matic.network/banners/matic-network-16x9.png
---

Devreler, bir işlemin doğru olarak değerlendirilmesi için uyması gereken kuralları tanımlamakta kullanılır. Temel olarak her işlem türü için bir tane olmak üzere üç tür devre vardır:

- [Fon Yatırma](#deposit)
- [Aktarma](#transfer)
- [Fon Çekme](#withdraw)

Her işlem, bu devrelerde belirtilen kısıtlamalara uyan bir ZK Kanıtı içerir. Kullanıcılar bu kanıtı bir Cüzdan kullanarak
veya bir İstemci sunucusu üzerinden oluştururlar.
Bir kanıt yalnızca aşağıdaki tüm durumlar doğruysa oluşturulur:

- Yeni [commitment](./commitments#what-are-commitments) geçerlidir
- Eski [commitment](./commitments#what-are-commitments) geçerlidir ve göndericiye aittir
- [Nullifier] (./commitments#what-are-nullifiers) geçerlidir
- Merkle Ağacı yolu/kökü geçerlidir
- Commitment'ı içeren şifreli metin geçerlidir


## Fon Yatırma {#deposit}
Fon yatırma işlemleri herkesçe görülebilen ERC token'larını, orijinal token ile aynı değer veya token kimliğini
ve öngörülen commitment sahibinin Nightfall genel anahtarını taşıyan bir token commintment'ına çevirir.

Bir Fon Yatırma ZK Kanıtı, kanıtlayanın geçerli bir commitment $Z_A$ with a public key $pk_A$ ögesi oluşturduğunu kanıtlar.

Devre daha sonra $Z_A$ == H(@ | ɑ | $pk_A$ | σ) olduğunu kontrol eder
Bir fon yatırma işleminde sızdırılan bilgiler arasında yeni commitment'ı mint eden adres ve kullanılan ERC token'ının adresi ve değeri yer alır.

![](../imgs/deposit.png)

## Aktarma {#transfer}
Aktarmalar, aynı varlığın en çok iki commitment'ının iletimini, önceki commitment'ları sıfırlayarak (nullify) ve en çok iki yeni commitment oluşturarak mümkün kılar:
- Aktarılan miktarın değerini içeren bir commitment alıcıya gönderilir
- Diğer commitment değişikliğin değeriyle (yani kullanılan commitment'ların değerlerin toplamı ile aktarılan değer arasındaki fark) oluşturulur ve göndericiye ait olur.

Bir Aktarma ZK Kanıtı, kanıtlayanın Merkle Ağacında bulunan en çok iki eski commitment'ı sıfırladığını, yeni commitment'ları oluşturduğunu ve bunun bilgilerini alıcı için şifrelediğini kanıtlar.

Her iki durumda da, sızdırılan bilgi, bir Ethereum adresinin göndericinin sahip olduğu commitment havuzundaki
commitment'ları sıfırladığı ve yeni commitment'lar oluşturulduğu olacaktır.
Commitment'ları harcanan ya da miktarı aktarılan yeni sahip hakkındaki bilgiler mahrem kalır.

İlk şemada mevcut bir commitment'ı (veya commitment'ları) sıfırlama ve `transaction` veri yapısına bilgiyi ekleme adımları gösterilmiştir.

![](../imgs/transfer_a.png)

İkinci şemada, yeni oluşturulan commitment'ın üretilmesi ve şifrelenmesi için gereken adımlar gösterilmiştir.

![](../imgs/transfer_b.png)

## Fon Çekme {#withdraw}
Fon çekme, mevcut bir Nightfall commitment'ını sıfırlama ve onu yakılan commitment ile aynı değer ve token kimliğine (token Id) sahip, herkes tarafından görülebilen ERC token'larına çevirme işlemidir. Fon Çekme, Fon Yatırma işleminin tersidir. Aktarmalara benzer şekilde, fon çekme işlemlerinde en fazla iki commitment girdi olarak kabul edilir.

Bir Fon Çekme ZK Kanıtı, kanıtlayanın, Merkle Ağacında bulunan en fazla iki eski commitment'ı sıfırladığını kanıtlar.

Fon çekme sırasında sızdırılan bilgiler arasında, commitment'ı çeken adres ve çekilen tokenin değeri/token kimliği ve adresi yer alır.

![](../imgs/withdraw.png)

### Cooling-off dönemi {#cooling-off-period}

Fon çekme işlemlerinde, işlemi kesinleştirmek için bir haftalık `COOLING OFF` döneminin geçmesi gerekir. Bunun sebebi Nightfall'un iyimser (optimistic) yapısıdır çünkü bir sorgulayıcı bir sahtekârlık kanıtı gönderene kadar tüm yeni blokların doğru olduğu varsayılır. Fonlar bir haftalık dönem geçene kadar tutulur ve L1'e çekilebilir.

# Ücretler {#fees}

Teklifçi gelen işlemleri alır ve bunları bir ücret karşılığında bir L2 bloğu içinde toplar.  İşleme bağlı olarak Teklifçiye ödenen iki farklı ücret türü vardır:
- Fon yatırmalarda ücretler ETH cinsinden doğrudan L1'de ödenir.
- Fon Aktarmalar ve Çekişlerde ücretler MATIC cinsinden L2'de ödenir.
