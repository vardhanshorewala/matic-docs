---
id: overview
title: Descripción general
sidebar_label: Overview
description: Una descripción general de lo que es Nightfall
keywords:
  - docs
  - polygon
  - nightfall
  - privacy
  - rollup
  - zk
image: https://matic.network/banners/matic-network-16x9.png
---

Polygon cree en una visión que ve muchas empresas en un futuro cercano interactuando entre si
a través de contratos inteligente para ejecutar la lógica de negocio y gestionar el intercambio de bienes y servicios.

En colaboración con [Ernst & Young](https://blockchain.ey.com/), Polygon ofrece una solución rollup pública de capa 2 enfocada en la privacidad llamada Polygon Nightfall para habilitar la accesibilidad y la privacidad de las empresas que desean
usar Ethereum.

## Un protocolo a prueba de conocimiento cero para las empresas {#a-zk-proof-protocol-for-enterprises}

Polygon Nightfall es parte del paquete de las soluciones de escalabilidad de Polygon, que incluyen
[Polygon Hermez](https://polygon.technology/solutions/polygon-hermez/),
[Polygon Miden](https://polygon.technology/solutions/polygon-miden/)
y [Polygon Zero](https://polygon.technology/solutions/polygon-zero/).
La diferencia clave es que Nightfall es un rollup enfocado en la privacidad diseñado para los casos de uso de las empresas al combinar
los conceptos de rollups optimistas y criptografía de conocimiento cero (ZK) para ofrecer transacciones privadas y escalables.

Mientras que Nightfall habilita la escalabilidad, también está configurado para eliminar una barrera importante que las empresas enfrentan hoy
cuando utilizan cadena de bloques: la falta de privacidad de las transacciones. Nightfall añade una capa de privacidad para que los parámetros clave de transacción (por ejemplo, valor y destino) no sean rastreables. Estas dos características han alimentado el interés de las empresas privadas que ven a Nightfall como una manera de ejecutar su lógica de negocio y coordinar con su cadena de suministro en una red descentralizada a un precio sostenible, todo mientras se mantiene la seguridad y la privacidad.

## Los pilares de Nightfall {#nightfall-s-pillars}

La propuesta de valor principal de Polygon Nightfall es habilitar las transferencias de datos seguras, privadas y de bajo costo
en una red descentralizada.

![](../imgs/overview.png)

## Privacidad {#privacy}

Polygon Nightfall utiliza las pruebas de conocimiento cero para enviar transacciones privadas. Un usuario puede generar una prueba de conocimiento cero de
la transacción sin revelar los parámetros clave de la transacción como el destino o el valor de
la transacción. Más detalles sobre el componente de privacidad de Nightfall están disponibles en la
guía de [protocolo](../protocol/protocol.md).

## Seguridad {#security}

> Actualmente, Nightfall está bajo auditoría de seguridad, y se espera terminar aproximadamente a mediados de junio del 2022.
> Una vez que el proceso de auditoría se haya completado, los resultados se publicarán aquí.

> Al ser una red nueva en período de arranque, Nightfall tiene medidas de seguridad transitorias para
> proteger el sistema con el objetivo de eliminarlos y dejarlo completamente descentralizado.

Polygon Nightfall es una construcción de capa 2 porque aprovecha a Ethereum al tomar prestada su seguridad como una
robusta cadena de bloques pública. Nightfall depende de ciertas suposiciones que garantizan la recuperación del activo. Estas suposiciones están
basadas en varias decisiones de diseño y arquitectura que giran alrededor de ZK-SNARKS, que utilizan
ciertas criptográficas primitivas, como hashes y firmas.
Por último, Nightfall embebe reglas operativas en diferentes contratos inteligentes para garantizar que los operadores no bloqueen
las transacciones de los usuarios y que estos puedan retirar sus activos en todo momento.

En resumen, Nightfall realiza las siguientes suposiciones de seguridad:

1. Suposiciones de seguridad de Ethereum
2. Supuestos de Groth16 (suposición de conocimiento del exponente).
3. Ciertas suposiciones criptográficas de primitivos como hashes (Poseidón) y firmas.
4. Supuestos de seguridad de software que dependen del diseño e implementación correctos.

## Eficiencia {#efficiency}

Los proponentes de bloque recopilan transacciones de varios usuarios y los agrupan en un bloque de L2.
Los tamaños de bloque L2 típicos contienen cerca de 32 transacciones.

Los costos de gas previstos para un depósito, transferencia y retiro son 9.000, 1.200 y 9.500. Este costo se debe al almacenamiento de 574 bytes de datos de llamada por transacción, más algunos datos de llamadas fijos y la computación para procesar un bloque L2. Los costos serán hasta un 80 % más bajos después de
[EIP 4488](https://eips.ethereum.org/EIPS/eip-4488).

## Transferencias no denegables {#non-deniable-transfers}

Como parte de la prueba de conocimiento cero de la transacción de transferencia, Nightfall incluye el cifrado de los secretos (dirección del token,
valor, Id., y sal) requeridos para procesar el compromiso transferido. Esto obliga al usuario a cifrar los secretos
con una clave conocida por el destinatario. Como la clave es parte de la prueba de conocimiento cero, el receptor se basa en la denegación plausible
ya que el remitente puede probar que se utilizó la clave de cifrado correcta.

## Descentralización {#decentralization}

Los validadores y [los desafiantes](docs/nightfall/protocol/actors) son una parte integral de Nightfall. Se aseguran de que
las transacciones y los bloques L2 produzcan de manera oportuna y correcta. Un mecanismo de consenso basado en prueba de participación (PoS) es
utilizado para seleccionar el [proponente](docs/nightfall/protocol/actors) siguiente de la red. Por otro lado, los desafiantes monitorean
el funcionamiento correcto de la red al plantear los desafíos cuando se detecta un bloque incorrecto y al retener la
participación avanzada por el proponente.


## Prueba de futuro {#future-proof}
Gracias a la flexibilidad proporcionada por la implementación rollup optimista de Nightfall, es posible incluir nuevas transacciones
en el futuro sin comprometer las transacciones existentes al solo definir y registrar un nuevo tipo de circuito que implementó la
transacción en conocimiento cero.

## Referencias {#references}

1. [Un enfoque multilateral para la escalabilidad ZK](https://messari.io/article/polygon-a-multi-sided-approach-to-zk-scaling)
2. [La opinión de Paul Brody sobre Nightfall](https://www.linkedin.com/pulse/say-hello-nightfall-paul-brody-1f/)
