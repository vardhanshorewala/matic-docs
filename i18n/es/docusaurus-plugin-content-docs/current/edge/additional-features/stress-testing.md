---
id: stress-testing
title: Pruebas de estrés de la red
description: Cómo realizar una prueba de estrés utilizando el robot de carga. de Polygon Edge.
keywords:
  - docs
  - polygon
  - edge
  - loadbot
  - stress
  - test
---

## Prerrequisitos {#prerequisites}

Esta guía asume que:

- Tienes una red Polygon Edge funcionando y ejecutando
- Ambas de tus terminales JSON-RPC y GRPC son alcanzables

## Resumen {#overview}

El robot de carga de Polygon Edge es una utilidad de ayuda que está destinada a probar el estrés de una red de Polygon Edge.

Actualmente, esta soporta 2 modos:

- `transfer` - modo que realiza pruebas de estrés utilizando transacciones de transferencia de fondos. **[Por defecto]**.
- `deploy` - modo que implementa contratos inteligentes específicos con cada transacción.

### Modo de transferir {#transfer-mode}

El modo de transferir asume que hay una cuenta de remitente que tiene fondos iniciales para realizar la ejecución del robot de carga.

la dirección de la cuenta del remitente y la clave privada deben establecerse en las variables del entorno:

```bash
# Example
export LOADBOT_0x9A2E59d06899a383ef47C1Ec265317986D026055=154c4bc0cca942d8a0b49ece04d95c872d8f53d34b8f2ac76253a3700e4f1151
```

### Modo Implementar  {#deploy-mode}

El modo de implementación lleva a cabo la implementación del contrato con cada nueva transacción en la ejecución del robot de carga. El contrato que se está implementando se puede especificar usando
 [indicadores específicos](/docs/edge/get-started/cli-commands#loadbot-flags), o si se omite la ruta del contrato, por defecto
`Greeter.sol`  [el contrato](https://github.com/nomiclabs/hardhat/blob/master/packages/hardhat-core/sample-projects/basic/contracts/Greeter.sol) en cambio, se utiliza.

### Terminología {#terminology}

Esta sección cubre alguna terminología básica con respecto a la configuración del robot de carga.

- **calcular** -el número de transacciones que se enviarán en el modo especificado
- **tps** - El número de transacciones que deben enviarse al nodo por segundo

## Iniciar el robot de carga {#start-the-loadbot}

Como un ejemplo, aquí hay un comando válido que puedes utilizar para ejecutar el robot de carga utilizando dos cuentas preacuñadas:
```bash
polygon-edge loadbot  --jsonrpc http://127.0.0.1:10002 --grpc-address 127.0.0.1:10000 --sender 0x9A2E59d06899a383ef47C1Ec265317986D026055 --count 2000 --value 0x100 --tps 100
```

Deberías obtener un resultado similar a esto en tu terminal:
```bash
=====[LOADBOT RUN]=====

[COUNT DATA]
Transactions submitted = 2000
Transactions failed    = 0

[TURN AROUND DATA]
Average transaction turn around = 3.490800s
Fastest transaction turn around = 2.002320s
Slowest transaction turn around = 5.006770s
Total loadbot execution time    = 24.009350s

[BLOCK DATA]
Blocks required = 11

Block #223 = 120 txns
Block #224 = 203 txns
Block #225 = 203 txns
Block #226 = 202 txns
Block #227 = 201 txns
Block #228 = 199 txns
Block #229 = 200 txns
Block #230 = 199 txns
Block #231 = 201 txns
Block #232 = 200 txns
Block #233 = 72 txns
```
