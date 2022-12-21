
# Cérémonie MPC {#mpc-ceremony}
Les preuves à divulgation nulle de connaissance nécessitent une configuration fiable. Cette configuration génère un « résidu toxique » qui pourrait potentiellement permettre de créer de fausses preuves. Pour éviter cela, une cérémonie doit avoir lieu où cette configuration est générée via le calcul multipartite (MPC).

Nightfall a effectué un calcul multipartite (MPC) suivant les mêmes principes de la cérémonie Perpetual Powers of Tau. Le processus a commencé avec la contribution 72 de la cérémonie Perpetual Powers of Tau pour la courbe BN254. Vous pouvez trouver cette contribution [ici](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response).

Comme Nightfall utilise le schéma de preuve Groth16, une deuxième phase du MPC est nécessaire pour chaque circuit. 4 contributions privées ont fait partie de cette phase 2 :

1. [Darko Macesic (identifiant github : dark64)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna (identifiant github : jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody (responsable mondial de la blockchain chez EY)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor (identifiant github : iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

Après la dernière contribution, nous avons appliqué une balise aléatoire pour les 4 circuits. Pour cette balise, nous avons créé une [transaction](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1) pour le mainnet avec la charge utile de données 0xe095cb (en décimal, 14718411).

Cette transaction a été incluse dans le bloc numéro [14711908](https://etherscan.io/block/14711908), qui
a atterri le 5 mai 2022 à 17:00:27 +UTC et a eu le hachage de blocs
`0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3`.
Ce hachage a ensuite été haché récursivement 1024 fois. Le résultat est `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`.

Le hachage final a été calculé avec ce programme :

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

 Les informations complètes sur la phase 2 sont disponibles [ici](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md).

