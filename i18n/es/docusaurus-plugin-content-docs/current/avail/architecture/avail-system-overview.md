---
id: avail-system-overview
title: Resumen del Sistema
sidebar_label: System Overview
description: Obtén información sobre la arquitectura de la cadena Avail
keywords:
  - docs
  - polygon
  - avail
  - data
  - availability
  - architecture
image: https://matic.network/banners/matic-network-16x9.png
slug: avail-system-overview
---

## Modularidad {#modularity}

Actualmente, las arquitecturas monolíticas de las cadenas de bloques como Ethereum no pueden manejar eficientemente la ejecución, solución y disponibilidad de datos.

El modularizar la ejecución de escalar las cadenas de bloques son en lo que se centra la acumulación. los modelos de cadena intentan hacerlo. Esto puede funcionar bien cuando asentamiento y las capas de disponibilidad de datos se encuentran en la misma capa en la que está el acercamiento. que Los rollups de Ethereum. toman Aun así, hay compensaciones necesarias al trabajar con los rollups, ya que la construcción del rollup puede ser más segura dependiendo de la seguridad de los datos disponibles en la capa desafiante de escalar.

Sin embargo, un diseño granular crea diferentes capas para ser ligera protocolos, como los microservicios. Entonces, la red general se convierte en una colección de protocolos ligeros débilmente acoplados. Un ejemplo es la disponibilidad de datos de capa que solo se especializa en la disponibilidad de datos. Avail Polygon es una capa de cadena de bloques de dos basadas en sustratos de (DA disponibilidad de datos).

:::note Tiempo de ejecución

Aunque Avail se basa en el código base de Substrate, esta incluye modificaciones en la estructura de bloques que evitan que interopere con otras redes Substrate. --- Avail implementa una red independiente no relacionada con Polkadot o Kusama.

:::

Avail proporciona una alta garantía de disponibilidad de datos a cualquier cliente ligero, pero no da garantías más altas para clientes ligeros acerca de DA que cualquier otra red. Avail se enfoca en hacer posible probar que los datos de bloque son disponible sin descargar todo el bloque aprovechando el polinomio de Kate compromisos, codificación de borrado y otras tecnologías para permitir que los clientes ligeros descarguen solo los _encabezados_ de la cadena de manera eficiente y aleatoria
 muestra pequeñas cantidades de los datos de bloque para verificar su completa disponibilidad. Sin embargo, existen primitivos fundamentalmente diferentes de los que Sistemas DA basados en pruebas de fraude, que se explican [aquí](https://blog.polygon.technology/the-data-availability-problem-6b74b619ffcc/).

:::info Proporcionar disponibilidad de datos

La garantía de DA es algo que un cliente determina por sí mismo; no tiene que nodos de confianza. A medida que crece el número de clientes ligeros, muestran colectivamente todo el bloque (aunque cada cliente solo muestra un pequeño porcentaje). Los clientes ligeros eventualmente forman una red p2p entre ellos; por lo tanto, después de que un bloque ha sido muestreado, se convierte en altamente disponible, es decir, incluso si los nodos fueran a bajar (o intentar censurar un bloque), los clientes ligeros serían capaces de reconstruir el bloque al compartir las piezas entre ellos mismos

:::

### Habilitación del siguiente conjunto de soluciones {#enabling-the-next-set-of-solutions}

Avail llevará los rollups al siguiente nivel, que las cadenas pueden asignar su componente de disponibilidad de datos a Avail. Avail también proporciona una manera alternativa de arrancar cualquier cadena independiente, ya que las cadenas pueden descargar sus datos disponibilidad. Hay, por supuesto, los acuerdos que se hacen con diferentes enfoques, de modularidad, pero el objetivo general es mantener una alta seguridad mientras es capaz de escalar.

También se reducen los costos de la transacción. Avail puede cultivar el tamaño de bloque con un menor impacto en la carga de trabajo del validador que en una cadena monolítica. Cuando una cadena monolítica aumenta el tamaño de bloques, los validadores tienen que hacer mucho más trabajo porque los bloques tienen que ejecutar, y el estado tiene que ser calculado. Dado que Avail no tiene un entorno de ejecución, es mucho más barato para aumentar el tamaño de bloque. El costo no es cero debido a la necesidad de calcular los compromisos de KZG y generar pruebas, pero todavía de bajo costo.

Avail también hace que los rollups soberanos sean una posibilidad. Los usuarios pueden crear cadenas soberanas que confíen en los validadores de Avail, para llegar a un consenso sobre los datos de la transacción y el orden. Los rollups soberanos en Avail permiten actualizaciones sin problemas, ya que los usuarios pueden empujar las actualizaciones de nodos específicos de la aplicación para actualizar la cadena y, a su vez, actualizar a una nueva solución lógica. Mientras que, en un entorno tradicional, la red requiere una bifurcación

:::info Avail no tiene un entorno de ejecución

Avail no ejecuta contratos inteligentes, pero permite que otras cadenas realicen su transacción de datos disponibles a través de Avail. Estas cadenas pueden implementar sus entornos de ejecución de cualquier tipo, EVM, Wasm, o cualquier otra cosa.

:::

:::info A Avail no le importa para qué son los datos

Avail garantiza que los datos del bloque están disponibles, pero no se preocupa acerca de qué son esos datos. Los datos pueden ser transacciones, pero pueden tomarlos también en otras formas.

:::

La disponibilidad de datos en Avail están disponibles para una ventana de tiempo que sea requerida. Por ejemplo, más allá de necesitar datos o reconstrucción, la seguridad no es comprometida.

Los sistemas de almacenamiento, por otro lado, están diseñados para almacenar datos por largos periodos, e incluir mecanismos de incentivación para incentivar a los usuarios a almacenar datos.

## Validación {#validation}

### Validación de pares {#peer-validation}

Tres tipos de pares normalmente componen un ecosistema:

* **Nodos validadores:**
 Un validador recoge transacciones del mempool, las ejecuta y genera un bloque de candidatos que se adjunta a la red. El bloque contiene un bloque pequeño cabecera con la digestión y los metadatos de las transacciones en el bloque.
* **Nodos completos:**
 El bloque de candidatos se propaga a nodos completos en la red para su verificación. Los nodos volverán a ejecutar las transacciones contenidas en el bloque de candidatos.
* **Clientes ligeros**
 Los clientes ligeros solo obtienen el encabezado de bloque para utilizarlo para la verificación y se buscarán detalles de las transacciones de nodos vecinos completos según sea necesario.

Mientras con un enfoque seguro, Avail aborda las limitaciones de esta arquitectura para crear robustez y mayores garantías. Los clientes ligeros pueden ser engañados para que acepten bloques cuyos datos subyacentes no están disponibles. Un productor de bloques puede incluir una transacción maliciosa en un bloque y no revelar todo su contenido a la red. Como se mencionó en la documentación de Avail, esto se conoce como el problema de disponibilidad de datos.

Entre los pares de la red de Avail se incluyen:

* **Nodos validadores:**
 Protocolos incentivados de nodos completos que participan en el consenso. Nodos de validador en Avail no ejecutes transacciones. Ellos empaquetan transacciones arbitrarias y construyen bloques de candidatos, generando compromisos de KZG para los datos.
  > Otros validadores comprueban que los bloques generados sean correctos.

* **Avail (DA) nodos completos:**
 Nodos que descargan y ponen a disposición todos los datos de bloque para todas las aplicaciones utilizando Avail. Del mismo modo, los nodos completos de Avail no ejecutan las transacciones.

* **Avail (DA) clientes ligeros:**
 Los clientes que solo descargan cabeceras de bloque muestran aleatoriamente pequeñas partes de el bloque para verificar la disponibilidad. Exponen una API local para interactuar con la red. Avail

:::info El objetivo de Avail es no depender de los nodos completos para mantener los datos disponibles

El objetivo es dar garantías de DA similares a un cliente ligero como un nodo completo. Se anima a los usuarios a utilizar a los clientes ligeros de Avail. Sin embargo, todavía pueden ejecutar los nodos completos de Avail que están bien soportados.

:::

:::caution La API local es un WIP y aún no es estable


:::

Esto permite a las aplicaciones que deseen utilizar Avail para incrustar a los clientes ligeros de DA n/a Entonces pueden construir:

* **Nodos completos de la aplicación:**
  - Inserta un cliente ligero de la (DA) Avail
  - Descarga todos los datos de una ID de app específica
  - Implementa un entorno de ejecución para ejecutar transacciones
  - Mantén el estado de la aplicación

* **Clientes ligeros de la App:**
  - Inserta un cliente ligero de la (DA) Avail
  - Implementar la funcionalidad orientada al usuario final

El ecosistema de Avail también contará con puentes para habilitar específicos casos de uso. Uno de estos puentes que se está diseñando en este momento es un _puente de atestación_ que publicará atestaciones de datos disponibles en
 Avail con Ethereum, permitiendo así la creación de validiums.

## Verificación de Estado {#state-verification}

### Verificación de bloques -> Verificación de DA {#block-verification-da-verification}

#### Validadores {#validators}

En lugar de utilizar validadores de Avail que verifican el estado de la aplicación, estos concentran en garantizar la disponibilidad de los datos de transacciones publicados y proporcionar pedidos de transacciones n/a Un bloque solo se considera válido si los datos detrás de ese bloque están disponibles.

Los validadores de Avail asumen las transacciones entrantes, las ordenan, construyen un bloque de candidatos, y proponen a la red. El bloque contiene características especiales, especialmente para la eliminación de la codificación de DA: y de los compromisos de KZG. Esto está en un formato particular, para que los clientes puedan hacer Muestreos aleatorios y descargar solo las transacciones de una única aplicación. Otros validadores verifican el bloque asegurando que el bloque está bien formado, y de los compromisos de KZG comprobar que los datos están allí, etc.

#### Clientes {#clients}

La exigencia de datos que están disponibles evita que los productores de bloques liberen los encabezados de bloques sin liberar los datos detrás de ellos, ya que esto evita que los clientes lean las transacciones necesarias para calcular el estado de sus aplicaciones. Como con otras cadenas, Avail utiliza la verificación de la disponibilidad de datos para abordarlo a través de las verificaciones de DA que utilizan códigos de borrado; estos controles se utilizan fuertemente en el diseño de la redundancia de datos.

Los códigos de borrado duplican eficazmente los datos de modo que si parte de un bloque es Suprimido los clientes pueden reconstruir esa parte utilizando otra parte del bloque. Esto significa que un nodo que intenta ocultar esa parte tendría que ocultar mucho más.

> La técnica se utiliza en dispositivos como CD-ROM y matrices de discos múltiples (RAID) por ejemplo, sí un disco duro muere, puede ser reemplazado y reconstruido a partir de los datos de otros discos.

Lo que es único acerca de Avail es que el diseño de la cadena permite *a cualquiera* comprobar la DA sin necesitar descargar los datos. Las verificaciones de DA requieren que cada cliente ligero muestre un mínimo de número de trozos aleatorios de cada bloque de la cadena. Un conjunto de clientes ligeros puede colectivamente mostrar toda la cadena de bloques de esta manera. Por lo tanto, los nodos más no consensuados allí son los mayores sea que el tamaño del bloque (y el rendimiento) puedan existir de forma segura. Significado, sin consenso Los nodos pueden contribuir al rendimiento y a la seguridad de la red.

### Liquidación de transacciones {#transaction-settlement}

Avail utilizará una capa de liquidación construida con Polygon Edge. La capa de liquidación proporciona una cadena de bloques compatible con EVM para que los rollups almacenen sus datos y realicen resoluciones de disputas. La capa de liquidación que utiliza Polygon Avail para su DA. Cuando los rollups están utilizando una capa de liquidación, también heredan todos las propiedades de DA de Avail.

:::note Diferentes maneras de liquidar

Hay diferentes formas de utilizar Avail, y los validiums no utilizarán las capas de liquidaciones, pero más bien se conforman con Ethereum.

:::

Avail ofrece alojamiento de datos y pedidos. Es probable que la capa de ejecución provenga de las múltiples soluciones de escalado fuera de la cadena o capas de ejecución heredadas. n/a la capa de liquidación asume el componente de verificación y resolución de conflictos.

## Recursos {#resources}

- [Introducción a Avail por la publicación de Polygon](https://medium.com/the-polygon-blog/introducing-avail-by-polygon-a-robust-general-purpose-scalable-data-availability-layer-98bc9814c048).
- [Conversaciones de Polygon: Avail de Polygon](https://www.youtube.com/watch?v=okqMT1v3xi0)
