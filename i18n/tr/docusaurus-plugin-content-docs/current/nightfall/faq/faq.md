---
id: faq
title: SSS
sidebar_label: FAQ
description: Nightfall hakkında sık sorulan sorular
keywords:
  - docs
  - polygon
  - nightfall
  - faq
image: https://matic.network/banners/matic-network-16x9.png
---

:::tip

Sorunuz bu listede yer almıyorsa lütfen sorunuzu <ins>**[Polygon Nightfall discord sunucusuna](https://discord.com/invite/pZkC3JV2bR)**</ins> gönderin.

:::

## Akıllı Sözleşmeleri nerede bulabilirim? {#where-can-i-find-the-smart-contracts}

Polygon Nightfall sözleşmeleri, [testnet Goerli](../deployments/testnet.md)'de ve [mainnet](../deployments/mainnet.md)'te devreye alınmıştır.

## Polygon Nightfall'un güvenlik denetiminde durum nedir? {#what-s-the-state-of-polygon-nightfall-s-security-audit}
Polygon Nightfall şu anda bir güvenlik denetiminden geçmektedir ve denetimin 3. çeyrek içinde tamamlanması planlanmaktadır. Bu arada, protokole birkaç kısıtlama eklenmiştir:

- Tek teklifçi çalışıyor, ve Polygon tarafından yönetiliyor
- [Kısıtlanmış fon yatırma ve fon çekme miktarları](../tools/nightfall-wallet.md#deposit-and-withdraw-restrictions)

## Nightfall Cüzdanımı nasıl kurabilirim? {#how-do-i-set-up-my-nightfall-wallet}
Polygon Nightfall cüzdanı kullanmaya nasıl başlayacağınıza dair tüm ayrıntıları içeren eksiksiz bir eğitim dokümanına [buradan](../tools/nightfall-wallet.md) ulaşabilirsiniz.

## Bir Ledger Donanım Cüzdanını Nightfall Cüzdan'a nasıl bağlayabilirim? {#how-do-i-connect-a-ledger-hardware-wallet-to-nightfall-wallet}
Cüzdan eğitim dokümanında, [bir Ledger Donanım Cüzdanının Metamask ile nasıl bağlanacağını](../tools/nightfall-wallet.md#how-to-connect-a-ledger-hardware-wallet-to-nightfall) açıklayan bir bölüm bulunmaktadır.

## Polygon Nightfall Ağında aktarımlar baştan sona ne kadar sürer? {#how-long-do-transfers-take-on-polygon-nightfall-network-from-start-to-finish}
Mevcut teklifçi kullanıcılardan işlemleri alır ve en çok 32 işlemden oluşan bloklar üretir. Bir blok oluşturmaya yetecek sayıda işlem toplanır toplanmaz işlem işlenecektir.

Ek olarak, blok üretme süresi üzerinde bir üst limit vardır, böylece her 6 saatte bir (teklifçinin topladığı işlemlerin sayısı ne olursa olsun) en az bir blok teklif edilir.

## Kimlerle işlem yapabilirim? {#who-can-i-transact-with}
Polygon Nightfall içinde varlıklar aktarmak için tek gereken hedef cüzdan adresidir, yani`Destination Wallet Address`. Fonlar almak için [Cüzdan Adresinizi nasıl paylaşacağınızı](../tools/nightfall-wallet.md#your-wallet-address) cüzdan eğitim dokümanından öğrenebilirsiniz.

## Commitment'lar nerede yedeklenir? {#where-are-commitments-backed-up}

Sıfır Bilgi kanıtları tarayıcıda hesaplanır, böylece gizli anahtarlarınız sizde kalır ve cüzdan, sahip olduğunuz commitment'ların takibini kendi IndexedDb'si içinde yapar. Bu verilere erişimi olan herkes sizin hangi commitment'lara sahip olduğunuzu öğrenebilir ama anahtarlarınız olmadan bunları çalamaz. Anahtarların şifresi yalnızca hatırlatıcıyı (mnemonic) girdiğinizde çözülür. Bu nedenle, cüzdanı yalnızca güvendiğiniz makinelerde kullanmanız gerekir.

Şimdilik bu veri herhangi bir yere dışa aktarılmıyor. Bu nedenle, farklı bir makinede tarayıcı kullanıyorsanız IndexedDB içeriklerini aktarmadığınız sürece commitment'larınıza erişemezsiniz. Commitment'ları cüzdan yoluyla dışa ve içe aktarmak için bir mekanizma sağlıyoruz.

## İşlemlerin gizliliği {#privacy-of-transactions}
Fon Yatırma ve Fon Çekme işlemlerinin mahrem olmadığını anlamanız önemli. Bunun nedeni bu işlemlerin Katman 1'le etkileşimde bulunmasıdır ve Katman 1 mahrem değildir. Bunun anlamı, herkes sizin bir Katman 2 commitment'ı oluşturup oluşturmadığınızı ve bu commitment'ın ne kadar içerdiğini bilir, demektir. Aynı şekilde, bir token'ı Katman 1'e bir Katman 2 commitment'ını imha ederek iade ederseniz herkes bunu kimin aldığını ve ne kadar olduğunu bilir.

Gizlilik tamamen Katman 2 içindeki aktarımlardan gelmektedir. Ethereum blok zinciri bakımından bunlar tamamen mahremdir. Sızdırılan tek veri, bir aktarma işlemini bir Blok Teklifçisine gönderdiğinizde IP adresinizdir. İlk Beta'da, Polygon sadece Teklifçileri çalıştırır.


## Fonlar nasıl çekilir? {#how-to-withdraw-funds}
Fonlar Polygon Nightfall cüzdanla çekilebilir. Çekişler, çekiş işlemini içeren bloğun üretildiği andan itibaren **bir haftalık** bir kesinleştirme (finalization) süresine tabidir. Bu süre dolduğunda, fonlarınızın Ethereum hesabınıza gönderilmesi için çekişi kesinleştirebilirsiniz.

## İşlemler Nightfall'da kaça mal olacak? {#how-much-will-transactions-cost-on-nightfall}
Farklı maliyetler taşıyan iki tür işlem vardır:

- Zincir içi işlemler: Bu işlemler akıllı sözleşmeye gönderilir ve mine edilmeleri için Ethereum üzerinde gaz ücretleri gerektirir. Bir teklifçi bu işlemi alıp bir blok içine koyabilir. Şu anda `deposit` ve `finalize withdrawal` zincir içi işlemlerdir.
- Zincir dışı işlemler: Bu işlemler doğrudan teklifçiye gönderilir. Şu anda tüm `transfer` ve `withdrawals` işlemleri zincir dışı işlemler olarak yapılandırılır.

## Nightfall Ağı üzerinde hangi token'ları kullanabilirim? {#which-tokens-can-i-use-on-nightfall-network}
Aşağıdaki token'lar Nightfall'da faaldir:

- MATIC
- WETH
- DAI
- USDC

## Nightfall'u kullanmak için MATIC token'lara ihtiyacım var mı? {#do-i-need-matic-tokens-to-use-nightfall}
Evet. `transfers` ve `withdrawals` işlemlerinin ücretini ödemek için Nightfall'a belli miktarda MATIC token'ları yatırmanız gerekecektir.

## Bir hata (bug) raporunu nereye gönderebilirim veya daha fazla yardım için Nightfall ile nasıl iletişime geçebilirim? {#where-can-i-submit-a-bug-report-or-contact-nightfall-for-additional-help}
Bunun en iyi yolu [Polygon Nightfall discord sunucumuza](https://discord.com/invite/pZkC3JV2bR) katılmak ve sorunuzu buraya göndermektir.
