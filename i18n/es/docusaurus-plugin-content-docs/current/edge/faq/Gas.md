---
id: gas
title: Preguntas frecuentes Gas
description: "Preguntas frecuentes Gas para Polygon Edge"
keywords:
  - docs
  - polygon
  - edge
  - FAQ
  - validators

---

## ¿Cómo hacer cumplir un precio mínimo de gas? {#how-to-enforce-a-minimum-gas-price}
Puedes usar la bandera `--price-limit`proporcionada en el comando del servidor. Esto obligará a tu nodo a solo aceptar transacciones que tienen el precio más alto o igual al límite de precios que estableces. Para asegurarte de que se aplica en toda la red, necesitas asegurarte de que todos los nodos tengan el mismo límite de precios.


## ¿Puedes realizar transacciones con tarifas de gas 0? {#can-you-have-transactions-with-0-gas-fees}
Sí, puedes. El límite de precio por defecto que los nodos aplican es,`0` lo que significa que los nodos aceptarán transacciones que tienen precio de gas establecido a`0`.

## ¿Cómo establecer el suministro total del token de gas (nativo)? {#how-to-set-the-gas-native-token-total-supply}

Puedes establecer un saldo preminado a las cuentas (direcciones) usando la`--premine flag`. Nota que esta es una configuración del archivo de génesis, y más tarde. no se puede cambiar.

Ejemplo de cómo usar la`--premine flag`:

`--premine=0x3956E90e632AEbBF34DEB49b71c28A83Bc029862:1000000000000000000000`

Esto establece un saldo preminado de 1000 ETH a 0x3956E90e632AEbBF34DEB49b71c28A83Bc029862 (la cantidad del argumento está en wei).

La cantidad preminada del token de gas será del suministro total. Ninguna otra cantidad de moneda nativa de gas (token de gas) se puede acuñar más tarde.

## ¿Admite Edge ERC-20 como token de gas? {#does-edge-support-erc-20-as-a-gas-token}

Edge no admite token ERC-20 como token de gas Solo admite la moneda nativa de Edge para el gas.