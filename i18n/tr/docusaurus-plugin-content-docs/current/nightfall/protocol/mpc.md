
# MPC Seremoni {#mpc-ceremony}
Sıfır-bilgi kanıtları (ZKP) güvenilir bir kurulum gerektirir. Bu kurulum, sahte kanıtlar oluşturulmasına izin verme potansiyeli taşıyan bir "toksik atık" üretir. Bunu önlemek için, bu kurulumun çok-taraflı hesaplama (MPC) ile oluşturulduğu bir seremoni tertiplenmesi gerekir.

Nightfall, Perpetual Powers of Tau Ceremony ile aynı ilkelere uyan bir Çok-Taraflı Hesaplama (MPC) düzenledi. Süreç, BN254 Eğrisi için Perpetual Powers of Tau Ceremony'den gelen 72 no.lu katkı ile başladı. Bu katkıyı [burada](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response) görebilirsiniz.

Nightfall, Groth16 kanıtlama şemasını kullandığından, her bir devre için MPC'nin ikinci bir evresine ihtiyaç vardır. 4 özel katkı bu phase2 içinde yer aldı:

1. [Darko Macesic (github ID: dark64)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna (github ID: jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody (EY Global Blok Zincir Lideri)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor (github ID: iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

Son katkıdan sonra, 4 devre için rastgele bir beacon uyguladık. Bu beacon için, 0xe095cb payload'u ile bir mainnet [işlemi](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1) oluşturduk (ondalık sistemde bu 14718411'e karşılık gelir).

Bu işlem [14711908](https://etherscan.io/block/14711908) numaralı bloğa eklendi, bu blok
5 Mayıs 2022'de UTC ile saat 17:00:27'de yerleştirildi ve `0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3` blok hash'ini aldı
.
Bu hash daha sonra yinelemeli olarak 1024 kez hash edildi. Çıktı olarak `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09` alındı.

Nihai hash şu program ile hesaplandı:

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

 Faz 2 hakkında tüm bilgiler [burada](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md) bulunmaktadır.

