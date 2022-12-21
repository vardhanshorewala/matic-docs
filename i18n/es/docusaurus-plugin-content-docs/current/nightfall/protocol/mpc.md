
# Ceremonia de MPC {#mpc-ceremony}
Las pruebas de conocimiento cero requieren una configuración de confianza. Esta configuración genera algo llamado "desperdicio tóxico" que podría permitir potencialmente crear pruebas falsas. Para evitar esto, se debe celebrar una ceremonia donde esta configuración es generada mediante la computación de múltiples partes (MPC).

Nightfall ejecutó una computación de múltiples partes (MPC) siguiendo los mismos principios de las Potencias Perpetuas de la Ceremonia Tau. El proceso comenzó con la contribución 72 de Potencias Perpetuas de la Ceremonia Tau para la curva BN254. Puedes encontrar esta contribución [aquí](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response).

Dado que Nightfall utiliza el esquema de prueba de Groth16, se necesita una segunda fase del MPC para cada circuito. De 4 contribuciones privadas que formaron parte de esta fase2:

1. [Darko Macesic (github ID: dark64)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna (github ID: jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody (Líder global de cadena de bloques de EY)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor (github ID: iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

Después de la última contribución, aplicamos unas balizas aleatorias para los 4 circuitos. Para esta baliza creamos una red principal [transacción](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1) 0xe095cb (en decimales esto es 14718411). con la carga útil de datos

Esta transacción se incluyó en el bloque número [14711908](https://etherscan.io/block/14711908), la cual
aterrizó el 5 de mayo de 2022 a las 05:00:27 PM +UTC y tuvo el bloque hash
`0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3`.
Este hash fue entonces hashado recursivamente 1024 veces. La salida es `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`.

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

