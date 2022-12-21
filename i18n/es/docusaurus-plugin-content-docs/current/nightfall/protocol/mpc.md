
# Ceremonia de MPC {#mpc-ceremony}
Las pruebas de conocimiento cero requieren una configuración confiable. Esta configuración genera un llamado "residuo tóxico" que podría permitir potencialmente crear pruebas falsas. Para evitar esto, se necesita realizar una ceremonia donde esta configuración se genere a través de un cómputo multipartido (MPC).

Nightfall ejecutó un cómputo multipartido (MPC) siguiendo los mismos principios de los Poderes Perpetuos de la ceremonia de Tau. El proceso comenzó con la contribución 72 de  Poderes Perpetuos de la ceremonia de Tau para la curva BN254. Puedes encontrar esta contribución [aquí](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response).

Ya que nightfall utiliza el esquema de prueba Groth16, se necesita una segunda fase del MPC, para cada circuito. Cuatro contribuciones privadas fueron parte de esta fase2:

1. [Darko Macesic (github Id. dark64)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna (github Id. jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody (Líder de cadena de bloques de EY Global)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor (github Id. iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

Después de la última contribución, aplicamos una señal aleatoria para los 4 circuitos. Para esta señal creamos una [transacción](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1) mainnet con la carga de datos 0xe095cb (en decimal esto es 14718411).

Esta transacción se incluyó en el bloque número [14711908](https://etherscan.io/block/14711908), que
aterrizó el 5 de mayo de 2022 a las 05:00:27 PM +UTC y tuvo el blockhash
`0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3`.
Este hash después fue hash recursivamente 1024 veces. La salida es `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`.

El hash final se calculó con este programa:

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

La información completa sobre la fase 2 se puede encontrar [aquí](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md).

