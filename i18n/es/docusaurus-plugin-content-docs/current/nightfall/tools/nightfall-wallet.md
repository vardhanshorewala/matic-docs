---
id: nightfall-wallet
title: Billetera Nightfall
sidebar: Nightfall Wallet
description: "Guía de la billetera Nightfall de Polygon"
keywords:
  - docs
  - matic
  - polygon
  - nightfall
  - wallet
image: https://matic.network/banners/matic-network-16x9.png

---

La billetera Nightfall de Polygon es una billetera de navegador que puede interactuar con la
 versión beta de la red principal de Nightfall.

:::info Utiliza la billetera Nightfall para realizar depósitos, transferencias y retiradas

### Restricciones {#restrictions}

Mientras Nightfall alcanza un estado de madurez, se aplican las siguientes restricciones:


| Token ERC-20 | Depósito máx. | Retirada máx. |
|-------------|-------------|--------------|
| MATIC | 250 MATIC | 1000 MATIC |
| WETH | 0,25 WETH | 1 WETH |
| DAI | 250 DAI | 1000 DAI |
| USDT | 250 USDT | 1000 USDT |
| USDC | 250 USDC | 1000 USDC |

:::

:::caution Medidas de seguridad

La billetera Nightfall ha sido probada en un navegador Chrome. Durante la fase beta, el kilometraje puede variar en otros
 navegadores.

**Te recomendamos enormemente que uses Nightfall en Chrome**.

:::



## Comenzar {#getting-started}

Visita la [billetera web de red principal](https://wallet-beta.polygon.technology) de Polygon o
 la [billetera de red de prueba](https://wallet.testnet.polygon-nightfall.technology/), conecta tu cuenta de MetaMask
 y selecciona billetera de Polygon de la izquierda. Si necesitas ayuda con MetaMask, consulta la:
 [documentación de Polygon sobre MetaMask](../../develop/metamask/tutorial-metamask.md)

![](../imgs/tools-wallet/polygon-wallet-click-nf.png)

En este momento, la billetera te pedirá que cambies a la red de Polygon, y una ventana emergente de Metamask
 te solicitará que confirmes el cambio.

![](../imgs/tools-wallet/polygon-network.png)

Luego, en la sección superior de la billetera, haz clic en el menú desplegable y selecciona `Polygon Nightfall`, y
 aparecerá una nueva solicitud para cambiar a una red principal de Ethereum. Por favor, acepta cambiar a la red principal de Ethereum
 para operar con Polygon Nightfall.

![](../imgs/tools-wallet/polygon-network-dropdown-nf.png)

Si estás trabajando en la red de prueba, la URL de la billetera te llevará inmediatamente a la página de destino de la billetera Nightfall de Polygon.

![](../imgs/tools-wallet/wallet-main-screen.png)

En tu primera visita, habrá que crear tu billetera Nightfall. Debería aparecer una ventana emergente para generar una frase mnemotécnica y crear la billetera. Haz clic en `Generate Mnemonic`, después `Create Wallet`. **Ten en cuenta que solo puedes utilizar esta billetera en tu dispositivo actual**.

![](../imgs/tools-wallet/generate-mnemonic-create-wallet.png)

:::caution Haz una copia de seguridad de tus compromisos y frase mnemotécnica

Las claves de tu billetera y las transacciones se almacenan en el navegador (IndexedDb). Al igual que la frase mnemotécnica que configuras cuando accedes a la billetera Nightfall por primera vez.

Asegúrate de almacenar esta frase mnemotécnica en algún lugar seguro. Es la única forma de poder presentar pruebas compatibles con tus fondos en L2. Lo mismo sucede con tus compromisos: no te olvides de guardarlos de forma segura pulsando `export commitments` siempre que uses otro navegador u otra máquina.

:::

**Si pierdes tus compromisos, tus fondos se pierden para siempre**


En este momento, deberías poder ver tu MetaMask y las direcciones de tu billetera Nightfall (arriba a la derecha).

**Espera unos minutos más a que termine la configuración de la billetera antes de empezar a hacer transacciones**.

En la esquina inferior izquierda de la billetera, el estado de la billetera aparecerá como `Syncing Nightfall`. En este estado, la billetera está recuperando los
 circuitos ZK y el estado de la red necesarios para realizar transacciones.

![](../imgs/tools-wallet/wallet-state-syncing.png)

Espera hasta que el estado de la billetera cambie a `Nightfall Synced`

![](../imgs/tools-wallet/wallet-state-synced.png)


## Cómo conectar una billetera de hardware Ledger a Nightfall {#how-to-connect-a-ledger-hardware-wallet-to-nightfall}
Hay una guía para conectar tu billetera de hardware Ledger con MetaMask en el sitio web oficial de MetaMask [aquí](https://support.ledger.com/hc/en-us/articles/4404366864657-How-to-access-your-Ledger-Ethereum-ETH-account-via-Metamask?docs=true).

Asegúrate de conectar la app de Ethereum a tu billetera y de habilitar la "firma a ciegas" en la configuración de la app de Ethereum


### La dirección de tu billetera {#your-wallet-address}
Obtén la dirección de tu billetera Nightfall desde la página de activos de Nightfall pulsando en `Receive`.

![](../imgs/tools-wallet/nightfall-wallet-address.png)

## Cómo realizar depósitos {#how-to-make-deposits}
Desde la página de activos de Nightfall, pulsa en el botón `Deposit` a la derecha del activo seleccionado o navega hasta la página del puente L2.

1. Comprueba que el modo de transferencia está establecido como `Deposit`
2. Comprueba que el token deseado esté seleccionado (WETH, MATIC, etc.)
3. Introduce el valor que hay que depositar en tu billetera Nightfall y pulsa en `Transfer`
4. Revisa la transacción en la ventana emergente
5. Haz clic en `Create Transaction`

![](../imgs/tools-wallet/deposit-click-transfer.png)

Se iniciará un proceso para calcular el ZKP y preparar la transacción: concede a MetaMask acceso a los saldos de tu cuenta. Cuando esto finalice, pulsa en `Send Transaction`: concede a MetaMask permisos adicionales para la interacción con el contrato.

![](../imgs/tools-wallet/deposit-tx-created-and-ready-to-be-sent.png)

Ve a la página de Transacciones para [ver tu depósito](#view-transactions).

### Información importante sobre depósitos {#important-information-about-deposits}
- [Las cantidades depositadas están restringidas](#note-the-following-deposit-and-withdrawal-restrictions) mientras estén en la versión beta

## Cómo realizar transferencias {#how-to-make-transfers}
Desde la página de activos de Nightfall, haz clic en el botón `Send` a la derecha del activo seleccionado.

1. Introduce una dirección válida existente en la Polygon Nightfall L2
2. Comprueba que el token deseado esté seleccionado (WETH, MATIC, etc.)
3. Introduce valor que hay que transferir desde tu billetera Nightfall, haz clic en `Continue`

![](../imgs/tools-wallet/send-nf.png)

Se iniciará un proceso para calcular el ZKP y preparar la transacción. Cuando este proceso termine, haz clic en `Send Transaction`.

Ve a la página de Transacciones para [ver tu transferencia](#view-transactions).

### Información importante sobre transferencias {#important-information-about-transfers}
Los actuales circuitos de transferencia de ZKP que se usan en Nightfall restringen las cantidades de transferencia a la que coincida exactamente con el valor de
 un compromiso existente o a cualquier combinación lineal de dos compromisos existentes.

Para explicar las restricciones de transferencia con un ejemplo, observa los siguientes conjuntos de compromisos:

- Conjunto A: [1, 1, 1, 1, 1, 1]
- Conjunto B: [2, 2, 2]
- Conjunto C: [2, 4]

Aunque los tres conjuntos tienen sumas totales equivalentes a 6, solo están disponibles las siguientes transferencias:

- Conjunto A: cualquier transferencia entre 0 y 2 (ambas excluidas)
- Conjunto B: cualquier transferencia entre 0 y 4 (ambas excluidas)
- Conjunto C: cualquier transferencia entre 0 y 6 (ambas excluidas)

Para seguir con el ejemplo, si Alex posee el conjunto C de compromisos, las transferencias disponibles incluyen cualquier cantidad entre 0 y 6, excluyendo ambos valores límite. Si Alex decide transferir 3,5 a Bob, Alex terminará con solo compromiso de 2,5 y Bob recibirá un compromiso de 3,5 cuando se proponga el bloque.

Por otro lado, si Alex decide transferir una cantidad de 6 a Bob, la prueba de ZK fallará, ya que no habrá una combinación válida de compromisos.

**Hay que tener en cuenta que estos valores representan compromisos adquiridos**, no p. ej., depósitos. Información adicional disponible en la sección de [compromisos](../protocol/commitments.md) de estos documentos.

## Cómo realizar retiradas {#how-to-make-withdrawals}
Desde la página de activos de Nightfall, pulsa en el botón `Withdraw` a la derecha del activo seleccionado o navega hasta la página del puente L2.

1. Comprueba que el modo de transferencia está establecido como `Withdraw`
2. Comprueba que el token deseado esté seleccionado (WETH, MATIC, etc.)
3. Introduce el valor que va a retirarse de tu billetera Nightfall y haz clic en `Transfer`
4. Revisa la transacción en la ventana emergente
5. Haz clic en `Create Transaction`

Se iniciará un proceso para calcular el ZKP y preparar la transacción. Cuando este proceso termine, haz clic en `Send Transaction`.

Ve a la página de Transacciones para [ver tu retirada](#view-transactions). Cuando venza el periodo de finalización de una semana, el usuario
 podrá finalizar y reclamar la cantidad de retirada.

### Información importante sobre retiradas {#important-information-about-withdrawals}
- El valor de retirada debe coincidir exactamente con la cantidad en uno de los compromisos adquiridos (más información en [acerca de los compromisos](#learn-about-commitments))
- Las retiradas tienen un periodo de finalización **de una semana** desde el momento en que se creó el bloque incluyendo la transacción de retirada. Cuando este periodo haya transcurrido, puedes finalizar la retirada para que tus fondos sean enviados a tu cuenta de Ethereum.
- [Las cantidades de retirada están restringidas](#note-the-following-deposit-and-withdrawal-restrictions) mientras estén en la versión beta
- Las retiradas son una transacción en la cadena y pagará las tarifas de gas durante la solicitud de transacción y también cuando la retirada esté finalizada.

![](../imgs/tools-wallet/cooling-off-vs-ready.png)

## Ver transacciones {#view-transactions}
Comprueba el estado de tus depósitos, transferencias y retiradas en la página de Transacciones. Ten en cuenta que cada transacción se procesa en cuanto hay suficientes transacciones para producir un bloque o después de 6 horas.

![](../imgs/tools-wallet/transactions.png)
