---
id: writing-style
title: Manual General de Redacción
sidebar_label: General writing guidelines
description: Sigue el siguiente manual cuando redactes.
keywords:
  - docs
  - matic
  - polygon
  - documentation
  - writing
  - contribute
  - style
image: https://matic.network/banners/matic-network-16x9.png
slug: writing-style
---

Este manual se centra en las mejores prácticas para redactar la documentación técnica y sobre las convenciones de estilo que debes utilizar cuando desarrollas documentación para Polygon Wiki El objetivo de esta guía es ayudar a los contribuyentes a redactar contenidos que sean claros, concisos, y consistentes. El equipo Polygon trata al Polygon Wiki como un producto de documentos oficiales.

## Manual principal {#primary-guidelines}

Creemos que una de las cosas que hacen especial a Polygon es su diseño coherente y tratar de conservar esta característica definitoria. El equipo de Polygon trata el Polygon Wiki como un producto de documentos oficiales. Desde el principio definimos algunas directrices en el manual para garantizar nuevas contribuciones que solo mejoran el proyecto en general:

- **Calidad**: Código en el proyecto Polygon que debe cumplir con las directrices de estilo, con
 suficientes casos de prueba, mensajes descriptivos, evidenciando que las contribuciones no rompen ningún compromiso de compatibilidad o causan interacciones de características adversas, y evidencia de revisión de pares de alta calidad.
- **Tamaño**: La cultura del proyecto Polygon es una de las pequeñas solicitudes de extracción regularmente
 presentadas. Cuanto mayor sea una solicitud de extracción, es más probable que te lo pregunten para volver a presentar como una serie de RP más pequeños independientes y revisables individualmente.
- **Capacidad de Mantenimiento**:si la característica requiere mantenimiento continuo, por ejemplo, soporte técnico
 para una marca de base de datos en particular, es posible que te pidamos que aceptes la responsabilidad de mantener esta característica.

La guía de estilo se inspira en los siguientes manuales de estilo:

> Si no puedes encontrar la respuesta a una pregunta de estilo, voz terminología en esta guía consulta estos recursos.

- [Guía de Estilo de Google](https://github.com/google/styleguide/blob/gh-pages/docguide/style.md)
- [El Manual de Estilo de Oxford](https://global.oup.com/academic/product/new-oxford-style-manual-9780198767251?cc=nl&lang=en&)
- [El Manual de Estilo de Microsoft](https://docs.microsoft.com/en-us/style-guide/welcome/)

### Generador de sitio estático {#static-site-generator}

El Wiki es construido usando [Docusaurus](https://docusaurus.io/), un generador de sitio estático para
 construir sitios de documentación de rebajas. El Wiki sigue los siguientes metadatos plantilla para sus archivos de rebajas y debe ser adaptada para cada nuevo documento:

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

Hay algunos aspectos importantes a considerar al redactar los metadatos para un archivo de reducción:
- Pedimos a los colaboradores que utilicen una **id única**; evite **solo** el uso de palabras genéricas o frases como "Introducción" o de "Visión general".
- El **título** es la frase utilizada al principio del artículo, "Manual General de Redacción" para este artículo. Por lo tanto, no es necesario agregar un encabezado H1/H2 para introducir cada artículo. En cambio, use este **título** desde los metadatos.
- La **descripción** no puede ser demasiado larga, ya que se usa en los mosaicos de índice los cuales tienen una limitación en el número de caracteres. Por ejemplo, la descripción "Blockchain es un libro mayor inmutable para registrar transacciones" para el *basics-blockchain.md* aparece en un mosaico de índice como tal:
 ![img](/img/contribute/index-tile.png)

La **descripción** entonces debe tener **hasta 60 caracteres**, considerando los espacios entre los caracteres.
- Las palabras clave son importantes para aumentar el SEO y describir el artículo. Trata de apuntar por lo menos cinco palabras clave.

:::note

Por favor, vea la [documentación oficial de metadatos](https://docusaurus.io/docs/next/api/plugins/@docusaurus/plugin-content-docs#markdown-front-matter) para más detalles.

:::

### Comparte la experiencia con el lector {#share-the-experience-with-the-reader}

- Para primera persona: no uses "I" o "yo". Usa el punto de vista en primera persona con moderación y con intención. Cuando se usa en exceso, la narrativa en primera persona puede abrumar el sentido de una experiencia compartida y oscurecer el viaje del lector.
- Segunda Persona: En la mayoría dirígete al lector directamente. Para los tutoriales, use primero ya sea persona plural—nosotros, nuestro, o el punto de vista de la segunda persona. Porque los tutoriales proporcionan un enfoque más guiado para un tema, utilizando el plural en primera persona que es un plural más natural y en la práctica es comúnmente aceptado que en otros tipos de documentación
- Tercera Persona: no uses "nosotros" para referirte a Polygon o a tecnología de Polygon.
- Voz activa: Usa el tiempo presente siempre que sea posible. Hay situaciones en las que una voz pasiva es apropiada; vuelve a la voz pasiva cuando el agente necesita ser el enfoque.
- Ten en cuenta la presencia humana: teniendo un tono dinámico al describir conceptos técnicos realmente ayuda a un lector a conectar con el material en lugar de describir el software (o código) solo para lo que hace.
- Pronombres: usa pronombres neutrales de género, como "ellos" siempre que sea posible. Generalmente puedes cambiar cualquier sustantivo de un singular a un plural para tener un acuerdo de sujeto verbo pronombre y evitar el uso de pronombres específicos de género como "él", a "él" o "ella", a "su" o "ella",
  - Ten cuidado con los pronombres impersonales y potencialmente ambiguos. Si usas cualquiera de los siguientes pronombres impersonales, asegúrate de responder "de ¿qué?", "de ¿cuál?" o "¿cómo qué?" en la frase.
    - todos, otro, cualquiera
    - Cada uno, cualquiera
    - pocos, muchos, ninguno de ellos, ninguno,
    - uno, otro
    - iguales, varios, algunos, tal
    - eso, ellos, estos, esos

### Ser rápido y conciso {#being-swift-and-concise}

- La documentación es fuerte y significativa cuando se usan las palabras necesarias y las frases correctas.
  - Usa palabras comunes y bien conocidas siempre que sea posible.
  - Evita el lenguaje floral y las frases literalmente excesivas.
  - Evita la jerga, los coloquialismos y las frases idiomáticas.
  - Evita los adverbios y las declaraciones subjetivas. Por ejemplo, no uses palabras y frases que incluyen fácilmente, rápidamente, simplemente, rápido. Si es necesario, también es mejor subestimar que sobreestimar.
  - No uses frases que introducen ambigüedad. Por ejemplo, en lugar de "Cuando este lanzamiento está en vivo..." usar "Después de que esta liberación está en vivo...".
  - Presta una atención adicional con la opción de las palabras. Eligiendo usar "desde" (lo que implica un período de tiempo) en lugar de "porque" (lo que implica la causa y el resultado) o usando "una vez" (una ocurrencia única) en lugar de "después" (cada tiempo).
  - Evita los signos de exclamación.
- Evita agregar palabras o frases innecesarias. Algunos ejemplos:
  - En lugar de decir "y luego", solo tienes que usar "luego".
  - En lugar de decir "Para que", solo tienes que usar "para".
  - En lugar de decir "igual como", solo tienes que usar "y".
  - En lugar de decir "vía", usa un sustituto apropiado en inglés, como "usar", "a través" o "por".
- Usa un tono conversacional que no sea demasiado formal, pero que aún debe ser profesional.
- Claridad: da vida a la palabra o frase siempre que sea posible. Por ejemplo:
  - En lugar de decir "ejem.", usa "por ejemplo".
  - En lugar de decir "es decir", usa "eso es" o reescribir la frase para dejar el significado claro sin necesitar una calificación extra.
  - En lugar de decir "etc.", usa "y así sucesivamente" o revisa el contenido para hacer que el término sea innecesario. En lugar de "etc." para terminar una lista de ejemplos enfócate en uno o dos ejemplos y utiliza "tales como" o "similares".
  - En lugar de "advertencia" usa un sustituto apropiado en inglés, como "aviso", "precaución"
  - Las contracciones le dan a la documentación un tono conversacional más natural, al menos para los hablantes de inglés. Sé consciente de cuándo y por qué usas contracciones.

## Estructura {#structure}

Los documentos deben organizarse en secciones. Cada sección debe ser responsable para presentar un tema o asunto. Dentro de cada sección existirán uno o varios párrafos Cada párrafo solo debe transmitir un pensamiento. Trata de evitar repetir los mismos pensamientos en diferentes secciones y párrafos divididos que tienen múltiples puntos de discusión. El lector debe entender de qué se trata un párrafo desde su primera frase.

## Documentación del producto {#product-documentation}

Si estás escribiendo sobre un producto específico, asegúrate de que el documento se parece a ese producto Anteriormente, la documentación de Polygon se generalizó, basado en PoS de Polygon Ahora que hay productos múltiples basados en Polygon, los contribuyentes necesitan tener cuidado acerca de sus adiciones.

Por ejemplo, "Implementar un contrato inteligente en Polygon usando ##" es ambiguo. Si este tutorial se refiere a PoS de Polygon, debe ser claro, como en, "Implementar un contrato inteligente en PoS de Polygon usando ##". Usando el mismo ejemplo con un Polygon Rollup como Polygon Hermez, "Implementando un contrato inteligente en Polygon Hermez usando ##".

Asegúrate de que la documentación del producto ya sea una guía general o que un tutorial este agregado a la documentación del producto correcto Hub. Para la mayoría de los documentos, su referencia debe existir bajo uno de los Hubs generales (por ejemplo, "Desarrollar" o "Validar"), pero el documento actual vivirá bajo su documentación del producto. Necesitarás hacer referencia al documento en el Hub agregándolo al`sidebars.js`
 Sin embargo, el documento actual, por sí mismo existirá en la respectiva documentación producto Hub, y será redirigido al usuario una vez que haga un clic en él. La misma guía se aplica a la mayoría de los documentos. Su referencia debe existir bajo uno de los Hubs generales, pero el documento actual vivirá bajo su documentación del producto.

La mayor parte de la documentación basada en API en el Polygon Wiki está en forma de documentación de referencia, con la excepción de las API mencionadas en los tutoriales. Por ejemplo, la documentación API en Matic.js proporciona una información acerca de la estructura, parámetros y regresar valores para cada función o método en API

## Documentación API {#api-documentation}

Considera lo siguiente cuando documentas API:

* Una introducción sólida que proporciona un punto de partida.
* Una descripción clara de la llamada o solicitud. Describe lo que las terminales hacen.
* Un listado completo de parámetros:
  * Tipos de Parámetros
  * Expresiones de sintaxis con marcadores de posición que muestran los parámetros disponibles
  * Formateo especial
* Ejemplos de códigos para varios idiomas.
* Una llamada de muestra con el resultado esperado.
* Códigos de error. Casos de borde
* Instrucciones acerca de cómo adquirir claves API si es necesario.
* Tomar en cuenta que las preguntas frecuentes comunes o los escenarios siempre es útil.
* Enlaces a recursos adicionales, como publicaciones en redes sociales, blogs o contenido de video.
