---
id: overview
title: Genel Bakış
sidebar_label: Overview
description: Nightfall'a genel bir bakış
keywords:
  - docs
  - polygon
  - nightfall
  - privacy
  - rollup
  - zk
image: https://matic.network/banners/matic-network-16x9.png
---

Polygon yakın gelecekte birçok şirketin birbirleriyle iş mantığının yürütülmesi ve mal ve
hizmet alışverişinin yönetilmesi için akıllı sözleşmeler yoluyla etkileşimde bulunacaklarını gören bir vizyona inanıyor.

Polygon, [Ernst & Young](https://blockchain.ey.com/) ile iş birliği yaparak, Ethereum kullanmak isteyen şirketler için erişilebilirliği ve mahremiyeti mümkün kılacak Polygon Nightfall adlı herkese açık (public), mahremiyet odaklı bir Katman 2 rollup
çözümü sunuyor.

## İşletmeler için Sıfır Bilgi Kanıtı (ZK-Proof) Protokolü {#a-zk-proof-protocol-for-enterprises}

Polygon Nightfall, Polygon'un ölçeklenebilirlik çözümleri paketinin bir parçasıdır. Bu pakette şunlar da yer alır:
[Polygon Hermez](https://polygon.technology/solutions/polygon-hermez/),
[Polygon Miden](https://polygon.technology/solutions/polygon-miden/)
ve [Polygon Zero](https://polygon.technology/solutions/polygon-zero/).
Anahtar fark, Nightfall'ın mahrem ve ölçeklenebilir işlemler sunmak için optimistik rollup'lar ve Sıfır Bilgi (ZK) kriptografisi kavramlarını birleştirerek kurumsal kullanım senaryoları
için tasarlanmış mahremiyet odaklı bir rollup olmasıdır.

Nightfall bir yandan ölçeklenebilirliği mümkün kılarken, diğer yandan şirketlerin bugün blok zinciri kullanırken karşılaştıkları büyük bir bariyeri
kaldırmayı hedefliyor: işlemlerin mahremiyetinin olmaması. Nightfall bir mahremiyet katmanı ekliyor, böylece anahtar işlem parametreleri (örneğin değer ve hedef adres) geriye doğru izlenemiyor. Bu iki özellik, Nightfall'u iş mantıklarını yürütmenin ve tedarik zincirleriyle merkeziyetsiz bir ağda ve sürdürülebilir bir fiyatla koordine olmanın, üstelik bütün bunları güvenliği ve mahremiyeti koruyarak yapmanın bir yolu olarak gören özel işletmelerin ilgisini çekmektedir.

## Nightfall'un Sütunları {#nightfall-s-pillars}

Polygon Nightfall'un ana değer önermesi, verilerin merkeziyetsiz bir ağda güvenli, mahrem ve düşük maliyetli aktarımlarını
mümkün kılmaktır.

![](../imgs/overview.png)

## Mahremiyet {#privacy}

Polygon Nightfall mahrem işlemler göndermek için ZK kanıtları kullanır. Kullanıcı işlemin bir ZK kanıtını
işlemin hedef adresi veya değeri gibi anahtar işlem parametrelerini belirtmeksizin
üretebilir. Nightfall'un mahremiyet bileşeni hakkında daha fazla bilgi
[protokol](../protocol/protocol.md) kılavuzunda bulunabilir.

## Güvenlik {#security}

> Nightfall şu anda bir güvenlik denetiminden geçiyor; bu denetimin 2022 Haziran ortalarında tamamlanması bekleniyor. Denetim süreci tamamlandıktan sonra sonuçlar burada yayınlanacaktır.

> Bir bootstrap dönemine tabi yeni bir ağ olarak, Nightfall sistemi korumak için geçici
> güvenlik önlemleri uygulamakta olup, bu önlemleri kaldırmayı ve sistemi tamamen merkeziyetsiz bırakmayı hedeflemektedir.

Polygon Nightfall bir Katman 2 yapısıdır çünkü sağlam bir genel blok zinciri olan Ethereum'un güvenliğini ödünç alarak
Ethereum'u kaldıraç olarak kullanır. Nightfall, varlıkların kurtarılmasını garanti eden belirli varsayımlara dayanır. Bu varsayımlar,
hash'ler ve imzalar gibi belirli kriptografik primitiflerin kullanıldığı ZK-SNARKS etrafında
şekillenen çeşitli tasarım ve mimari kararlarına dayanmaktadır.
Son olarak Nightfall farklı akıllı sözleşmelere işleticilerin kullanıcı işlemlerini bloke etmemelerini ve kullanıcıların varlıklarını diledikleri zaman çekebilmelerini garanti edecek
işletim kuralları gömer.

Özet olarak Nightfall aşağıdaki güvenlik varsayımlarında bulunur:

1. Ethereum'un güvenlik varsayımları.
2. Groth16 varsayımları (exponent bilgisi varsayımı).
3. Hash'ler (Poseidon) ve imzalar gibi primitiflerden gelen bazı kriptografik varsayımlar.
4. Doğru tasarım ve uygulamaya dayanan yazılım güvenliği varsayımları.

## Verimlilik {#efficiency}

Blok teklifçileri çeşitli kullanıcılardan gelen işlemleri toplar ve bunları bir L2 Bloğunda birleştirir (batch).
Tipik L2 bloğu boyutları yaklaşık 32 işlem içerir.

Bir yatırma, aktarma ve çekme işleminin beklenen gaz maliyetleri 9000, 1200 ve 9500'dür. Bu maliyet işlem başına 574Byte'lık çağrı verisinin depolanmasından ve ayrıca bir L2
bloğunu işlemek için gerekli sabit çağrı verisinden ve bilgisayar hesaplamasından kaynaklanır. Maliyetler
[EIP 4488](https://eips.ethereum.org/EIPS/eip-4488) sonrasında %80'e kadar daha düşük olacaktır.

## İnkâr Edilemez Aktarmalar {#non-deniable-transfers}

Nightfall, aktarma işleminin ZK kanıtının bir parçası olarak, aktarılan commitment'ı
işlemek için gizli bilgilerin (token adresi, değer, kimlik ve salt) şifrelenmesini içerir. Bu, kullanıcıyı gizli bilgileri alıcının bildiği
bir anahtarla şifrelemeye zorlar. Bu anahtar ZK kanıtının bir parçası olduğundan, alıcı inandırıcı inkâr edebilirliğe
güvenir çünkü gönderici doğru şifre anahtarının kullanıldığını kanıtlayabilir.

## Merkeziyetsizlik {#decentralization}

Doğrulayıcılar ve [Sorgulayıcılar](docs/nightfall/protocol/actors) Nightfall'un ayrılmaz bir parçasıdır. Bunlar, işlemlerin
ve L2 bloklarının zamanında ve doğru şekilde üretilmesini sağlarlar. Hisse kanıtına (PoS) dayalı bir konsensüs mekanizması
kullanılarak ağın bir sonraki [Teklifçisi](docs/nightfall/protocol/actors) seçilir. Diğer yandan, Sorgulayıcılar doğru olmayan bir blok
tespit edildiğinde sorgulamalar göndererek ve Teklifçinin yaptığı stake'i alıkoyarak
ağın doğru çalışmasını sağlar.


## Gelecek Kanıtı {#future-proof}
Nightfall'un Optimistik rollup uygulamasının sağladığı esneklik sayesinde, işlemleri ZK'de uygulayan yeni bir devre tipi tanımlayıp kaydetmek suretiyle mevcut işlemleri
tehlikeye düşürmeden gelecekte yeni işlemler eklemek
mümkündür.

## Referanslar {#references}

1. [ZK Ölçeklemesine Çok Taraflı Bir Yaklaşım](https://messari.io/article/polygon-a-multi-sided-approach-to-zk-scaling)
2. [Paul Brody'nin Nightfall hakkındaki düşünceleri](https://www.linkedin.com/pulse/say-hello-nightfall-paul-brody-1f/)
