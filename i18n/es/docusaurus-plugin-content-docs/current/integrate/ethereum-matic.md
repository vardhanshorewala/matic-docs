---
id: ethereum-polygon
title: Ethereum ↔ Polygon
description: Desarrolla tu próxima app de cadena de bloques en Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Solución asegurada por plasma para transferir tus activos Ethereum a Polygon y vice-versa.
* Utiliza [matic.js](https://github.com/maticnetwork/matic.js) para interactuar con los contratos de Polygon Plasma.

<!-- * [getting-started](https://maticnetwork.github.io/matic.js/): Set-up the environment for maticjs.
1. [(Ethereum → Matic)](/docs/develop/maticjs/deposit): Deposit assets from root chain to Matic.
2. [(Matic ↔ Matic)](/docs/develop/maticjs/transfer): Transfer assets between accounts on Matic.
3. [(Matic → Ethereum)](/docs/develop/maticjs/withdraw): Withdraw assets from Matic to root chain. -->

## Flujo {#flow}
Aquí está el flujo con la implementación de tus contratos en Polygon y soporte para Ethereum↔Polygon.

1. El usuario implementa el token ERC-20 en Ethereum - XToken

2. Ahora comparte la dirección de tu contrato con [Polygon](https://t.me/joinchat/HkoSvlDKW0qKs_kK4Ow0hQ). Este es un ejemplo de solicitud...

> Hola a todos, somos AwesomeDApp implementada en Polygon. Buscando una solución para transferir mis activos de Ethereum a Polygon y vice-versa. <br/><br/>
> Una breve descripción en mi AwesomeDApp...<br/><br/>
> Token_Address (dirección de token) en Ropsten-> "0x.."<br/>
> Token_Name-> (nombre de token) "XToken"<br/>
> Token_Symbol-> (símbolo de token) "X"<br/>
> Token_Decimals-> (decimales de token) "18"<br/><br/>
> Se solicita que mapees estos tokens a la versión testnet de Polygon.<br/>

Implementaremos un contrato secundario para ti en Polygon que puede ser flexible en función de los requisitos y mapeado a tus tokens Ethereum ↔ Polygon.( La implementación en Polygon requiere su token nativo Polygon, que se puede depositar desde Ethereum a Polygon o se puede comprar en el mercado secundario).

3. El usuario puede acuñar los Xtokens y transferir en Ethereum. Por ejemplo, digamos que se acuñan 100XToken y luego se transfieren a otra cuenta.

4. Para aprovechar estos tokens en la cadena de Polygon, llama al depósito de la función, que requerirá dos transacciones: primero aprueba y luego deposita ERC20.

5. Ahora 100XTokens están disponibles en la cadena de Polygon en la misma dirección.

6. Puedes transferir 50 XToken desde TuDirección a la NuevaDirección. Nuevamente, para transacciones en Polygon similares a Ethereum, Polygon utiliza su propio token nativo.

7. Si los usuarios quieren recuperar estos Xtokens en la cadena de Ethereum, entonces llama a StartWithdraw (iniciar retiro), que se retirará del contrato de token secundario y quemará estos tokens en la cadena de Polygon. Para evitar cualquier mala participación, se realizará una serie de validaciones. Una vez hecho esto, los tokens estarán disponibles en la cadena de Ethereum.

8. Llama a las salidas del proceso para recibir esos tokens en tu EOA o en la dirección de tu cuenta.

9. Deberías ver los 50 XToken en la red principal de Ethereum en la dirección de tu cuenta.
