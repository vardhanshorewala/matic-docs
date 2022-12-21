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
El 17 de mayo de 2022 se lanzó Beta 1.0. Esta incluyó el mecanismo básico para tener desplegada la prueba de concepto de Nightfall.
Era compatible con una única `Proposer`y primera `coarse`implementación de transacciones. También proporcionó una versión
preliminar de una billetera de usuario.
La versión desplegada se puede encontrar [aquí](https://github.com/EYBlockchain/nightfall_3/commit/bc3e475de3e2877f14430f9599e5b38ea960765b)

## Beta 2.0 {#beta-2-0}
Encuentra la versión desplegada [aquí](https://github.com/EYBlockchain/nightfall_3/commit/4c2af01ac95af5ea6f5b40071d73a1624f06ba46)
Se han realizado varias mejoras:
- **Cobro de comisiones**

Capacidad para que los proponentes cobren comisiones por las transacciones que cobran. Esta característica incentivará múltiples proponentes.
- **Despliegue del desafiante**

La red ahora incluye a un desafiante que monitorea los bloques del proponente.
- **Transacciones de circuitos**

Más flexibilidad y mejor rendimiento al generar el ZKP de cualquier transacción. Ambas `transfer`y `withdrawal`aceptar hasta dos compromisos y devolver el cambio.
Con respecto al rendimiento, las transacciones ahora están optimizadas para que se requiera menor tiempo de prueba.

| Operaciones | Limitantes anteriores | Limitantes posteriores |
|-----------|--------------------|------------------|
| Depósito | 84.766 | 1.277 |
| Transferencia | 499.119 | 67.694 |
| Retiro | 168.883 | 53.348 |

Parte de la optimización es posible al cambiar a Poseidón.

- **Cifrado de secretos**

Pasamos de El-Gamal a un proceso de cifrado [KEM-DEM](../protocol/secrets), que ha dado como resultado varios beneficios:
- Simplificación del proceso de cifrado/descifrado
- Reducción de las limitantes y de los costos del gas en cadena.

- **Despliegue del desafiante**

