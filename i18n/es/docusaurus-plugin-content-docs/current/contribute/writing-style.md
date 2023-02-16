---
id: writing-style
title: Directrices generales de escritura
sidebar_label: General writing guidelines
description: Sigue las siguientes directrices al escribir.
keywords:
  - docs
  - matic
  - polygon
  - documentation
  - writing
  - contribute
  - style
image: https://wiki.polygon.technology/img/polygon-wiki.png
slug: writing-style
---

Esta guía se centra en las mejores prácticas para escribir documentación técnica y
en las convenciones de estilo que se pueden utilizar al desarrollar documentación para Polygon Wiki.
La meta de esta guía es ayudarle a los contribuyentes a escribir contenido claro, conciso
y consistente. El equipo de Polygon trata a Polygon Wiki como un producto de documentos oficiales.

## Directrices principales {#primary-guidelines}

Creemos que una de las cosas que hace a Polygon especial es su diseño coherente y
buscamos conservar esta característica distintiva. El equipo de Polygon trata a Polygon Wiki
como un producto de documentos oficiales. Desde el principio, definimos algunas directrices para garantizar que nuevas
contribuciones solo mejoren el proyecto en general:

- **Calidad**: el código del proyecto de Polygon debe cumplir las directrices de estilo y contar con
suficientes casos de prueba, mensajes de confirmación descriptivos, evidencia de que las contribuciones
no contraríen los compromisos de compatibilidad ni causen interacciones adversas de sus características
y evidencia de un alto grado de evaluación de pares de alta calidad.
- **Tamaño**: la cultura del proyecto de Polygon consta de pequeñas "pull requests", o peticiones de validación,
que se presentan regularmente. Cuanto más grande sea la pull request (PR), más probable será que se te pida
volver a presentarla como una serie de PR más pequeñas, autocontenidas y que se puedan revisar individualmente.
- **Mantenibilidad**: si la característica requiere mantenimiento continuo (por ejemplo, soporte
para una marca particular de bases de datos), podemos pedirte que aceptes la responsabilidad
de mantener esta característica.

La guía de estilo se inspira en los siguientes manuales de estilo:

> Si no puedes encontrar la respuesta a una pregunta de estilo, tono de voz o terminología
> en esta guía, consulta estos recursos.

- [Guía de estilo de Google](https://github.com/google/styleguide/blob/gh-pages/docguide/style.md)
- [Manual de estilo de Oxford](https://global.oup.com/academic/product/new-oxford-style-manual-9780198767251?cc=nl&lang=en&)
- [Manual de estilo de Microsoft](https://docs.microsoft.com/en-us/style-guide/welcome/)

### Generador de sitios estáticos {#static-site-generator}

Wiki se desarrolla con un [Docusario](https://docusaurus.io/), un generador de sitios estáticos para
construir sitios de documentación en "Markdown", lenguaje de marcado. Wiki sigue la siguiente plantilla de metadatos
para sus archivos en lenguaje de marcado y se debe adaptar para cada documento nuevo:

```
---
id: wiki-maintainers
title: Wiki Maintainers
sidebar_label: Maintainers
description: A list of Polygon Wiki maintainers
keywords:
  - docs
  - matic
  - polygon
  - wiki
  - docs
  - maintainers
  - contributors
image: https://matic.network/banners/matic-network-16x9.png
slug: community-maintainers
---
```

Hay algunos aspectos importantes a considerar al escribir los metadatos para un archivo de marcado:
- Pedimos a los colaboradores que usen una **identidad única** y que eviten **solo** usar palabras o frases genéricas, como "Introducción" o "Descripción general".
- El **título** es la frase que se usa al inicio de un artículo; en el caso de este, es "Directrices generales de escritura". No es necesario añadir un encabezado de H1 o H2 para introducir cada artículo. En su lugar, usa este **título** de los metadatos.
- La **descripción** no puede ser demasiado larga, ya que se usa en los títulos del índice, cuyas cantidades de caracteres tienen un límite. Por ejemplo, la descripción "Una cadena de bloques es un libro mayor para registrar transacciones" para *basics-blockchain.md* aparece en un título de índice así:
![img](/img/contribute/index-tile.png)

  La **descripción** debe tener **hasta 60 caracteres**, incluidos los espacios entre ellos.
- Las palabras clave son importantes para aumentar la SEO y describir el artículo. Proponte incluir al menos cinco palabras clave.

:::note

Consulta la
[documentación oficial de metadatos](https://docusaurus.io/docs/next/api/plugins/@docusaurus/plugin-content-docs#markdown-front-matter) para obtener más información.

:::

### Comparte la experiencia con el lector {#share-the-experience-with-the-reader}

- Primera persona: no uses "Yo". Usa el punto de vista de primera persona frugalmente y
con intención. Cuando se usa demasiado, la narrativa en primera persona puede abrumar con un sentido de
experiencia compartida y oscurecer el viaje del lector.
- Segunda persona: en la mayoría de los casos, puedes dirigirte al lector directamente. Para tutoriales, puedes usar la primera
persona plural (nosotros, nuestro, nuestras) o el punto de vista de la segunda persona. Dado que los tutoriales proporcionan
un enfoque más guiado para un tema, el uso de la primera persona en plural es una práctica más natural y
comúnmente aceptada que en otros tipos de documentación.
- Tercera persona: no uses "nosotros" para referirte a Polygon o a Polygon Technology.
- Voz activa: usa el tiempo presente siempre que sea posible. Hay situaciones en las que la voz pasiva
es apropiada; úsala cuando debas enfocarte en el agente.
- Ten en cuenta la presencia humana: usa un tono dinámico al describir conceptos técnicos,
lo cual le ayuda mucho al lector a sentirse conectado con el material, en vez de describir el software (o el código)
únicamente en función de lo que hace.
- Pronombres: usa lenguaje de género neutro cuando sea posible. En general, puedes
cambiar cualquier sustantivo de singular a plural para lograr concordancia entre sujeto, verbo y pronombre, y con esto evitar el
uso de pronombres de género específico como "él" o "ella".
  - Ten cuidado con los pronombres impersonales y potencialmente ambiguos. Si usas cualquiera de los siguientes
  pronombres impersonales, asegúrate de responder "¿de qué?", "de cuál?" o "¿como qué?" en la oración.
    - todos, todas, otro, otra, cualquier, cualquiera
    - cada uno, cada una, ambos, ambas
    - pocos, pocas, muchos, muchas, ninguno, ninguna,
    - uno, una, otro, otra
    - iguales, varios, varias, algunos, algunas, tal
    - que, ellos, ellas, estos, estas, aquellos, aquellas

### Brevedad y concisión {#being-swift-and-concise}

- La documentación es fuerte y significativa cuando se usan las palabras necesarias y las frases correctas.
  - Utiliza palabras comunes y conocidas siempre que sea posible.
  - Evita adornar demasiado el lenguaje y usar frases excesivamente literarias.
  - Evita la jerga, los coloquialismos y las frases idiomáticas.
  - Evita el uso de adverbios y las declaraciones subjetivas. Por ejemplo, no uses palabras y frases que incluyan
  fácilmente, rápidamente, simplemente o velozmente. Si es necesario, también es mejor no resaltar algo lo suficiente
  que exagerarlo.
  - No uses frases que presenten ambigüedad. Por ejemplo, en lugar de escribir "Cuando esta versión esté en vivo..."
  usa "Después de que esta versión esté en vivo...".
  - Pon mucha atención a la selección de palabras. Elige el uso de "desde" (lo que implica un período de tiempo) en lugar de
  "porque" (que implica causa y resultado), o usa "una vez" (ocurrencia única) en vez de "después de"
  (múltiples ocurrencias posteriores a algo).
  - Evita el uso de signos de exclamación.
- Evita agregar palabras o frases innecesarias. Algunos ejemplos:
  - En vez de decir "y luego", usa solo "luego".
  - En lugar de decir "Con el fin de", puedes decir "Para".
  - En vez de decir "al igual que", puedes usar "y".
  - En lugar de decir "vía", puedes usar un sustituto más adecuado del español, como "con" "a través de" o "por".
- Usa un tono conversacional que no sea demasiado formal, pero que sea profesional.
- Claridad: dale vida a la palabra o a la frase cuando sea posible. Por ejemplo:
  - En lugar de usar "p. ej.", utiliza "por ejemplo".
  - En vez de decir "i.e.", puedes decir "en otras palabras" o reestructurar la oración para que tenga un significado claro sin
  la necesidad de la calificación adicional.
  - En lugar de escribir "etc.", escribe "entre otros" o revisa el contenido para que no sea necesario aplicar el término. En vez de
  usar "etc." para terminar una lista de ejemplos, concéntrate en uno o dos y emplea expresiones como "similar a" o "como".
  - En lugar de usar palabras como "in situ", usa un sustituto apropiado del español, como "en el sitio".
  - El lenguaje común le da un tono conversacional más natural a la documentación.
  Asegúrate de conservar un nivel apropiado de formalidad.

## Estructura {#structure}

Los documentos deben organizarse en secciones. Cada sección debe contener
un tema. Dentro de cada sección habrá uno o varios párrafos.
Cada párrafo debe transmitir una sola idea. Intenta evitar repetir las mismas ideas
en diferentes secciones, y divide los párrafos de modo tal que contengan múltiples perspectivas.
El lector debería poder comprender de qué se trata un párrafo desde la primera oración.

## Documentación del producto {#product-documentation}

Si estás escribiendo sobre un producto específico, asegúrate de que el documento se asemeje al
producto. Anteriormente, la documentación de Polygon era generalizada y basada en PoS de Polygon.
Ahora que hay múltiples productos basados en Polygon, los contribuyentes deben estar al tanto
de sus adiciones.

Por ejemplo, "Desplegar un contrato inteligente en Polygon con ####" es ambiguo. Si este tutorial
se refiriera a PoS de Polygon, eso debería quedar claro y
se debería escribir "Desplegar un contrato inteligente en PoS de Polygon con ####". Si usamos el mismo ejemplo con un
rollup de Polygon, como Polygon Hermez, escribiríamos "Desplegar un contrato inteligente en Polygon Hermez con ####".

Asegúrate de que la documentación del producto, ya sea una guía general o un tutorial,
se agregue al núcleo adecuado de documentación del producto. Para la mayoría de los documentos, su referencia de estar
bajo uno de los núcleos generales (por ejemplo, "Desarrollar" o "Validar"), pero el documento en sí
estará bajo la documentación de su producto. Te deberás referir al producto en el núcleo
al agregarlo a `sidebars.js`. Sin embargo, el documento en sí estará en su respectivo núcleo de documentación de productos
y redirigirá al usuario cuando haga click en él. La misma guía aplica a la mayoría
de los documentos. La referencia debería estar bajo uno de los núcleos generales, pero el documento en sí
estará bajo la documentación del producto.

Casi toda la documentación basada en API en Polygon Wiki se encuentra como
documentación de referencia, con la excepción de las API mencionadas en los tutoriales.
Por ejemplo, la documentación de API en Matic.js proporciona información sobre
la estructura, los parámetros y los valores de retorno para cada función o método en la API.

## Documentación de la API {#api-documentation}

Puedes considerar lo siguiente al documentar una API:

* Diseña una introducción sólida que proporcione un punto de partida.
* Proporciona una descripción clara de la llamada o la solicitud. Describe el propósito del punto final.
* Lista completa de parámetros:
  * Tipos de parámetros
  * Expresiones sintácticas con marcadores de posición que muestran los parámetros disponibles
  * Formato especial
* Ejemplos de códigos para muchos lenguajes
* Llamada de muestra con el resultado esperado.
* Códigos de error. Casos de borde.
* Instrucciones sobre cómo adquirir claves de API, de ser necesario.
* Notar escenarios comunes o preguntas frecuentes siempre es útil.
* Enlaces a recursos adicionales, como publicaciones en redes sociales, blogs o contenido de video.
