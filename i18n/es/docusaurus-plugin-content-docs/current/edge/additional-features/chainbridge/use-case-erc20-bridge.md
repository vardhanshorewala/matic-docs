---
id: use-case-erc20-bridge
title: Usa el caso Puente ERC-20
description: Ejemplo para el contrato del Puente ERC-20
keywords:
  - docs
  - polygon
  - edge
  - Bridge
  - ERC20
---

Esta sección tiene como objetivo proporcionarte un flujo de configuración del Puente ERC-20 para un uso práctico del caso.

En esta guía utilizarás la red de pruebas de Mumbai, de PoS de Polygon y de la cadena local de Polygon Edge. Asegúrate de que tienes un punto de extremo de JSON-RPC para Mumbai y que has configurado Polygon Edge en un ambiente local. Cosulte [Configuración Local](/docs/edge/get-started/set-up-ibft-locally) o [Configuración de Cloud](/docs/edge/get-started/set-up-ibft-on-the-cloud) para más detalles.

## Escenario {#scenario}

Este escenario es el de configurar un puente para el token ERC-20 que se ha desplegado en una cadena pública (Polygon Pos) con el fin de permitir la transferencia de bajo costo en una cadena privada (Polygon Edge) para los usuarios en un caso regular.
 En tal caso, el suministro total de tokens ha sido definido en la cadena pública y solo la cantidad del token la cual ha sido transferida desde la cadena pública a la cadena privada debe existir en la cadena privada. Por esa razón, necesitarás usar el modo de bloqueo/liberación en la cadena pública y el modo de quemar/acuñar en la cadena privada.

Al enviar tokens desde la cadena pública a la cadena privada, el token se bloqueará en el contrato de la cadena pública en el Manejador ERC-20 y la misma cantidad de tokens se acuñará en la cadena privada. Por otro lado, en caso de transferir desde la cadena privada a la cadena pública, el token en la cadena privada se quemará y la misma cantidad de tokens se liberará desde el contrato del Manejador ERC-20 en la cadena pública.

## Contratos {#contracts}

Explicando con un simple contrato ERC20 en lugar del contrato desarrollado por ChainBridge. Para el modo quemar/acuñar, el contrato ERC20 debe tener`mint` y `burnFrom`de otros métodos además de los métodos para ERC20 como este:

```sol
pragma solidity ^0.8.14;

import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
import "@openzeppelin/contracts/access/AccessControl.sol";

contract SampleToken is ERC20, AccessControl {
    bytes32 public constant MINTER_ROLE = keccak256("MINTER_ROLE");
    bytes32 public constant BURNER_ROLE = keccak256("BURNER_ROLE");

    constructor(string memory name, string memory symbol) ERC20(name, symbol) {
        _setupRole(DEFAULT_ADMIN_ROLE, _msgSender());
        _setupRole(MINTER_ROLE, _msgSender());
        _setupRole(BURNER_ROLE, _msgSender());
    }

    function mint(address recipient, uint256 amount)
        external
        onlyRole(MINTER_ROLE)
    {
        _mint(recipient, amount);
    }

    function burnFrom(address owner, uint256 amount)
        external
        onlyRole(BURNER_ROLE)
    {
        _burn(owner, amount);
    }
}
```

Todos los códigos y scripts están en el repositorio de Github [Trapesys/chainbridge-como ejemplo](https://github.com/Trapesys/chainbridge-example).

## Paso 1: Desplegar puente y contratos de manejador ERC-20 {#step1-deploy-bridge-and-erc20-handler-contracts}

En primer lugar, desplegar contratos puente y de manejador ERC20 usando`cb-sol-cli` en ambas cadenas.

```bash
# Deploy Bridge and ERC20 contracts in Polygon PoS chain
$ cb-sol-cli deploy --bridge --erc20Handler --chainId 99 \
  --url https://rpc-mumbai.matic.today \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --gasPrice [GAS_PRICE] \
  --relayers [RELAYER_ACCOUNT_ADDRESS] \
  --relayerThreshold 1
```

```bash
# Deploy Bridge and ERC20 contracts in Polygon Edge chain
$ cb-sol-cli deploy --bridge --erc20Handler --chainId 100 \
  --url http://localhost:10002 \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --relayers [RELAYER_ACCOUNT_ADDRESS] \
  --relayerThreshold 1
```

Obtendrás las direcciones de los contratos puente y de manejador ERC20 como esto:

```bash
Deploying contracts...
✓ Bridge contract deployed
✓ ERC20Handler contract deployed

================================================================
Url:        https://rpc-mumbai.matic.today
Deployer:   <ADMIN_ACCOUNT_ADDRESS>
Gas Limit:   8000000
Gas Price:   20000000
Deploy Cost: 0.00029065308

Options
=======
Chain Id:    <CHAIN_ID>
Threshold:   <RELAYER_THRESHOLD>
Relayers:    <RELAYER_ACCOUNT_ADDRESS>
Bridge Fee:  0
Expiry:      100

Contract Addresses
================================================================
Bridge:             <BRIDGE_CONTRACT_ADDRESS>
----------------------------------------------------------------
Erc20 Handler:      <ERC20_HANDLER_CONTRACT_ADDRESS>
----------------------------------------------------------------
Erc721 Handler:     Not Deployed
----------------------------------------------------------------
Generic Handler:    Not Deployed
----------------------------------------------------------------
Erc20:              Not Deployed
----------------------------------------------------------------
Erc721:             Not Deployed
----------------------------------------------------------------
Centrifuge Asset:   Not Deployed
----------------------------------------------------------------
WETC:               Not Deployed
================================================================
```

## Paso 2: Desplegar tu contrato ERC-20 {#step2-deploy-your-erc20-contract}

tú desplegarás tu contrato ERC-20. Este ejemplo te guía con el proyecto hardhat [ejemplo Trapesys/chainbridge](https://github.com/Trapesys/chainbridge-example).

```bash
$ git clone https://github.com/Trapesys/chainbridge-example.git
$ cd chainbridge-example
$ npm i
```

Crea `.env`un archivo y establece los siguientes valores.

```.env
PRIVATE_KEYS=0x...
MUMBAI_JSONRPC_URL=https://rpc-mumbai.matic.today
EDGE_JSONRPC_URL=http://localhost:10002
```

A continuación, desplegarás un contrato ERC-20 en las dos cadenas.

```bash
$ npx hardhat deploy --contract erc20 --name <ERC20_TOKEN_NAME> --symbol <ERC20_TOKEN_SYMBOL> --network mumbai
```

```bash
$ npx hardhat deploy --contract erc20 --name <ERC20_TOKEN_NAME> --symbol <ERC20_TOKEN_SYMBOL> --network edge
```

Después de que la implementación sea exitosa, obtendrás una dirección de contrato como esta:

```bash
ERC20 contract has been deployed
Address: <ERC20_CONTRACT_ADDRESS>
Name: <ERC20_TOKEN_NAME>
Symbol: <ERC20_TOKEN_SYMBOL>
```

## Paso 3: Registrar identificación de recurso en el puente {#step3-register-resource-id-in-bridge}

Registrarás una identificación de recurso que asocia el recurso en un entorno de cadena cruzada. Necesitas establecer el mismo recurso de identificación en ambas cadenas.

```bash
$ cb-sol-cli bridge register-resource \
  --url https://rpc-mumbai.matic.today \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --gasPrice [GAS_PRICE] \
  --resourceId "0x000000000000000000000000000000c76ebe4a02bbc34786d860b355f5a5ce00" \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --handler "[ERC20_HANDLER_CONTRACT_ADDRESS]" \
  --targetContract "[ERC20_CONTRACT_ADDRESS]"
```

```bash
$ cb-sol-cli bridge register-resource \
  --url http://localhost:10002 \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --resourceId "0x000000000000000000000000000000c76ebe4a02bbc34786d860b355f5a5ce00" \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --handler "[ERC20_HANDLER_CONTRACT_ADDRESS]" \
  --targetContract "[ERC20_CONTRACT_ADDRESS]"
```

## Paso 4: establece el modo de Quemar/Acuñar en el puente ERC-20 del Edge {#step4-set-mint-burn-mode-in-erc20-bridge-of-the-edge}

El puente espera funcionar como modo de quemar/acuñar en Polygon Edge. Configurará el modo quemar/acuñar usando`cb-sol-cli`.

```bash
$ cb-sol-cli bridge set-burn \
  --url http://localhost:10002 \
  --privateKey [ADMIN_ACCOUNT_PRIVATE_KEY] \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --handler "[ERC20_HANDLER_CONTRACT_ADDRESS]" \
  --tokenContract "[ERC20_CONTRACT_ADDRESS]"
```

Y necesitarás otorgar un papel de acuñador y quemador al contrato de manejador ERC-20

```bash
$ npx hardhat grant --role mint --contract [ERC20_CONTRACT_ADDRESS] --address [ERC20_HANDLER_CONTRACT_ADDRESS] --network edge
$ npx hardhat grant --role burn --contract [ERC20_CONTRACT_ADDRESS] --address [ERC20_HANDLER_CONTRACT_ADDRESS] --network edge
```

## Paso 5: Acuñar Token  {#step5-mint-token}

Tú acuñarás nuevos tokens ERC-20 en la cadena de Mumbai.

```bash
$ npx hardhat mint --type erc20 --contract [ERC20_CONTRACT_ADDRESS] --address [ACCOUNT_ADDRESS] --amount 100000000000000000000 --network mumbai # 100 Token
```

Después de que la transacción haya sido exitosa, la cuenta tendrá el token acuñado.

## Paso 6: Iniciar transferencia ERC-20  {#step6-start-erc20-transfer}

Antes de iniciar este paso por favor asegúrate de que has iniciado un repetidor. Revisar [Configuración](/docs/edge/additional-features/chainbridge/setup) para más detalles.

Durante la transferencia de tokens desde Mumbai a Edge, al contrato de manejador ERC-20 en Mumbai retira los tokens de tu cuenta. Llamarás a aprobación antes de la transferencia.

```bash
$ npx hardhat approve --type erc20 --contract [ERC20_CONTRACT_ADDRESS] --address [ERC20_HANDLER_CONTRACT_ADDRESS] --amount 10000000000000000000 --network mumbai # 10 Token
```

Finalmente, iniciarás la transferencia de tokens desde Mumbai a Edge usando`cb-sol-cli`.

```bash
# Start transfer from Mumbai to Polygon Edge chain
$ cb-sol-cli erc20 deposit \
  --url https://rpc-mumbai.matic.today \
  --privateKey [PRIVATE_KEY] \
  --gasPrice [GAS_PRICE] \
  --amount 10 \
  # ChainID of Polygon Edge chain
  --dest 100 \
  --bridge "[BRIDGE_CONTRACT_ADDRESS]" \
  --recipient "[RECIPIENT_ADDRESS_IN_POLYGON_EDGE_CHAIN]" \
  --resourceId "0x000000000000000000000000000000c76ebe4a02bbc34786d860b355f5a5ce00"
```

Después de la transacción exitosa del depósito, el repetidor obtendrá el evento y votará por la propuesta. Eso ejecuta la transacción de enviar tokens a la cuenta del destinatario en la cadena Polygon Edge después de que el número requerido de votos sean presentados.

```bash
INFO[11-19|08:15:58] Handling fungible deposit event          chain=mumbai dest=100 nonce=1
INFO[11-19|08:15:59] Attempting to resolve message            chain=polygon-edge type=FungibleTransfer src=99 dst=100 nonce=1 rId=000000000000000000000000000000c76ebe4a02bbc34786d860b355f5a5ce00
INFO[11-19|08:15:59] Creating erc20 proposal                  chain=polygon-edge src=99 nonce=1
INFO[11-19|08:15:59] Watching for finalization event          chain=polygon-edge src=99 nonce=1
INFO[11-19|08:15:59] Submitted proposal vote                  chain=polygon-edge tx=0x67a97849951cdf0480e24a95f59adc65ae75da23d00b4ab22e917a2ad2fa940d src=99 depositNonce=1 gasPrice=1
INFO[11-19|08:16:24] Submitted proposal execution             chain=polygon-edge tx=0x63615a775a55fcb00676a40e3c9025eeefec94d0c32ee14548891b71f8d1aad1 src=99 dst=100 nonce=1 gasPrice=5
```

Una vez que la ejecución de la transacción haya sido exitosa, obtendrás tokens en la cadena Polygon Edge.
