
# Cerimonia MPC {#mpc-ceremony}
Le Zero-Knowledge Proof richiedono una configurazione fidata. Questa configurazione genera un cosiddetto "rifiuto tossico", che potrebbe potenzialmente consentire di creare dimostrazioni false. Per evitare questo inconveniente, è necessario tenere una cerimonia in cui la configurazione viene generata tramite computazione a parti multiple (Multi-Party Computation, o MPC).

Nightfall ha eseguito un'MPC seguendo gli stessi principi della cerimonia "Perpetual Powers of Tau". Il processo è iniziato con il contributo 72 della cerimonia "Perpetual Powers of Tau" per BN254 Curve. Il contributo è consultabile [qui](https://github.com/weijiekoh/perpetualpowersoftau/tree/master/0071_edward_response).

Dato che Nightfall utilizza il sistema di prova Groth16, è stata necessaria una seconda fase di MPC per ogni circuito. Questa seconda fase è stata costituita da 4 contributi privati:

1. [Darko Macesic (ID Github: dark64)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/1_Darko.md)
2. [Jordi Bailyna (ID Github: jbaylina)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/2_Baylina.md)
3. [Paul Brody (Global Blockchain Leader di EY)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/3_Brody.md)
4. [Michael Connor (ID Github: iAmMichaelConnor)](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/4_Connor.md)

Dopo l'ultimo contributo, abbiamo applicato un beacon casuale per i 4 circuiti. Per questo beacon abbiamo creato una [transazione](https://etherscan.io/tx/0xd42eff8e34aa9227cdceb12daf1d868b3dec025ac23073cfd103bb697642dbc1) mainnet con il payload dati 0xe095cb (in decimali, 14718411).

La transazione è stata inclusa nel blocco numero [14711908](https://etherscan.io/block/14711908),
ottenuto il 5 maggio 2022 alle 17:00:27 +UTC con hash blocco
`0x875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3`.
L'hash è stato poi sottoposto a un'esecuzione di hash ricorsivo per 1024 volte. L'output è `0x144212c1ae36d729307364dcb845a04b9c5f523fe557eb777a910d4ea6cc5a09`.

L'hash finale è stato calcolato con questo programma:

```js
import crypto from 'crypto';

let h = '875966a4d290bae914acd733315d1a1cbea3fb2b9fde133a0c6fffa7f726cbe3';
for (let i = 0; i < 1024; i++) {
  h = crypto.createHash('sha256').update(h, 'hex').digest('hex');
}
console.log(h);
```

Le informazioni complete sulla fase 2 sono disponibili [qui](https://github.com/maticnetwork/nightfall_phase2ceremony/blob/main/atttestations/phase2.md).

