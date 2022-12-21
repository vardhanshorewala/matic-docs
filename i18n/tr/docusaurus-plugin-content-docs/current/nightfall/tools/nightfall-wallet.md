---
id: nightfall-wallet
title: Nightfall Cüzdan
sidebar: Nightfall Wallet
description: "Polygon Nightfall cüzdan kılavuzu."
keywords:
  - docs
  - matic
  - polygon
  - nightfall
  - wallet
image: https://matic.network/banners/matic-network-16x9.png

---

Polygon Nightfall cüzdan, Nightfall mainnet beta sürümüyle etkileşim kurabilen
bir web tarayıcı cüzdanıdır.

:::info Fon yatırma, aktarma ve çekme işlemleri yapmak için Nightfall cüzdanı kullanın

### Sınırlamalar {#restrictions}

Nightfall olgunluğa ulaşmış olmakla beraber aşağıdaki sınırlamalar uygulanır:


| ERC20 token | Yatırma Üst Limiti | Çekme Üst Limiti |
|-------------|-------------|--------------|
| MATIC | 250 MATIC | 1000 MATIC |
| WETH | 0.25 WETH | 1 WETH |
| DAI | 250 DAI | 1000 DAI |
| USDT | 250 USDT | 1000 USDT |
| USDC | 250 USDC | 1000 USDC |

:::

:::caution Güvenlik önlemleri

Nightfall cüzdan bir Chrome tarayıcıda test edilir. Beta sırasında sayaç diğer tarayıcılarda
değişik olabilir.

**Nightfall'u Chrome'da kullanmanızı özellikle tavsiye ederiz**.

:::



## Kullanmaya Başlama {#getting-started}

Polygon web [mainnet cüzdanı](https://wallet-beta.polygon.technology) veya
[testnet cüzdanı](https://wallet.testnet.polygon-nightfall.technology/) ziyaret edin, MetaMask hesabınızı
bağlayın ve soldaki Polygon Cüzdan'ı seçin. MetaMask için yardım gerekirse,
[MetaMask hakkında Polygon belgeleri](../../develop/metamask/tutorial-metamask.md)'ne bakın

![](../imgs/tools-wallet/polygon-wallet-click-nf.png)

Bu noktada cüzdan sizden Polygon Ağı'na Geçiş yapmanızı isteyecek ve bir Metamask açılır penceresi
geçişi onaylamanızı isteyecek.

![](../imgs/tools-wallet/polygon-network.png)

Ardından, cüzdanın üst kısmındaki Aşağı Açılır menüye tıklayın ve `Polygon Nightfall`'u seçin; bundan sonra
Ethereum Mainnet'e geçiş için yeni bir istek görünecektir. Polygon Nightfall ile çalışmak için
Ethereum Mainnet'e geçişi kabul edin.

![](../imgs/tools-wallet/polygon-network-dropdown-nf.png)

Test ağında çalışıyorsanız, cüzdan URL'si sizi doğrudan Polygon Nightfall cüzdanının açılış sayfasına götürecektir.

![](../imgs/tools-wallet/wallet-main-screen.png)

İlk ziyaretinizde Nightfall cüzdanın oluşturulması gerekecek. Bir hatırlatıcı (mnemonic) üretmeniz ve cüzdanı oluşturmanız için bir açılır pencere görünür. `Generate Mnemonic`'e tıklayın, ardından `Create Wallet`'a tıklayın. **Bu cüzdanı yalnızca şu anda kullandığınız cihazda kullanabileceğinizi aklınızda bulundurun**.

![](../imgs/tools-wallet/generate-mnemonic-create-wallet.png)

:::caution Commitment'larınızı ve hatırlatıcılarınızı yedekleyin

Cüzdan anahtarlarınız ve işlemleriniz tarayıcıda (IndexedDb) depolanır. Nightfall Cüzdan'a ilk girdiğinizde belirlediğiniz hatırlatıcı da öyle.

Bu hatırlatıcıyı güvenli bir yerde sakladığınızdan emin olun. L2'deki fonlarınızla uyumlu kanıtlar üretmenin tek yolu budur. Aynı şey commitment'larınız için de geçerlidir: başka bir tarayıcı veya makine kullandığınızda `export commitments`'a basarak bunları güvenli bir şekilde sakladığınızdan emin olun.

:::

**Commitment'larınızı kaybederseniz fonlarınızı sonsuza kadar kaybedersiniz**


Bu noktada hem Metamask hem de Nightfall cüzdan adreslerinizi (sağ üstte) görüyor olmanız gerekir.

**İşlem yapmaya başlamadan önce cüzdan kurulumunun tamamlanması için birkaç dakika daha bekleyin**.

Cüzdanın sol alt köşesinde cüzdan durumu `Syncing Nightfall` olarak gösterilir. Cüzdan bu durumdayken işlemler yapmak için gerekli
ZK devrelerini ve ağ durumunu getirmektedir.

![](../imgs/tools-wallet/wallet-state-syncing.png)

Cüzdan durumu `Nightfall Synced` olarak değişene kadar bekleyin

![](../imgs/tools-wallet/wallet-state-synced.png)


## Bir Ledger Donanım Cüzdanı Nightfall'a nasıl bağlanır {#how-to-connect-a-ledger-hardware-wallet-to-nightfall}
Resmî Metamask sitesindeki Ledger Donanım Cüzdanını Metamask'le bağlama kılavuzunu [burada](https://support.ledger.com/hc/en-us/articles/4404366864657-How-to-access-your-Ledger-Ethereum-ETH-account-via-Metamask?docs=true) bulabilirsiniz.

Cüzdanınızda Ethereum App'i bağladığınızdan ve Ethereum App ayarlarında "blind signing" (kör imzalama) ögesini etkinleştirdiğinizden emin olun.


### Cüzdan adresiniz {#your-wallet-address}
Nightfall cüzdan adresinizi Nightfall Assets sayfasından `Receive`'e tıklayarak getirin.

![](../imgs/tools-wallet/nightfall-wallet-address.png)

## Fon yatırma nasıl yapılır {#how-to-make-deposits}
Nightfall Assets sayfasından, seçilen varlığın sağ tarafındaki `Deposit` düğmesine tıklayın veya L2 Bridge sayfasına gidin.

1. Transfer modunun `Deposit` olarak ayarlandığını kontrol edin
2. İstenen token'ın (WETH, MATIC vb) seçildiğini kontrol edin
3. Nightfall cüzdanınıza yatıracağınız değeri girin, `Transfer`'a tıklayın
4. Açılır pencerede işlemi gözden geçirin
5. `Create Transaction`'a tıklayın

![](../imgs/tools-wallet/deposit-click-transfer.png)

ZKP'yi hesaplayan ve işlemi hazırlayan bir süreç başlayacaktır - Metamask'e hesap bakiyelerinize erişim izni verin. Bu sona erdiğinde, `Send Transaction`'a tıklayın - sözleşme etkileşimi için Metamask'e ek izinleri verin.

![](../imgs/tools-wallet/deposit-tx-created-and-ready-to-be-sent.png)

[Yatırımınızı görüntülemek](#view-transactions) için Transactions sayfasına gidin.

### Fon yatırmalar hakkında önemli bilgi {#important-information-about-deposits}
- [Yatırma miktarları Beta sırasında sınırlandırılır](#note-the-following-deposit-and-withdrawal-restrictions)

## Aktarmalar nasıl yapılır {#how-to-make-transfers}
Nightfall Assets sayfasından, seçilen varlığın sağ tarafındaki `Send` düğmesine tıklayın.

1. Polygon Nightfall L2'de mevcut olan geçerli bir adres girin
2. İstenen token'ın (WETH, MATIC vb) seçildiğini kontrol edin
3. Nightfall cüzdanınızdan aktarılacak miktarı girin, `Continue`'a tıklayın

![](../imgs/tools-wallet/send-nf.png)

ZKP'yi hesaplamak ve işlemi hazırlamak için bir süreç başlayacaktır. Bu sona erdiğinde, `Send Transaction`'a tıklayın.

[Aktarımınızı görüntülemek](#view-transactions) için Transactions sayfasına gidin.

### Aktarmalar hakkında önemli bilgi {#important-information-about-transfers}
Nightfall'de şu anda kullanılan ZKP aktarma devreleri aktarma miktarlarını mevcut bir commitment'dan veya mevcut iki commitment'ın doğrusal bir kombinasyonundan
birinin değeriyle tam olarak eşleşen miktarla sınırlar.

Aktarma sınırlamalarını bir örnek üzerinde görmek için aşağıdaki commitment kümelerine bakın:

- A Kümesi: [1, 1, 1, 1, 1, 1]
- B Kümesi: [2, 2, 2]
- C Kümesi: [2, 4]

Bu üç kümenin hepsinin toplam tutarları 6 birime eşit olmakla beraber, yalnızca aşağıdaki aktarmalar yapılabilir:

- A Kümesi: 0 ile 2 arasında bir aktarma (her ikisi hariç)
- B Kümesi: 0 ile 4 arasında bir aktarma (her ikisi hariç)
- C Kümesi: 0 ile 6 arasında bir aktarma (her ikisi hariç)

Bu örnekle devam edersek, eğer Alex C Kümesi commitment'lara sahipse, kullanılabilir aktarmalar 0 ile 6 arasındaki bir miktarı içerir, her iki limit değeri hariç tutar. Eğer Alex Bob'a 3,5 birim aktarmak isterse, blok teklif edildikten sonra Alex'te 2,5 birimlik tek bir commitment kalacak ve Bob 3,5 birimlik bir commitment alacaktır.

Diğer yandan, eğer Alex Bob'a 6 birimlik bir miktar aktarmak isterse, ZK kanıtı başarısız olacaktır çünkü commitment'ların geçerli bir kombinasyonu olmayacaktır.

**Bu değerlerin sahip olunan commitment'ları temsil ettiğini**, örneğin yatırmaları temsil etmediğini akılda tutmak önemli. Daha fazla bilgiyi bu belgelerin [commitment'lar](../protocol/commitments.md) bölümünde bulabilirsiniz.

## Fon çekişleri nasıl yapılır {#how-to-make-withdrawals}
Nightfall Assets sayfasından, seçilen varlığın sağ tarafındaki `Withdraw` düğmesine tıklayın veya L2 Bridge sayfasına gidin.

1. Transfer modunun `Withdraw` olarak ayarlandığını kontrol edin
2. İstenen token'ın (WETH, MATIC vb) seçildiğini kontrol edin
3. Nightfall cüzdandan çekeceğiniz miktarı girin, `Transfer`'a tıklayın
4. Açılır pencerede işlemi gözden geçirin
5. `Create Transaction`'a tıklayın

ZKP'yi hesaplamak ve işlemi hazırlamak için bir süreç başlayacaktır. Bu sona erdiğinde, `Send Transaction`'a tıklayın.

[Çekişinizi görüntülemek](#view-transactions) için Transactions sayfasına gidin. Bir haftalık kesinleştirme süresi dolduktan sonra, kullanıcı,
çekiş miktarını kesinleştirerek talep edebilir.

### Çekişler hakkında önemli bilgi {#important-information-about-withdrawals}
- Çekiş değeri sahip olunan commitment'lardan biriyle tam olarak eşleşmelidir (daha fazla bilgi için [commitment'lar](#learn-about-commitments) belgesine bakın)
- Çekişler, çekiş işlemini içeren bloğun üretildiği andan itibaren **bir haftalık** bir kesinleştirme süresine tabidir. Bu süre dolduğunda, fonlarınızın Ethereum hesabınıza gönderilmesi için çekim işlemini kesinleştirebilirsiniz.
- Beta sırasında [çekiş miktarları sınırlanır](#note-the-following-deposit-and-withdrawal-restrictions)
- Çekişler bir zincir içi işlemdir ve işlem isteği sırasında ve ayrıca çekiş kesinleştirildiğinde gaz ücretleri ödenir.

![](../imgs/tools-wallet/cooling-off-vs-ready.png)

## İşlemleri görüntüleyin {#view-transactions}
Fon yatırma, aktarma ve çekme işlemlerinizin durumunu Transactions sayfasında kontrol edin. Her bir işlemin bir blok üretmeye yetecek sayıda işlem mevcut olur olmaz ya da 6 saat sonra işleneceğini aklınızda bulundurun.

![](../imgs/tools-wallet/transactions.png)
