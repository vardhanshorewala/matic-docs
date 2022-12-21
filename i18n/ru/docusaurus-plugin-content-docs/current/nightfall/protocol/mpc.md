
# Церемония MPC {#mpc-ceremony}
Доказательства с нулевым разглашением требуют доверенной настройки. Эта настройка генерирует так называемые «токсичные отходы», которые могут потенциально допустить создание поддельных доказательств. Чтобы избежать этого, необходимо провести церемонию, в ходе которой эта настройка генерируется посредством многосторонних вычислений (MPC).

Nightfall запустил многосторонние вычисления (MPC), следуя тем же принципам, что и в церемонии Perpetual Powers of Tau. Процесс начался с вклада 72 из церемонии Perpetual Powers of Tau для кривой BN254. Вы можете ознакомиться с этим вкладом [здесь](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response).

Поскольку Nightfall использует схему доказательства Groth16, для каждой схемы необходим второй этап MPC. Четыре приватных вклада были частью этого второго этапа:

1. [Дарко Мацесич (Darko Macesic) (github ID: dark64)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Джорди Байлина (Jordi Bailyna) (github ID: jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Пол Броуди (Paul Brody) (лидер глобального блокчейна EY)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Майкл Коннор (Michael Connor) (github ID: iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

После последнего вклада мы применили случайный маяк для четырех схем. Для этого маяка мы создали [транзакцию](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1) в mainnet с пересылаемыми данными 0xe095cb (в десятичном виде это 14718411).

Эта транзакция была включена в блок номер [14711908](https://etherscan.io/block/14711908), который
достиг пункта назначения 5 мая 2022 года в 17:00:27 +UTC и имел blockhash
`0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3`.
Этот хэш затем был хэширован рекурсивно 1024 раза. Выходное значение: `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`.

Окончательный хэш был вычислен с помощью этой программы:

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

 Полная информация о втором этапе приводится [здесь](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md).

