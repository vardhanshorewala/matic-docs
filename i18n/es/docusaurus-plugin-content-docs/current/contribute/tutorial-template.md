---
id: tutorial-template
title: Plantilla general de tutoriales
sidebar_label: Tutorial template
description: Sigue la plantilla de tutoriales cuando escribas un tutorial técnico.
keywords:
  - docs
  - matic
  - polygon
  - documentation
  - tutorial
  - contribute
  - template
image: https://wiki.polygon.technology/img/polygon-wiki.png
slug: tutorial-template
---

Debes usar esta plantilla para contribuir a Polygon Wiki
con un tutorial. Puedes contribuir con un tutorial sobre un tema de tu elección.

## Directrices generales {#general-guidelines}

* El alcance del tutorial debe quedar claro desde el título.
* El tutorial debe describir las características y funcionalidades
de los productos o servicios con precision.
* Trata de hacer el tutorial breve y conciso, pero amplia los conceptos clave
cuando sea apropiado. Proporciona información de fondo y contexto adicional cuando sea posible.
* Los pasos de configuración e implementación deben ser bien específicos.
* Haz el esfuerzo de incluir imágenes, íconos o capturas de pantalla
que complementen el contenido escrito.
  > El equipo de documentación felizmente trabajará contigo en la creación de diagramas.
* Recuerda el público para el que estás escribiendo. Si el material tiene cierto nivel de dificultad,
debes mencionar eso en el tutorial.
  > Si hay pasos que el usuario debe dar antes de implementar el tutorial, menciónalos.
* El equipo de documentación estará encantado de trabajar conjuntamente en la creación del tutorial.
* Ten presente la **[guía de estilo](writing-style.md)**.

:::caution Actualización de tutoriales actuales

Si te das cuenta de que los tutoriales actuales en Polygon Wiki
no siguen esta plantilla, es porque el equipo de documentación
decidió implementar un estándar, por lo que el flujo del tutorial es consistente
en todos los tutoriales. El equipo está trabajando para actualizar estos tutoriales,
de modo tal que se asemejen a esta plantilla. Si te interesa, también puedes actualizar
un tutorial existente para reestructurarlo.

:::

## Secciones de los tutoriales {#tutorial-sections}

### Descripción general {#overview}

Explica los productos o los servicios que se discuten en el tutorial.
Proporciona información de fondo para el propósito del tutorial y lo que
tiene por objetivo presentar. El tutorial siempre se debe basar en un
producto de Polygon.

### Lo que aprenderás {#what-you-ll-learn}

Resume lo que el usuario aprenderá en el tutorial.

:::note Ejemplo

Explorarás cómo usar el paquete de Truffle para desarrollar aplicaciones descentralizadas (dApps)
de Polygon.

:::

#### Resultados del aprendizaje {#learning-outcomes}

Describe los resultados del aprendizaje.

:::note Ejemplo

1. Aprenderás sobre la fauna.
2. Aprenderás a usar ReactJS para la interfaz de usuario de tu dApp.
3. Descubrirás cómo proteger los datos de tu dApp.

:::

Menciona los prerrequisitos y con lo que el usuario
ya debe estar familiarizado. Incluye los enlaces necesarios en la documentación para las áreas
sobre las que el usuario ya debería estar bien informado.

:::note Ejemplo

Antes de comenzar este tutorial, debes entender los conceptos básicos
del desarrollo de dApps basado en EVM. Consulta estos documentos para obtener más información.

:::

### Lo que harás {#what-you-ll-do}

Describe los pasos del tutorial y las herramientas que se utilizarán.

:::note Ejemplo

Usarás Solidity para crear un contrato inteligente en un entorno de ChainIDE.

1. Configuración de billeteras
2. Escribir un contrato inteligente de ERC-721
3. Compilar un contrato inteligente de ERC-721
4. Desplegar un contrato inteligente de ERC-721
5. Crear un archivo aplanado con la biblioteca Flattener
6. Verificar un contrato inteligente
7. Acuñamiento de NFT

:::

### El tutorial en sí {#the-tutorial-itself}

En general, el tutorial se puede presentar en la mejor categorización, a
criterio del escritor; esto se debe reflejar en la sección [Lo que harás](#what-youll-do)
. Sin embargo, las secciones del tutorial deberán abarcar estas tres categorías principales:

> Durante la creación de las secciones, considera las palabras clave
> y ten en cuenta la SEO.

#### Desarrolla tu aplicación {#build-your-application}

Contenido del tutorial principal Esto puede incluir secciones como "configuración"
e "implementación", para nombrar algunas.

#### Ejecutar o desplegar tu aplicación {#run-or-deploy-your-application}

Explica cómo debería el usuario ejecutar o desplegar su aplicación.

#### Prueba tu aplicación {#test-your-application}

Esto puede incluir pruebas de escritura para un contrato inteligente y verificación
de un contrato inteligente, entre otros.

### Próximos pasos {#next-steps}

Concluye el tutorial y reflexiona sobre los resultados del aprendizaje.
Enumera los siguientes pasos que el usuario puede dar.

:::note Ejemplo

Felicidades por desplegar tu contrato inteligente. Ahora sabes cómo usar ChainIDE
para crear y desplegar contratos inteligentes. Considera probar "este tutorial".

:::
