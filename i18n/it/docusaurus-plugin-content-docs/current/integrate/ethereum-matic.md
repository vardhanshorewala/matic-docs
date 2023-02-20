---
id: ethereum-polygon
title: Ethereum ↔ Polygon
description: Costruisci la tua prossima app blockchain su Polygon.
keywords:
  - docs
  - matic
  - polygon
  - ethereum
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

# Ethereum ↔ Polygon {#ethereum-polygon}

Plasma è una soluzione sicura per trasferire i tuoi asset da Ehereum a Polygon e viceversa.
* Usa [matic.js](https://github.com/maticnetwork/matic.js) per interagire con i contratti Plasma di Polygon.

## Flusso {#flow}
Ecco il Flusso con la distribuzione dei tuoi contratti su Polygon e il Supporto per Ethereum↔Polygon.

1. L'utente distribuisce il token ERC-20 su Ethereum - XToken

2. Ora condividi l'indirizzo del tuo contratto con [Polygon](https://t.me/joinchat/HkoSvlDKW0qKs_kK4Ow0hQ). Ecco un esempio di richiesta...

> Ciao a tutti, ecco AwesomeDApp distribuita su Polygon. Cerco una soluzione per trasferire i miei asset da Ethereum a Polygon e viceversa. <br/><br/>
> Una breve descrizione della mia AwesomeDApp...<br/><br/>
> Token_Address su Ropsten-> "0x.."<br/>
> Token_Name-> "XToken"<br/>
> Token_Symbol-> "X"<br/>
> Token_Decimals-> "18"<br/><br/>
> Ti richiede di mappare questi token sulla Polygon Testnet.<br/>

Distribuiremo per te un contratto figlio su Polygon che può essere adattato in base ai requisiti e mappato sui tuoi token Ethereum ↔ Polygon. ( La distribuzione su Polygon richiede il token nativo di Polygon che può essere depositato da Ethereum a Polygon oppure può essere acquistato nel mercato secondario).

3. L'utente può effettuare il minting degli Xtoken e trasferirli su Ethereum. Ad esempio, vengono creati 100X Token e poi trasferiti su un altro account.

4. Per usufruire di questi token sulla Polygon chain, chiama la funzione deposita che richiederà due transazioni, prima approva quindi depositERC20.

5. Ora 100 XToken sono disponibili sulla Polygon chain allo stesso indirizzo.

6. Puoi trasferire 50 XToken da YourAddress a NewAddress. Similmente ad Ethereum, per eseguire transazioni su Polygon è necessario il token nativo della blockchain.

7. Nel caso gli utenti desiderino recuperare questi Xtoken sulla Ethereum chain, è necessario chiamare StartWithdraw che preleverà questi token da childTokenContract ed effettuerà il burning sulla Polygon chain. Per evitare qualsiasi tentativo fraudolento di partecipazione, avrà luogo una serie di convalide. Una volta fatto, i token saranno disponibili sulla Ethereum chain.

8. Chiama processExits() per ricevere quei token nel tuo EOA o all'indirizzo del tuo account.

9. Dovresti vedere i 50 XToken sulla Ethereum mainnet all'indirizzo del tuo account.
