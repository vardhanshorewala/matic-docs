---
id: versions
title: Historia
sidebar_label: History of changes
description: "Versiones desplegadas"
keywords:
  - docs
  - polygon
  - nightfall
  - changelog
image: https://matic.network/banners/matic-network-16x9.png
---


## Beta 1.0 {#beta-1-0}
Beta 1.0 fue lanzado el 17 de mayo de 2022. Este incluyó el mecanismo básico para tener una prueba de concepto desplegada de Nightfall.
Soportó un solo `Proposer` y primera `coarse` implementación de transacciones. También proporcionó una versión
preliminar de un usuario de billetera.
Versión desplegada que se puede encontrar [aquí](https://github.com/EYBlockchain/nightfall_3/commit/bc3e475de3e2877f14430f9599e5b38ea960765b)

## Beta 2.0 {#beta-2-0}
La versión desplegada se puede encontrar [aquí](https://github.com/EYBlockchain/nightfall_3/commit/4c2af01ac95af5ea6f5b40071d73a1624f06ba46)
Se han realizado varias mejoras:
- **Cobro de Tarifas**

Capacidad para que los proponentes cobren tarifas por las transacciones que recojan. Esta característica incentivará a múltiples proponentes.
- **Despliegue de desafiador**

La red ahora incluye un desafiador que monitorea los bloques de los proponentes.
- **Transacciones de Circuitos**

Mayor flexibilidad y mejor rendimiento al generar el ZKP de cualquier transacción.  Tanto `transfer` y `withdrawal` acepta hasta dos compromisos y devuelve cambio.
En cuanto al rendimiento, las transacciones ahora están optimizadas para que tomen menos tiempo las pruebas.

| Operaciones | Restricciones antes | Restricciones después |
|-----------|--------------------|------------------|
| Depositar | 84,766 | 1277 |
| Transferir | 499,119 | 67,694 |
| Retirar | 168,883 | 53,348 |

Parte de la optimización ha sido posible cambiando a Poseidon

- **Encriptación de secretos**

Hemos pasado desde El-Gamal a un proceso de encriptación [KEM-DEM](../protocol/secrets) que ha resultado en varios beneficios:
- Simplificación del proceso de encriptado/desencriptado
- Reducción de las restricciones y de los costos de gas en cadena.

- **Despliegue de desafiador**

