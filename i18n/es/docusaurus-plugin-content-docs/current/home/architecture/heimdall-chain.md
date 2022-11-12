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
Heimdall es la capa de prueba de participación verificadora de Polygon, responsable de comprobar una representación de los bloques de Plasma en la cadena principal, dentro de nuestra arquitectura. Hemos implementado esto a partir de la construcción por encima del motor de consenso Tendermint, con cambios en el esquema de firma y en diversas estructuras de datos.

El contrato del administrador de participación de la cadena principal funciona en forma conjunta con el nodo Heimdall, para desempeñarse como el mecanismo de administración de participación sin intermediarios para el motor de la prueba de participación (PoS), que incluye seleccionar el conjunto validador, la actualización de validadores, etc. Dado que el staking se realiza, en realidad, en el contrato inteligente de Ethereum, no nos basamos solo en la honestidad de un validador, sino que heredamos la seguridad de la cadena de Ethereum para esta parte clave.

La capa Heimdall gestiona la agregación de bloques que produce Bor dentro de un árbol de Merkle y publica la raíz Merkle de forma periódica en la cadena raíz. Estas publicaciones periódicas se denominan “puntos de verificación”. Después de algunos bloques en Bor, un validador (en la capa Heimdall) realiza lo siguiente:

1. Valida todos los bloques desde el último punto de verificación;
2. Crea un árbol de Merkle de los hashes de los bloques
3. Publica la raíz de Merkle en la cadena principal

Los puntos de verificación son importantes por dos razones:

1. Proporcionan una finalidad a la cadena raíz
2. Proporcionan prueba de quemado en la retirada de activos

Un panorama general del proceso se puede explicar de la siguiente manera:

- Se selecciona un subconjunto de validadores activos del grupo para que funcionen como productores de bloques para un span. La selección de cada span también tendrá el consentimiento de al menos dos tercios de los que tengan el control. Estos productores de bloques son responsables de crear bloques y transmitirlos al resto de la red.
- Un punto de verificación incluye la raíz de todos los bloques que se crearon durante un determinado intervalo. Todos los nodos validan el mismo y le adjuntan su firma.
- Un proponente de bloques seleccionado del conjunto de validadores es responsable de recopilar todas las firmas para un punto de verificación en particular y de remitir lo mismo en la cadena principal.
- La responsabilidad de crear bloques y también de proponer puntos de verificación depende, de forma variable, de la tasa de participación de un validador dentro del grupo general.