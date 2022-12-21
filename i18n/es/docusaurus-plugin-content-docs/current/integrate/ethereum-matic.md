---
id: ethereum-polygon
title: Ethereum ↔ Polygon
description: Desarrolla tu próxima app de cadena de bloques en Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Solución segura con Plasma para transferir tus activos de Ethereum a Polygon y viceversa.
* Utiliza [matic.js](https://github.com/maticnetwork/matic.js) para interactuar con los contratos Plasma de Polygon.

<!-- * [getting-started](https://maticnetwork.github.io/matic.js/): Set-up the environment for maticjs.
1. [(Ethereum → Matic)](/docs/develop/maticjs/deposit): Deposit assets from root chain to Matic.
2. [(Matic ↔ Matic)](/docs/develop/maticjs/transfer): Transfer assets between accounts on Matic.
3. [(Matic → Ethereum)](/docs/develop/maticjs/withdraw): Withdraw assets from Matic to root chain. -->

## Flujo {#flow}
A continuación, mostramos el flujo para el despliegue de tus contratos en Polygon y el soporte para Ethereum↔Polygon.

1. El usuario despliega tokens ERC-20 a Ethereum - XToken

2. Ahora, comparte tu dirección de contrato con [Polygon](https://t.me/joinchat/HkoSvlDKW0qKs_kK4Ow0hQ). Un ejemplo de solicitud se ve así:

> Hola a todos: Somos AwesomeDApp desplegada en Polygon. Estamos buscando una solución para transferir mis activos de Ethereum a Polygon y viceversa. <br/><br/>
> Breve descripción en mi AwesomeDApp:<br/><br/>
> Dirección_Token en Ropsten-> "0x.."<br/>
> Nombre_Token-> "TokenX"<br/>
> Símbolo_Token-> "X"<br/>
> Decimales_Token-> "18"<br/><br/>
> Solicitamos que mapees estos tokens a la versión de red de prueba de Polygon.<br/>

Desplegaremos un contrato secundario para ti en Polygon, el cual puede ser flexible según los requisitos y estar mapeado a tus tokens Ethereum ↔ Polygon. (El despliegue en Polygon requiere tokens nativos de Polygon, los cuales pueden depositarse de Ethereum a Polygon o comprarse en un mercado secundario).

3. El usuario puede acuñar los tokens X y transferirlos a Ethereum. Por ejemplo, digamos que se acuñan 100 tokens X y, luego, se transfieren a otra cuenta.

4. Para usar estos tokens en la cadena de Polygon, llama al depósito de función, que llamará a dos transacciones: primero, la aprobación y, luego, depositERC20.

5. Ahora, los 100 tokens X están disponibles en la cadena de Polygon en la misma dirección.

6. Puedes transferir 50 tokens X de YourAddress a NewAddress. De nuevo, para las transacciones en Polygon similares a Ethereum, Polygon utiliza su propio token nativo.

7. Si los usuarios quieren recuperar estos tokens X en la cadena de Ethereum, deben llamar a StartWithdraw, con lo que podrán retirarlos de childTokenContract y quemarlos en la cadena de Polygon. Para evitar cualquier mala participación, se realizará un conjunto de validaciones. Una vez realizadas, los tokens estarán disponibles en la cadena de Ethereum.

8. Llama a processExits() para recuperar esos tokens en tu EOA o tu dirección de cuenta.

9. Deberás ver los 50 tokens X en la red principal de Ethereum en tu dirección de cuenta.
