---
id: protocol
title: Nightfall Protocol
sidebar_label: Nightfall Protocol
description: "Nightfall Süreci."
keywords:
  - docs
  - polygon
  - nightfall
  - protocol
  - chain
  - block
  - structure
  - layer
image: https://matic.network/banners/matic-network-16x9.png
---

En az 1 Teklifçinin sisteme kaydolduğunu ve asgari bir Stake gönderdiğini varsayıyoruz.

## İşlem gönderme {#transaction-posting}
Yeni işlemler göndermek için iki mekanizma vardır:

- [Zincir içi](#on-chain)
- [Zincir dışı](#off-chain)

### Zincir içi {#on-chain}
Süreç bir İşlemcinin `Shield.sol` dosyasında `submitTransaction` komutunu çağırarak bir işlem oluşturmasıyla başlar. İşlemci bu İşlem için Shield sözleşmesine bir ücret öder, ki İşlemcinin karar verdiği herhangi bir şey olabilir. Bu, İşlemi bir Bloğa dâhil eden Teklifçiye ödenir. Mevcut durumda, teklifçi ve altta yatan Optimist oturumu bir bloğa dâhil etmek için muhtemelen daha yüksek ücretleri seçecektir, tıpkı bir madencinin yapacağı gibi.
İşlem çağrısı, işlem bilgilerini içeren bir blok zinciri olayının gönderilmesine sebep olur. Bu işlem bir Fon Yatırma işlemiyse, Shield sözleşmesi söz konusu Katman 1 ERC token ödemesini alır.

### Zincir dışı {#off-chain}
Aktarma ve Fon Çekme işlemlerinde, işlemin yukarıdaki süreç yoluyla zincir içi gönderilmesi yerine doğrudan dinleyen teklifçilere gönderilmesi seçeneği vardır.
Bu zincir dışı işlemler İşlemcileri bir fon yatırma işleminin zincir içi gönderilmesi maliyetinden (yaklaşık 45k gaz) kurtarır ama işlemciler ve bağlanmayı seçtikleri teklifçiler arasında daha yüksek derecede bir güven gerektirirler. Kötü niyetli teklifçilerin zincir dışı alınan işlemleri sansürlemeleri zincir içi işlemleri sansürlemelerinden daha kolaydır, çünkü bu işlemler dinleyen tüm teklifçilere yayınlanmaz. Bu durumda işlemciler bir işlemi ancak cooling-off dönemi (1 hafta) geçtikten sonra güvenilebilir saymalıdır.

## İşlem kabulü {#transaction-acceptance}
Teklifçiler işlemler aldıklarında o işlemin iyi yapılandırıldığını ve kanıtın public input hash'e karşı doğrulandığını doğrulamak için bir dizi kontroller icra ederler.
Tüm kontrollerden geçen işlem bir Bloğa alınmak üzere Teklifçinin bellek havuzuna eklenir.

## Blok birleştirme ve gönderme {#block-assembly-and-submission}
Teklifçiler Shield sözleşmesinin kendilerini geçerli teklifçi olarak atayana kadar bekler.
Geçerli Teklifçi kendi dâhili Optimist oturumundan işlemleri içeren yeni bir bloğu kendi bellek havuzundan alır. Her işlem için, bu işlemlerin Shield sözleşmesine eklenmeleri halinde oluşacak yeni commitment Merkle Ağacını hesaplayacaktır.

Dolayısıyla Blok, Blok içinde yer alan İşlemlerin hash'lerini ve Blok içindeki tüm işlemler işlendikten sonra oluşacak commitment Merkle Ağacı kökünü (Commitment Kökü) içerir. Daha sonra Teklifçi bu bloğu Durum akıllı sözleşmesine gönderir.

Bir blok teklif edildiğinde aşağıdaki bilgiler zincir içinde kaydedilir:

- Blok veri yapısı
```
  struct Block {
    uint48 leafCount; // note this is defined to be the number of leaves BEFORE the commitments in this block are added
    address proposer;
    bytes32 root; // the 'output' commitment root after adding all commitments
    uint256 blockNumberL2;
    bytes32 previousBlockHash;
    bytes32 transactionHashesRoot;
  }
```
- Blok içindeki işlemler
```
    struct Transaction {
        uint112 value;
        uint112 fee;
        TransactionTypes transactionType;
        TokenType tokenType;
        uint64[2] historicRootBlockNumberL2; // number of L2 block containing historic root
        uint64[2] historicRootBlockNumberL2Fee; //number of L2 block containing historic root fee
        bytes32 tokenId;
        bytes32 ercAddress;
        bytes32 recipientAddress;
        bytes32[2] commitments;
        bytes32[2] nullifiers;
        bytes32[1] commitmentFee;
        bytes32[2] nullifiersFee;
        bytes32[2] compressedSecrets;
        uint256[4] proof;
    }
```

## Sorgulamalar {#challenges}
Bloklar, bir hafta boyunca kuyrukta sorgulanabilir olarak kalır; bu süre zarfında doğrulukları sorgulama fonksiyonlarından biri çağrılarak sorgulanabilir. Yapılabilecek sorgulamalar şunlardır:

- **INVALID_PROOF** - bir işlemde verilen kanıtın doğruluğunun onaylanmaması;
- **INVALID_PUBLIC_INPUT_HASH** - bir işlemin public input hash'inin public input'larının doğru hash'i olmaması;
- **HISTORIC_ROOT_EXISTS** - işlem kanıtını oluşturmada kullanılan commitment Merkle  Ağacı kökünün hiç var olmaması;
- **DUPLICATE_NULLIFIER** - bir İşlemin parçası olarak verilen bir nullifier'ın harcanmış nullifier'lar listesinde olması;
- **HISTORIC_ROOT_INVALID** - Blok içindeki işlemlerin işlenmesiyle ortaya çıkan güncellenmiş commitment kökünün doğru olmaması;
- **DUPLICATE_TRANSACTION** - bu blokta yer alan bir işlemin birebir aynısı bir işlemin önceki bloklardan birine eklenmiş olması;
- **TRANSACTION_TYPE_INVALID** - işlem türüne (ör. Fon Yatırma, Aktarma, Çekme) göre işlemin iyi yapılandırılmış olmaması.

Sorgulama başarılı olursa, yani zincir içi hesaplama bunun geçerli bir sorgulama olduğunu gösterirse aşağıdaki eylemler gerçekleştirilir:

- Söz konusu Bloğun ve takip eden tüm Blokların hash'leri kuyruktan kaldırılır.
- Teklifçi tarafından gönderilen Blok stake'i Sorgulayıcıya ödenir.
- Blok içinde işlemi olan İşlemcilere, Teklifçilere ödemiş oldukları ücret ve bir Fon Yatırma durumunda Shield sözleşmesi tarafından alıkonulan tüm emanet fonlar iade edilir.

