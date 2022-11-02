---
id: heimdall-chain
title: ¿Qué es la cadena Heimdall?
sidebar_label: Heimdall Chain
description: Desarrolla tu próxima app de cadena de bloques en Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
Heimdall es la capa de prueba de participación verificadora de Polygon, responsable de comprobar una representación de los bloques de Plasma a la cadena principal, dentro de nuestra arquitectura. Hemos implementado esto a partir de la construcción por encima del motor de consenso Tendermint, con cambios en el esquema de firma y en diversas estructuras de datos.

El contrato de administración de participación de la cadena principal funciona en forma conjunta con el nodo Heimdall, para desempeñarse como el mecanismo de administración trust-less (sin intermediarios) para el motor de la PoS, que incluye el conjunto validador, la actualización de validadores, etcétera. Dado que el apilamiento se realiza, en realidad, en el contrato inteligente de Ethereum, no nos basamos solo en la honestidad de un validador, sino que heredamos la seguridad de la cadena de Ethereum para esta parte clave.

La capa Heimdall gestiona la agregación de bloques que produce Bor dentro de un árbol de Merkle y publica la raíz Merkle de forma periódica en la cadena raíz. Estas publicaciones periódicas se denominan “puntos de verificación”. Por cada algunos bloques en Bor, un validador (en la capa Heimdall) realiza lo siguiente:

1. valida todos los bloques desde el último punto de verificación;
2. crea un árbol de Merkle de los hashes de los bloques;
3. publica la raíz de Merkle en la cadena principal.

Los puntos de verificación son importantes por dos razones:

1. le proporcionan una finalización a la cadena raíz;
2. proporcionan prueba de quemado en el retiro de activos

Una vista “desde arriba” del proceso se puede explicar de la siguiente manera:

- se selecciona un subconjunto de validadores activos del grupo para que funcionen como productores de bloques para un span. La selección de cada span también tendrá el consentimiento de al menos dos tercios de los que los posean. Estos productores de bloques son responsables de crear bloques y transmitirlos al resto de la red.
- Un punto de verificación incluye la raíz de todos los bloques que se crearon durante un determinado intervalo. Todos los nodos validan el mismo y le adjuntan su firma.
- Un proponente de bloques seleccionado del conjunto de validadores es responsable de recopilar todas las firmas para un punto de verificación en particular y de remitir lo mismo en la cadena principal.
- La responsabilidad de crear bloques y también de proponer puntos de verificación depende, de forma variable, de la tasa de participación de un validador dentro del grupo general.