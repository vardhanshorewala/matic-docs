---
id: overview
title: Resumen
sidebar_label: Overview
description: Un resumen acerca de Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - privacy
  - rollup
  - zk
image: https://matic.network/banners/matic-network-16x9.png
---

Polygon cree en una visión que ve a muchas compañías en el futuro cercano interactuar con cada
uno a través de contratos Smart para ejecutar la lógica empresarial y administrar el intercambio de bienes y servicios.

En colaboración con [Ernst & Young](https://blockchain.ey.com/) Polygon ofrece una solución acumulativa de capa 2 pública y centrada en la privacidad llamada Polygon Nightfall para permitir la accesibilidad y la privacidad de las empresas que desean
usar Ethereum.

## Un protocolo de ZK-Proof para empresas {#a-zk-proof-protocol-for-enterprises}

Polygon Nightfall es parte del conjunto de soluciones de escalabilidad de Polygon que incluyen
[Polygon Hermez](https://polygon.technology/solutions/polygon-hermez/),
[Polygon Miden](https://polygon.technology/solutions/polygon-miden/)
y [Polygon Zero](https://polygon.technology/solutions/polygon-zero/).
La diferencia de la clave es que Nightfall es un rollup centrado en la privacidad diseñado para casos de uso para las empresas mediante la combinación de
los conceptos optimistas de los rollups y de la criptografía Zero-Knowledge (ZK) para ofrecer transacciones privada y escalables.

Mientras Nightfall permite escalabilidad, también se establece para eliminar una importante barrera que enfrentan las empresas hoy
cuando usan una cadena de bloques: como la falta de privacidad de las transacciones. Nightfall añade una capa de privacidad para que los parámetros de la clave de transacción (por ejemplo, valor y destinación) que no puedan rastrear. Estas dos características han alimentado el interés de las empresas privadas que ven a Nightfall como una manera de ejecutar su lógica de negocios y coordinar con su cadena de suministros en una red descentralizada a un precio sostenible, todo esto manteniendo la seguridad y la privacidad.

## Pilares de Nightfall {#nightfall-s-pillars}

La principal propuesta de valor de Polygon Nightfall es habilitar transferencias seguras y privadas de bajo costo de
datos en una red descentralizada.

![](../imgs/overview.png)

## Privacidad {#privacy}

Polygon Nightfall utiliza pruebas de ZK para enviar transacciones privadas. Donde un usuario puede generar una prueba de ZK de
la transacción sin revelar parámetros claves de la transacción como el destino o el valor de la
transacción. Más detalles sobre el componente de privacidad de Nightfall están disponibles en
[protocolo](../protocol/protocol.md) que encontrará en la guía.

## Seguridad {#security}

> Nightfall se encuentra actualmente en una auditoría de seguridad y se espera que finalice a mediados de junio de 2022.
> Una vez que el proceso de auditoría esté completo, los resultados se publicarán aquí.

> Como una nueva red con un periodo de arranque, Nightfall tiene medidas de seguridad transitorias para
> proteger el sistema con el objetivo de eliminarlos y dejarlo completamente descentralizados.

Polygon Nightfall es una construcción de capa 2 porque esta aprovecha Ethereum al tomar prestada su seguridad como una robusta
cadena de bloques pública. Nightfall confía en ciertos supuestos que garantizan la recuperación del activo. Estas suposiciones están
basadas en varias decisiones de diseño y de arquitectura que giran en torno a ZK-SNARKS, que utilizan
ciertos criptográficos, primitivos como los hashes y las firmas.
Por último, Nightfall incrusta las reglas de operación en diferentes contratos Smart para garantizar que los operadores no bloqueen
las transacciones del usuario y que los usuarios retiren sus activos en todo momento.

Como un resumen, Nightfall realiza las siguientes suposiciones de seguridad:

1. Suposiciones de seguridad Ethereum.
2. Suposiciones de Groth16 (conocimiento de la suposición exponente).
3. Ciertas suposiciones criptográficas desde primitivos como los hashes (Poseidon) y las firmas.
4. Suposiciones de seguridad del software que dependen en los diseños e implementaciones correctas.

## Eficiencia {#efficiency}

Los proponentes de bloques recopilan las transacciones de varios usuarios y agrupan dentro de un bloque L2.
Los tamaños típicos de los bloques L2 contienen alrededor de 32 transacciones.

Los costos esperados del gas para un depósito transferencia y retiro son 9000, 1200 y 9500. Este costo es debido a que almacena 574 Bytes de datos de llamadas por transacción y algunos extras
como datos de llamadas y computación fijos para procesar un bloque L2. Los costos serán hasta de un 80 % menores después
[EIP 4488](https://eips.ethereum.org/EIPS/eip-4488).

## Transferencias no negables {#non-deniable-transfers}

Como parte de la prueba ZK de transferir transacciones, Nightfall incluye encriptar los secretos (como las direcciones de los tokens,
valores, identificaciones y sal) requeridos para procesar el compromiso transferido. Esto obliga al usuario a encriptar los secretos
con una clave conocida por el destinatario. Como la clave es parte de la prueba ZK, el receptor depende de la negación plausible
como el emisor puede probar que se utiliza la clave de encriptación correcta.

## Descentralización {#decentralization}

Validadores y [Desafiadores](docs/nightfall/protocol/actors) son una parte integral de Nightfall. Ellos aseguran que
las transacciones y los bloques L2 producen de forma oportuna y correcta. Una prueba de Participación (POS) basada en un mecanismo de consenso es
usada para seleccionar al siguiente [Proponente](docs/nightfall/protocol/actors) de la red. Por otro lado, los Challengers (Desafiadores) monitorean
el funcionamiento correcto de la red al elevar los desafíos cuando se detecta un bloque incorrecto y mantengan la
participación avanzada por el proponente.


## Prueba de Futuro {#future-proof}
Gracias a la flexibilidad proporcionada por la optimista implementación de rollups de Nightfall, es posible incluir nuevas transacciones
en el futuro sin comprometer las transacciones existentes al simplemente definir y registrar un nuevo tipo de circuito que implementó la
transacción en ZK.

## Referencias {#references}

1. [Un enfoque multifacético para escalar ZK](https://messari.io/article/polygon-a-multi-sided-approach-to-zk-scaling)
2. [La vista de Paul Brody en Nightfall](https://www.linkedin.com/pulse/say-hello-nightfall-paul-brody-1f/)
