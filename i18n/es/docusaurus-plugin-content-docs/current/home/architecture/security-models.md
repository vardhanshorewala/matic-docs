---
id: security-models
title: Modelos de seguridad
description: "Valores PoS, Plasma e híbridos."
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Matic proporciona tres tipos de modelos de seguridad para que un desarrollador construya su aplicación descentralizada en:

1. [Prueba de participación seguridad](#proof-of-stake-security)
2. [Seguridad de plasma](#plasma-security)
3. [Híbrido (Plasma + PoS)](#hybrid)

Lo que sigue es una descripción de cada uno de estos modelos de seguridad que ofrece Polygon, y cuál sería el flujo de trabajo de los desarrolladores con un ejemplo de aplicación descentralizada (DApp).

### Prueba de participación seguridad {#proof-of-stake-security}

La prueba de seguridad de participación es proporcionada por la capa Heimdall & Bor, que está construida encima de Tendermint, Un punto de verificación se compromete a la cadena raíz, solo cuando los dos tercios de los validadores han firmado en él.

Para habilitar el mecanismo PoS en nuestra plataforma, utilizamos un conjunto de contratos de administración de participación de apuestas en Ethereum, así como un conjunto de validadores incentivados que ejecutan nodos Heimdall y Bor. Estos implementan las siguientes características:

- La capacidad de que cualquiera pueda apostar fichas MATIC en el contrato inteligente de Ethereum, y unirse al sistema como validador.
- Gana recompensas de apuesta por validar transiciones de estado en Polygon.
- Habilita las penalizaciones/recortes para actividades como la firma doble, el tiempo de inactividad de los validadores, etc.

El mecanismo PoS también actúa como una mitigación del problema de falta de disponibilidad de datos para nuestras cadenas de distribución lateral en términos de Plasma.

Tenemos una capa de finalización rápida que termina periódicamente el estado de la cadena lateral a través de los puntos de verificación. La finalización rápida nos ayuda a cementar el estado de la cadena lateral. La cadena compatible con EVM tiene pocos validadores y un tiempo de bloqueo más rápido con un alto rendimiento. Elige la escalabilidad en los altos grados de descentralización. Heimdall se asegura de que el compromiso estatal final sea infalible y pase por un gran conjunto de validadores y, por lo tanto, una alta descentralización.

**Para los desarrolladores**

Como desarrollador de DApp, para basarse en la seguridad de PoS, el procedimiento es tan sencillo como llevar tu contrato inteligente y utilizarlo en Polygon. Esto es posible gracias a la arquitectura basada en cuentas que permite una cadena lateral compatible con EVM.



### Seguridad de Plasma {#plasma-security}

Polygon proporciona garantías de plasma con respecto a diversos escenarios de ataque. Los dos casos principales considerados son:

- El operador de cadena (o en Polygon, o en la capa Heimdall) está dañado.
- El usuario está dañado

En ambos casos, si los activos de un usuario en la cadena de plasma se han visto comprometidos, necesitan comenzar a salir en masa. Polygon proporciona construcciones en el contrato inteligente de la cadena de raíces, que pueden ser aprovechadas. (Para más detalles y especificaciones técnicas con respecto a esta construcción y los vectores de ataque, consulta [aquí](https://ethresear.ch/t/account-based-plasma-morevp/5480)).

De forma efectiva, la seguridad que ofrece el Plasma de Polygon, contrata a los piggybacks sobre la seguridad de Ethereum. Los fondos de los usuarios solo corren riesgo si Ethereum falla. En pocas palabras, una cadena de plasma es tan segura como el mecanismo de consenso de la cadena principal. (Esto puede extrapolarse para decir que la cadena de plasma puede utilizar mecanismos de consenso realmente simples y aun así estar seguros).

**Para los desarrolladores**

Como desarrollador de DApp, si quieres construir en Polygon con la garantía de seguridad de Plasma, debes escribir predicados personalizados para tus contratos inteligentes. Lo que básicamente, significa escribir los contratos externos que manejan las condiciones de disputa establecidas por construcciones de plasma de Polygon.

### Híbrido {#hybrid}

Además de la seguridad pura de Plasma y la seguridad pura de prueba de participación en apuestas es posible que en DApps desplegada en Polygon, los desarrolladores pueden seguir, lo que simplemente significa contar con garantías de plasma y prueba de participación en algunos flujos de trabajo particulares de la DApp.

Este enfoque se entiende mejor con un ejemplo: Considere una DApp de juegos con un conjunto de contratos inteligentes que describen la lógica del juego. Supongamos que el juego utiliza su propia ficha erc20 para recompensar a los jugadores. Ahora, los contratos inteligentes que definen la lógica de juego se pueden desplegar directamente en la cadena lateral de Polygon, garantizando la seguridad de la prueba de participación de apuestas a los contratos, mientras que la transferencia de las fichas erc20 pueden estar aseguradas con garantías de Plasma y a prueba de fraude incrustada en los contratos de la cadena raíz.
