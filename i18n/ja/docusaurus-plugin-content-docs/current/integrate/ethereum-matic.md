---
id: ethereum-polygon
title: Ethereum ↔ Polygon
description: Polygonで新しいブロックチェーンアプリを構築します。
keywords:
  - docs
  - matic
  - polygon
  - ethereum
image: https://wiki.polygon.technology/img/polygon-wiki.png
---

# Ethereum ↔ Polygon {#ethereum-polygon}

Plasmaのセキュアなソリューションで資産のEthereumからPolygonへの転送やその逆をすることができます。
*  [matic.js](https://github.com/maticnetwork/matic.js)を使用してPolygon Plasmaコントラクトとやり取りします。

## フロー {#flow}
これはPolygonでコントラクトをデプロイすることとEthereum↔Polygonをサポートするためのフローです。

1. ユーザーはERC-20トークンをEthereumにデプロイします - XToken

2. ここで [Polygon](https://t.me/joinchat/HkoSvlDKW0qKs_kK4Ow0hQ) とコントラクトアドレスを共有します。これはリクエスト例です...

> みなさんこんにちは。私たちはPolygonにデプロイされたAwesomeDAppです。アセットをEthereumからPolygon、またはその逆に転送するためのソリューションを探していますか <br/><br/>
> AwesomeDAppに関する簡単な説明です...<br/><br/>
> RopstenのToken_Address-> "0x..<br/>
> Token_Name-> "XToken<br/>
> Token_Symbol-> "X"<br/>
> Token_Decimals-> "18"<br/><br/>
> これらのトークンをPolygonテストネットバージョンにマッピングするようあなたに求めます。<br/>

私たちがあなたのためにPolygonにデプロイするコントラクトは要件に応じて柔軟であり、Ethereum↔Polygonトークンにマッピングされます。(Polygonにデプロイするには、ネイティブなトークンPolygonが必要であり、これはEthereumからPolygonに預け入れたり、Secondary Market Placeで購入したりすることができます。)

3. ユーザーはXtokenをミントし、Ethereumで転送することができます。 たとえば、100XTokenをミントし、これを別のアカウントに転送することにします。

4. Polygonチェーンでこれらのトークンを使用可能にするためには、機能預け入れを呼び出すと、これがまず承認とその後ERC20の預け入れの２つのトランザクションを呼び出します。

5. 現在、100XTokensはPolygonチェーンで同一アドレスで利用可能です。

6. YourAddressからNewAddressに50XTokenを転送することもできます。Ethereumと同様のPolygonでのトランザクションでも、Polygonは独自のネイティブトークンを使用します。

7. ユーザーがこれらのXtokenをEthereumチェーンに戻したい場合は、StartWithdrawを呼び出すと、これがchildTokenContractから引き出し、これらのトークンをPolygonチェーンでバーンします。あらゆる不正の参加を避けるために、バリデーションのセットが行われます。これがいったん完了すると、トークンはEthereumチェーンで利用可能になります。

8. これらのトークンをEOAまたはアカウントアドレスに戻すには、processExits()を呼び出します。

9. アカウントアドレスでEthereumメインネットに50XTokenが表示されるはずです。
