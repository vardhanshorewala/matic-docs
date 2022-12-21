
# MPC 仪式 {#mpc-ceremony}
零知识证明要求具有受信任设置。这种设置会产生一种所谓的“有毒废物”，这可能会导致产生假证据。为了避免这种情况，需要举行一种仪式，通过多方计算 (MPC) 来生成该设置。

Nightfall 运行了一项多方计算 (MPC)，遵循与永续 Tau 计算仪式相同的原则。该流程从 BN254 椭圆曲线的永续 Tau 仪式 的第 72 个贡献开始。您可以在[此处](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response)找到这一贡献。

Nightfall 采用 Groth16 证明机制，因此每个回路都需要进行第二阶段的 MPC，由 4 个私有贡献构成：

1. [Darko Macesic (github ID：dark64）](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna (github ID: jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody（安永全球区块链负责人）](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor (github ID: iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

上一次贡献后，我们已将一个随机信标应用于这四个回路。我们为该信标建立了一项主网[交易](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1)，数据负载为 0xe095cb（用十进制来表示，即为 14718411）。

该交易被纳入编号为 [14711908](https://etherscan.io/block/14711908) 的区块，于 2022 年 5 月 5 日 +UTC 下午 05:00:27 上链，区块哈希为 `0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3`。
然后对该哈希进行 1024 次递归式哈希计算，结果为 `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`。

最后用下方的程序计算出最终哈希值：

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

有关第二阶段的完整信息请参见[此处](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md)。

