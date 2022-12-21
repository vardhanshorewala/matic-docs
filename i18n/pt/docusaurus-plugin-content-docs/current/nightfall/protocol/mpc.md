
# Cerimónia MPC {#mpc-ceremony}
As provas de conhecimento zero exigem uma configuração confiável. Esta configuração gera um chamado “lixo tóxico”, que poderia potencialmente permitir criar provas falsas. Para evitar isto, é necessário realizar uma cerimónia onde esta configuração seja gerada através de computação multipartidária (MPC).

O Nightfall executou uma Computação de Várias Partes (MPC) seguindo os mesmos princípios de Perpetual Powers of Tau Ceremony. O processo começou com a contribuição 72 de Perpetual Powers of Tau Ceremony para a Curva BN254. Pode encontrar esta contribuição [aqui](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response).

Como o Nightfall usa o esquema de comprovação Groth16, é necessária uma segunda fase da MPC para cada circuito. 4 contribuições privadas fizeram parte desta fase2:

1. [Darko Macesic (ID github: dark64)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna (ID github: jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody (Líder Global de Blockchain da EY)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor (ID github: iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

Após a última contribuição, aplicamos um beacon aleatório para os 4 circuitos. Para este beacon, criamos uma [transação](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1) mainnet com o payload de dados 0xe095cb (em decimal isto é 14718411).

Esta transação foi incluída no bloco número [14711908](https://etherscan.io/block/14711908), que entrou a 5 de maio de 2022 às 05:00:27 +UTC e teve o blockhash`0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3` .
Este hash foi então utilizado recursivamente 1024 vezes. O resultado é `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`.

O hash final foi calculado com este programa:

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

As informações completas sobre a fase 2 podem ser encontradas [aqui](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md).

