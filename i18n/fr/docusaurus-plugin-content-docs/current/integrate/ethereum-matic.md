---
id: ethereum-polygon
title: Ethereum ↔ Polygon
description: Créez votre prochaine application blockchain sur Polygon.
keywords:
  - docs
  - matic
  - polygon
  - ethereum
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

# Ethereum ↔ Polygon {#ethereum-polygon}

Solution sécurisée Plasma pour transférer vos actifs d'Ethereum vers Polygon et vice versa.
* Utilisez [matic.js](https://github.com/maticnetwork/matic.js) pour interagir avec les contrats Polygon Plasma.

## Flux {#flow}
Voici le flux avec le déploiement de vos contrats sur Polygon et le support pour Ethereum↔Polygon.

1. L'utilisateur déploie un jeton ERC-20 sur Ethereum - xToken

2. Partagez maintenant votre adresse contractuelle avec ​ [Polygon](https://t.me/joinchat/HkoSvlDKW0qKs_kK4Ow0hQ). Voici un exemple de demande...

> Bonjour à tous, Nous sommes AwesomeDApp, déployé sur Polygon. Je cherche une solution pour transférer mes actifs d'Ethereum à Polygon et vice versa. <br/><br/>Une brève description sur mon AwesomeDApp...<br/><br/> Token_Address sur Ropsten-> "0x.."<br/> Token_Name-> "XToken"<br/> Token_Symbol-> "X"<br/> Token_Decimals-> "18"<br/><br/> Vous demandant de mapper ces jetons avec la version de Polygon Testnet.<br/>

Nous mettrons en place un contrat enfant pour vous sur Polygon, qui pourra être flexible en fonction des exigences et mappé sur vos jetons Ethereum ↔ Polygon. ( le déploiement sur Polygon nécessite son jeton natif Polygon, qui peut être déposé d'Ethereum à Polygon ou peut être acheté sur le marketplace secondaire.)

3. L'utilisateur peut lancer les xToken et transférer sur Ethereum. Par exemple, imaginons que 100 xToken sont lancés puis transférés vers un autre compte.

4. Pour bénéficier de ces jetons sur la chaîne Polygon, il faut activer la fonction Appel qui appellera deux transactions : approuver puis déposer des ERC20.

5. Maintenant, 100 xToken sont disponibles sur la chaîne Polygon à la même adresse.

6. Vous pouvez transférer 50 xToken de votre adresse à la nouvelle adresse. Encore une fois, pour les transactions sur Polygon similaires à Ethereum, Polygon utilise son propre jeton natif.

7. Si les utilisateurs veulent récupérer ces xToken sur la chaîne Ethereum, vous pouvez appeler StartWithdraw, qui se retirera du contrat de jetons enfant et gravera ces jetons sur la chaîne Polygon. Pour éviter toute mauvaise participation, un ensemble de validations aura lieu. Aussitôt après, les jetons seront disponibles sur la chaîne Ethereum.

8. Appelez processExits() pour recevoir ces jetons à votre adresse EOA ou à votre adresse de compte.

9. Vous devriez voir les 50 xToken sur le réseau principal Ethereum à votre adresse de compte.
