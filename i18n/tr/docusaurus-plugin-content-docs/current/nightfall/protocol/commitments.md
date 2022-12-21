---
id: commitments
title: Commitment'lar ve Nullifier'lar
sidebar_label: Commitment and Nullifiers
description: "Tek ve çift aktarma."
keywords:
  - docs
  - polygon
  - nightfall
  - commitment
  - nullifier
image: https://matic.network/banners/matic-network-16x9.png
---


## Commitment'lar nedir?  {#what-are-commitments}
Bir commitment, bir kullanıcının seçilen bir değeri işlemesine (commit) ve bunu diğerlerinden gizli tutmasına,
işlenen değeri daha sonra açıklamasına izin veren bir kriptografik primitiftir.
Değerin ve alıcının gizliliği bu şekilde sağlanır.

Bir kullanıcının Nightfall'u kullanarak gerçekleştirdiği her işlemde, tarayıcı cüzdanı bir Sıfır Bilgi Kanıtı (ZKP)
hesaplar ve bir commitment oluşturur (veya nullify eder, yani sıfırlar).
Örneğin, fon yatırma veya aktarma işlemi yaptığınızda bir commitment oluşturursunuz ve fon aktarma veya çekme yaptığınızda
bir commitment'ı nullify edersiniz, yani sıfırlarsınız.

ZKP hesaplamasının temel aldığı [devreler](../protocol/circuits.md), bir işlemin doğru olması için uyması gereken
kuralları tanımlar.

Commitment aşağıdaki property'leri gizlemek için kullanılır:
- **Token'ın ERC adresi**
- **Token kimliği**
- **Değer**
- **Sahibi**

Commitment'lar bir *Merkle Ağacı* yapısında saklanır. Bu *Merkle Ağacının*'nin kökü, zincir içinde tutulur.

![](../imgs/commitment.png)

### UTXO {#utxo}
Fon yatırma ve aktarma işlemleri sırasında commitment'lar oluşturulur ve fon aktarma ve çekme işlemleri sırasında commitment'lar harcanır. **Commitment'lar birbiriyle toplanmaz**. Bir commitment harcanırken, harcanan commitment'ın değeri, sahip olunan en fazla iki commitment'ın değeri ile sınırlıdır.

Nightfall'da şu anda kullanılan ZKP fon aktarma ve çekme devreleri, ödemeler hariç 2 giriş - 2 çıkış (aktarma/çekme commitment'ı ve değişikliği) ile sınırlıdır.
Bir işlemcinin commitment'lar kümesi, çoğunlukla düşük değerde commitment'lar (dust) içeriyorsa, gelecekte aktarma yapmakta zorlanabilir.

Aşağıdaki değer kümelerini inceleyin

- **A Kümesi**: [1, 1, 1, 1, 1, 1]
- **B Kümesi**: [2, 2, 2]
- **C Kümesi**: [2, 4]

Bu üç kümenin hepsinin toplam tutarları eşit olsa da, *A*, *B* ve *C* kümeleri tarafından işlenebilecek maksimum değer aktarımı sırasıyla 2, 4 ve 6'dır. Bu, büyük commitment değerlerinin tercih edilme nedenlerinden biridir. Kullanılan commitment seçme stratejisi, düşük değerde commitment'ların kullanımına öncelik verilmesi riskini azaltırken, aynı zamanda dust commitment'ların oluşturulmasını en aza indirir.


## Nullifier'lar nedir? {#what-are-nullifiers}
Bir **Nullifier**, bir commitment ve nullifier anahtarı kombinasyonunun sonucudur. Nullifier zincir içinde yayınlandıktan sonra, commitment harcanmış kabul edilir.
Nullifier'lar blok teklifi sırasında çağrı verilerinin bir parçası olarak zincir içinde depolanır.

![](../imgs/nullifier.png)



