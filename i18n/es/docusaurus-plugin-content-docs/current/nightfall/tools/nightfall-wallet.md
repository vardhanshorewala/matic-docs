---
id: nightfall-wallet
title: Billetera Nightfall
sidebar: Nightfall Wallet
description: "Guía de la billetera de Polygon Nightfall"
keywords:
  - docs
  - matic
  - polygon
  - nightfall
  - wallet
image: https://matic.network/banners/matic-network-16x9.png

---

La billetera de Polygon Nightfall es una billetera de navegador que es capaz de interactuar con la
mainnet beta de Nightfall lanzada.

:::info Utilice la billetera Nightfall para realizar depósitos, transferencias y retiros

### Restricciones {#restrictions}

Mientras que Nightfall logra un estado maduro, se aplican las siguientes restricciones:


| Token ERC-20 | Depósito máximo | Retiro máximo |
|-------------|-------------|--------------|
| MATIC | 250 MATIC | 1000 MATIC |
| WETH | 0,25 WETH | 1 WETH |
| DAI | 250 DAI | 1000 DAI |
| USDT | 250 USDT | 1000 USDT |
| USDC | 250 USDC | 1000 USDC |

:::

:::caution Medidas de seguridad

La billetera Nightfall se prueba en un navegador Chrome. Durante la versión Beta, el millaje puede variar en otros
navegadores.

**Le recomendamos encarecidamente que use Nightfall en Chrome**.

:::



## Cómo empezar {#getting-started}

Visita la web de Polygon [billetera de mainnet](https://wallet-beta.polygon.technology) o
[billetera de la red de pruebas](https://wallet.testnet.polygon-nightfall.technology/), conecte su cuenta
Metamask y seleccione la billetera de Polygon a la izquierda. Si necesita ayuda con Metamask, consulte la
[documentación de Polygon en Metamask](../../develop/metamask/tutorial-metamask.md)

![](../imgs/tools-wallet/polygon-wallet-click-nf.png)

En este punto, la billetera le pedirá que cambie a la red de Polygon y una ventana emergente de Metamask
solicitará que confirme el cambio.

![](../imgs/tools-wallet/polygon-network.png)

A continuación, en la sección superior de la billetera, haga clic en el menú desplegable y seleccione `Polygon Nightfall`, y una
nueva solicitud para cambiar a la red principal de Ethereum aparecerá. Acepte cambiar a la red principal de Ethereum
para trabajar con Polygon de Nightfall.

![](../imgs/tools-wallet/polygon-network-dropdown-nf.png)

Si está trabajando en la red de pruebas, la URL de la billetera lo llevará inmediatamente a la página landing de la billetera de Polygon de Nightfall.

![](../imgs/tools-wallet/wallet-main-screen.png)

En su primera visita, tendrá que crear su billetera de Nightfall. Una ventana emergente deberá aparecer para generar un mnemónico y crear la billetera Haga clic en `Generate Mnemonic`, después `Create Wallet`. **Nota: Solo puede utilizar esta billetera en su dispositivo actual**.

![](../imgs/tools-wallet/generate-mnemonic-create-wallet.png)

:::caution Respalde sus compromisos y mnemónicos

Las claves y transacciones de su billetera se almacenan en el navegador (IndexedDb). Lo mismo para el mnemónico que configura cuando accede a la billetera de Nightfall por primera vez.

Asegúrese de almacenar este mnemónico en algún lugar seguro. Es la única manera de poder producir pruebas compatibles con sus fondos en L2. Lo mismo ocurre con sus compromisos: asegúrese de almacenarlos de forma segura haciendo clic en `export commitments` cuando use otro navegador o máquina.

:::

**Si pierde sus compromisos, sus fondos se pierden para siempre**


En este punto, debe poder ver tanto sus direcciones Metamask como las de su billetera Nightfall (superior derecha).

**Permita algunos minutos más para completar la configuración de su billetera antes de empezar a hacer transacciones**.

En la esquina inferior izquierda de la billetera, el estado de la billetera se mostrará como `Syncing Nightfall`. En este estado, la billetera está recuperando los
circuitos ZK y el estado de la red necesarios para realizar transacciones.

![](../imgs/tools-wallet/wallet-state-syncing.png)

Espere hasta que el estado de la billetera cambie a `Nightfall Synced`

![](../imgs/tools-wallet/wallet-state-synced.png)


## Cómo conectar una billetera Ledger Hardware a Nightfall {#how-to-connect-a-ledger-hardware-wallet-to-nightfall}
Existe una guía para conectar su billetera Ledger Hardware con Metamask en el sitio oficial de Metamask [aquí](https://support.ledger.com/hc/en-us/articles/4404366864657-How-to-access-your-Ledger-Ethereum-ETH-account-via-Metamask?docs=true).

Asegúrese de conectar la app de Ethereum en su billetera y habilite "la firma ciega" en la configuración de la app de Ethereum.


### La dirección de su billetera {#your-wallet-address}
Obtenga la dirección de su billetera de Nightfall desde el sitio los activos de Nightfall al hacer clic en `Receive`.

![](../imgs/tools-wallet/nightfall-wallet-address.png)

## Cómo hacer depósitos {#how-to-make-deposits}
Desde la página de los activos de Nightfall, haga clic en el botón `Deposit` a la derecha del activo elegido, o navegue a la página del puente L2.

1. Revise que el modo de transferencia esté configurado en `Deposit`
2. Revise que el token deseado esté seleccionado (WETH, MATIC, etc.)
3. Ingrese el valor que se depositará en su billetera Nightfall, haga clic en `Transfer`
4. Revise la transacción en la ventana emergente
5. Haga clic en `Create Transaction`

![](../imgs/tools-wallet/deposit-click-transfer.png)

Comenzará un proceso para calcular el ZKP y preparar la transacción - otorgue acceso a Metamask a su cuenta de saldos. Cuando esto termine, haga clic en `Send Transaction` - otorgue acceso a Metamask a más permisos para la interacción con el contrato.

![](../imgs/tools-wallet/deposit-tx-created-and-ready-to-be-sent.png)

Vaya a la página de transacciones para [ver su depósito](#view-transactions).

### información importante sobre los depósitos {#important-information-about-deposits}
- [Los importes de depósito están restringidos](#note-the-following-deposit-and-withdrawal-restrictions) mientras se está en la versión Beta

## Cómo hacer transferencias {#how-to-make-transfers}
Desde la página de los activos de Nightfall, haga clic en el botón `Send` a la derecha del activo seleccionado.

1. Ingrese una dirección válida existente en el Polygon Nightfall L2.
2. Revise que el token deseado esté seleccionado (WETH, MATIC, etc.)
3. Ingrese el valor que se transferirá desde su billetera de Nightfall, haga clic en `Continue`

![](../imgs/tools-wallet/send-nf.png)

Iniciará un proceso para calcular el ZKP y preparar la transacción. Cuando esto termine, haga clic en `Send Transaction`.

Vaya a la página de transacciones para [ver su transferencia](#view-transactions).

### Información importante sobre sus transferencias {#important-information-about-transfers}
Los circuitos de transferencia ZKP actuales utilizados en Nightfall restringen los importes de transferencia ya sea para igualar exactamente el valor de uno de
los compromisos existentes o cualquier combinación lineal de dos compromisos existentes.

Para ilustrar las restricciones de las transferencias con un ejemplo, observe los siguientes conjuntos de compromisos:

- Conjunto A: [1, 1, 1, 1, 1, 1]
- Conjunto B: [2, 2, 2]
- Conjunto C: [2, 4]

Mientras que los tres conjuntos tienen cantidades equivalentes en total de 6, solo están disponibles las siguientes transferencias:

- Conjunto A: cualquier transferencia entre 0 y 2 (ambos excluidos)
- Conjunto B: cualquier transferencia entre 0 y 4 (ambos excluidos)
- Conjunto C: cualquier transferencia entre 0 y 6 (ambos excluidos)

Para continuar con el ejemplo, si Alex posee el conjunto C de los compromisos, las transferencias disponibles incluyen cualquier monto entre 0 y 6, excluyendo ambos valores límites. Si Alex decide transferir 3.5 a Bob, Alex terminará con un único compromiso de 2.5 y Bob recibirá un compromiso de 3.5 una vez que se proponga el bloque.

Por otro lado, si Alex decide transferir un monto de 6 a Bob, la prueba ZK fallará porque no habrá una combinación válida de compromisos.

**Es importante notar que estos valores representan los compromisos poseídos**, y no por ejemplo, los depósitos. Información adicional disponible en la sección de [compromisos](../protocol/commitments.md) de estos documentos.

## Cómo hacer retiros {#how-to-make-withdrawals}
Desde la página de los activos de Nightfall, haga clic en el botón `Withdraw` a la derecha del activo elegido, o navegue a la página del puente L2.

1. Revise que el modo de transferencia esté configurado en `Withdraw`
2. Revise que el token deseado esté seleccionado (WETH, MATIC, etc.)
3. Ingrese el valor que se retirará de su billetera Nightfall, haga clic en `Transfer`
4. Revise la transacción en la ventana emergente
5. Haga clic en `Create Transaction`

Iniciará un proceso para calcular el ZKP y preparar la transacción. Cuando esto termine, haga clic en `Send Transaction`.

Vaya a la página de transacciones para [ver su depósito](#view-transactions). Después de que expira el período de finalización de una semana, el usuario
podrá finalizar y reclamar el monto retirado.

### Información importante sobre los retiros {#important-information-about-withdrawals}
- El valor a retirar debe igualar exactamente el monto en uno de los compromisos poseídos (más información sobre los [compromisos](#learn-about-commitments))
- Los retiros tienen un período de finalización de **una semana** desde el momento en que se creó el bloque incluyendo la transacción de retiro. Una vez transcurrido este período de tiempo, puedes finalizar el retiro para que tus fondos sean enviados a tu cuenta Ethereum.
- [Los montos a retirar están restringidos](#note-the-following-deposit-and-withdrawal-restrictions) mientras se está en la versión Beta
- Los retiros son una transacción en cadena, y pagarán por las tarifas de gas durante la solicitud de la transacción y también cuando se finaliza el retiro.

![](../imgs/tools-wallet/cooling-off-vs-ready.png)

## Ver las transacciones {#view-transactions}
Revise el estado de sus depósitos, transferencias y retiros en la página de las transacciones. Nota: Cada transacción se procesa tan pronto como haya suficientes transacciones para producir un bloque o después de 6 horas.

![](../imgs/tools-wallet/transactions.png)
