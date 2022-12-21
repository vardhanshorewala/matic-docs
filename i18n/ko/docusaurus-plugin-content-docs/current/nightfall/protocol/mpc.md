
# MPC 세리머니 {#mpc-ceremony}
영지식 증명에는 신뢰할 수 있는 설정이 필요합니다. 이러한 설정은 잠재적으로 허위 증명을 만들 수 있는 소위 '독성 폐기물'을 생성합니다. 이를 피하기 위해 다자간 계산(MPC)을 통해 이러한 설정을 생성하는 세리머니를 개최해야 합니다.

나이트폴은 Perpetual Powers of Tau Ceremony의 동일한 원칙을 따르는 다자간 계산(MPC)을 실행했습니다. 이 프로세스는 BN254 커브를 위한 Perpetual Powers of Tau Ceremony의 기여 72로 시작되었습니다. [여기](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response)에서 이 기여를 찾을 수 있습니다.

나이트폴은 Groth16 증명 방식을 사용하기 때문에 각 서킷을 위해 MPC의 두 번째 단계가 필요합니다. 이 2단계의 일부로 4건의 개인 기여가 있었습니다.

1. [Darko Macesic(github ID: dark64)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna(github ID: jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody(EY 글로벌 블록체인 리더)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor(github ID: iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

마지막 기여 후 당사는 4개 서킷을 위해 임의의 비콘을 적용했습니다. 이 비콘을 위해 당사는 데이터 페이로드 0xe095cb(십진수로 14718411)를 사용하여 Mainnet [트랜잭션](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1)을 생성했습니다.

이 트랜잭션은 2022년 5월 5일 05:00:27 PM(UTC 기준)에 생성된 블록 번호 [14711908](https://etherscan.io/block/14711908)에 포함되었으며
블록해시는
`0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3`입니다.
이후 이 해시는 재귀적으로 1024회 해싱되었습니다. 출력은 `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`입니다.

마지막 해시는 이 프로그램을 통해 계산되었습니다.

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

 2단계에 대한 자세한 정보는 [여기](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md)에서 찾을 수 있습니다.

