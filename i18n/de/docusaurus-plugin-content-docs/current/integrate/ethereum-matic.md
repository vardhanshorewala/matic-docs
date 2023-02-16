---
id: ethereum-polygon
title: Ethereum ↔ Polygon
description: Erstelle deine nächste Blockchain-App auf Polygon.
keywords:
  - docs
  - matic
  - polygon
  - ethereum
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

# Ethereum ↔ Polygon {#ethereum-polygon}

Die sichere Lösung von Plasma, mit der Sie Ihre Aktiva von Ethereum zu Polygon und umgekehrt übertragen können.
* Mit [matic.js](https://github.com/maticnetwork/matic.js) gibt es einen Datenaustausch mit dem Polygon Plasma Contracts.

## Ablauf {#flow}
Nachfolgend der Ablauf, mit dem Ihrer Verträge auf Polygon und Support für Ethereum↔Polygon eingesetzt werden.

1. Der Benutzer stellt ERC-20 Token an Ethereum bereit – XToken

2. Geben Sie nun Ihre Contract-Adresse an [Polygon](https://t.me/joinchat/HkoSvlDKW0qKs_kK4Ow0hQ) weiter. Hier ist eine Beispielanfrage...

> Hallo zusammen, wir sind AwesomeDApp und bei Polygon im Einsatz. Auf der Suche nach einer Lösung, mit der meine Aktiva von Ethereum zu Polygon and umgekehrt übertragen werden können. <br/><br/>
> Eine Kurzbeschreibung über meine AwesomeDApp...<br/><br/>
> Token_Adresse bei Ropsten-> "0x."
> <br/>Token_Name-> "XToken"<br/>
> Token_Symbol-> "X"<br/>
> Token_Dezimalstellen-> "18"<br/><br/>
> Wir ersuchen Sie, diese Token der Polygon Testnet Version zuzuordnen.<br/>

Wir haben für Sie einen Child-Contract auf Polygon, der flexibel basierend auf den Voraussetzungen und auf Ihre Token Ethereum ↔ Polygon angepasst werden kann. ( Für den Einsatz auf Polygon brauchen Sie native Polygon-Token, die von Ethereum zu Polygon eingezahlt oder am Sekundärmarkt erworben werden können.

3. Der Benutzer kann Xtoken ausstellen und auf Ethereum übertragen. Nehmen wir, es wurden 100XToken ausgegeben und anschließend auf ein anderes Konto übertragen.

4. Wenn Sie diese Token auf der Polygon-Chain nutzen möchten, rufen Sie die Funktion Einzahlung auf, die zwei Transaktionen voraussetzt: Erstens die Genehmigung und zweitens die Einzahlung von ERC20.

5. Jetzt sind 100XToken auf der Polygon-Chain an der gleichen Adresse verfügbar.

6. Sie können 50 XToken von Ihrer zur neuen Adresse übertragen. Wir weisen nochmals darauf hin, Transaktionen auf Polygon braucht es ähnlich wie bei Ethereum die eigenen nativen Token.

7. Wenn die Nutzer diese Xtoken auf der Ethereum Chain zurückbekommen wollen, rufen Sie die Funktion StartWithdraw auf, worauf der ChildTokenContract widerrufen wird und diese Token auf der Polygon Chain ausgeschieden werden. Um eine Benachteiligung zu vermeiden, gibt es eine Reihe von Überprüfungen. Sobald dies geschehen ist, sind die Token auf der Ethereum Chain verfügbar.

8. Rufen Sie processExits() auf, um diese Token an Ihre EOA- oder Ihre Kontoadresse zurückzubekommen.

9. Sie sollten die 50 XToken auf dem Ethereum Mainnet auf Ihrem Konto sehen.
