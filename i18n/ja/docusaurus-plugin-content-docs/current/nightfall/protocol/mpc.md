
# MPCセレモニー {#mpc-ceremony}
ゼロナレッジのプルーフには、信頼できるセットアップが必要です。この設定により、いわゆる「有毒廃棄物」が生成され、偽のプルーフを作成する可能性があります。これを回避するには、このセットアップがマルチパーティ計算（MPC）によって生成される式典を開催する必要があります。

Nightfallは、Tauセレモニーの永続的な権限の同じ原則に従って、マルチパーティ計算（MPC）を実行しました。このプロセスは、Tauセレモニーの永続的な権限によるBN254曲線への貢献72から始まりました。この貢献は[こちら](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response)でご覧いただけます。

NightfallはGroth16証明方式を使用するため、回線ごとにMPCの第2フェーズが必要です。 4つのプライベート貢献は、このフェーズ2の一部でした：

1. [Darko Macesic（githubID：dark64）](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna（githubID：jbaylina）](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody（EYグロブロックチェーンリーダー）](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor（githubID：iAmMichaelConnor）](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

前回の貢献後、4回線にランダムビーコンを適用しました。このビーコンに対して、データペイロード0xe095cb（10進数では14718411）とのメインネット[トランザクション](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1)を作成しました。

このトランザクションは、2022年5月5日05:00:27PM+UTCに上陸し、ブロックハッシュが発生したブロック番号[14711908](https://etherscan.io/block/14711908)に含まれていました
`0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3`。
その後、このハッシュは1024回繰り返しハッシュされました。出力は、`0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`です。

最終的なハッシュは、次のプログラムを使用して計算されました：

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

フェーズ2の詳細情報については、[ここ](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md)を参照してください。

