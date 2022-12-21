---
id: contracts
title: Akıllı Sözleşmeler
sidebar_label: Smart Contracts
description: "Shield, teklifçiler, sorgulamalar ve Merkle Ağacı Hesaplamaları."
keywords:
  - docs
  - polygon
  - nightfall
  - smart
  - contracts
  - shield
image: https://matic.network/banners/matic-network-16x9.png
---

Sözleşmeler, ağ içinde işlem yapmak isteyen her Nightfall aktörünün uyması gereken kuralları tanımlar.
Akıllı Sözleşmeler şunları içerir:

- [Shield.sol](#shield)
- [Proposers.sol](#proposers)
- [Challenges.sol](#challenges)
- [MerkleTree_Computations.sol](#merkletree_computations)

## Shield {#shield}
Bu sözleşme, bir kullanıcının, bir Teklifçi tarafından işlenecek bir işlem göndermesine olanak sağlar. Bu bir fon yatırma İşlemi ise, ödeme alır.
Ayrıca, herkesin Shield sözleşmesinin (commitment kökü ve nullifier listeleri) durumunun güncellenmesini talep etmesine izin verir.
Durum güncellendiğinde, güncellemedeki fon çekmeler işlenir.

Blok zincirine bir aktarma veya fon çekme işlemi göndermeye temelde bir ihtiyaç yoktur: sadece teklifçilerin işlemleri alması
ve bunları bir Katman 2 Bloğuna eklemesi için bir mesaj panosu görevi görür.

Nightfall gerçek ERC sözleşmeleri ile etkileşimde bulunduğundan, aşağıdaki kontroller gizli olarak yapılamaz:

- **Fon Yatırma/Çekme** sırasında ERC token adresi geçerli olmalıdır.
- **Fon yatırma** sırasında, kullanıcı, commitment oluşturacak bakiye veya tokenlere sahip olmalıdır.

## Teklifçiler {#proposers}
Sözleşme; teklifçileri kaydetme, kayıtlarını silme, ödeme yapma ve rotasyona tabi tutma ve blok zincirine yeni bir Katman 2 Bloğu teklif etme fonksiyonlarını içerir.
Nightfall'un ilk versiyonunda yalnızca Polygon tarafından işletilen tek bir Boot Teklifçi edilmektedir. Gelecek versiyonlarda bu kısıtlama kaldırılacak ve birden çok teklifçiye izin verilecektir.

## Sorgulamalar {#challenges}
İşlevsellik, bir Bloğun doğru olup olmadığının sorgulanmasına olanak sağlar.

## MerkleTree_Stateless {#merkletree_stateless}
Orijinal `MerkleTree.sol`'ın durumsuz (saf fonksiyon) versiyonudur; `Challenges.sol` tarafından zincir içinde blok sorgulamalarının hesaplanmasında kullanılır.

## Diğer sözleşmeler {#other-contracts}
- `Utils.sol` - çeşitli sözleşmelerde kullanılan veya inline olarak (içerilmiş) bırakılırsa kodun okunabilirliğini etkileyecek işlevleri bir araya getirir.
- `Config.sol` - bir Node.js yapılandırma dosyasına benzer şekilde, içinde sabitler tutulur.
- `Structures.sol` - global structları, enumları, olayları, eşlemeleri ve durum değişkenlerini tanımlar. Bunların bulunmasını kolaylaştırır.

## Upgrade edilebilirlik {#upgradability}
Polygon, en azından başlangıçta, devreye alma sonrasında Nightfall sözleşmelerini upgrade etme imkanına sahiptir.
Bunu yapmak için Truffle için Openzeppelin [Upgrade Plugin](https://docs.openzeppelin.com/upgrades-plugins/1.x/)'lerini kullanıyoruz.

Polygon, sözleşmeleri upgrade etmek için bir [deployer](https://github.com/EYBlockchain/nightfall_3/tree/master/nightfall-deployer) modülü kullanır.
`deployer` modülünün migration klasöründe depolanmış 4 migration vardır.
İlk üç migration, Polygon Nightfall sözleşme paketinin 'normal' şekilde devreye alınmasını gerçekleştirir. Bununla birlikte
bu migrationlar, daha sonraki bir tarihte upgrade edilmelerini sağlamak için tüm sözleşmelerin (kütüphanelerin değil) bir proxy ile
devreye alınmasını sağlarlar. Dördüncü migration, sözleşmeleri upgrade etmek için kullanılır.
