---
id: contributor-guidelines
title: Cómo contribuir
sidebar_label: Contributor guidelines
description: Prepárate para tu próxima contribución
keywords:
  - docs
  - matic
  - polygon
  - contribute
  - contributor
  - contributing
image: https://wiki.polygon.technology/img/polygon-wiki.png
slug: orientation
---

:::tip
Siéntete libre de [plantear un problema en nuestro repositorio de Wiki](https://github.com/maticnetwork/matic-docs/issues)
:::

## Identifica un área en la cual contribuir {#identify-an-area-to-contribute-to}

Hay varias maneras de identificar un área en la cual contribuir a Wiki:

- Lo más fácil es ponerse en contacto con uno de los [mantenedores de Wiki](/docs/contribute/community-maintainers)
y decirle que quieres hacer una contribución a Polygon Wiki. La persona trabajará contigo para encontrar
un área en la cual puedas contribuir.
- Si tienes una contribución específica en mente, pero no estás seguro al respecto, confirma si
la contribución es apropiada al contactar a uno de los [mantenedores de Wiki](/docs/contribute/community-maintainers) directamente.
- Si no tienes una contribución específica en mente, también puedes navegar por los problemas,
según se encuentran etiquetados `help wanted`en el [repositorio de Polygon GitHub](https://github.com/maticnetwork).
- Los problemas que además tienen la `good first issue`etiqueta se consideran ideales
para los novatos.

## Añadir a la documentación de Polygon {#add-to-the-polygon-documentation}

  - Si necesitas agregar o cambiar algo en Polygon Wiki, presenta un pull request (PR)
  contra la `master`rama (consulta la PR de muestra).
  - El equipo de documentación revisará la PR o se comunicará, según corresponda.
  - Repositorio: https://github.com/maticnetwork/matic-docs
  - Muestra de PR: https://github.com/maticnetwork/matic-docs/pull/360

:::tip
Si quieres ejecutar nuestra Wiki localmente en tu máquina, consulta la sección [que ejecuta la](https://github.com/maticnetwork/matic-docs#run-the-wiki-locally) Wiki localmente. Si estás añadiendo un nuevo documento, se recomienda tener un resumen o introducción básico y un enlace a tu Github o documentación para obtener más detalles.
:::

## Reglas de Git {#git-rules}

Para cambiar entradas, usamos `gitchangelog` para todos nuestros repositorios. Para eso, tenemos que
cumplir con la siguiente convención para el mensaje de compromiso. Si no sigues esta convención,
no habrá ninguna fusión.

### Convención para comprometer mensajes {#commit-message-convention}

Las siguientes son sugerencias de temas útiles en los que pensar al agregar
tus mensajes de compromiso. Puede que quieras separar tus compromisos en secciones grandes:

- Por intención (por ejemplo: nuevo, corrección, cambio...)
- Por objetivo (por ejemplo: documento, empaque, código...)
- Por audiencia (por ejemplo: desarrolladores, testers, usuarios...)

Además, podrías etiquetar algunos compromisos como:

- Compromisos "menores": son los que no deberían generar resultados en tu registro de cambios (cambios cosméticos,
pequeños errores tipográficos en los comentarios...).
- "Refractores: si en realidad no hay cambios significativos de las características. Por lo tanto, esto
tampoco debería formar parte del registro de cambios que se le muestra al usuario final, pero
podría ser de tu interés si tienes un registro de cambios para desarrollador.
- También, podrías etiquetar con "api" para marcar cambios de API, o si es una nueva API o algo similar.

Intenta escribir tu mensaje de compromiso al dirigirte a la funcionalidad del usuario tan a menudo como puedas.

:::note Ejemplo

Este es un `--oneline` de registro de Git estándar para mostrar cómo se podría guardar esta información:

```
* 5a39f73 fix: encoding issues with non-ascii chars.
* a60d77a new: pkg: added ``.travis.yml`` for automated tests.
* 57129ba new: much greater performance on big repository by issuing only one shell command for all the commits. (fixes #7)
* 6b4b267 chg: dev: refactored out the formatting characters from GIT.
* 197b069 new: dev: reverse ``natural`` order to get reverse chronological order by default. !refactor
* 6b891bc new: add utf-8 encoding declaration !minor
```

:::

Para obtener más información, consulta
[¿Cuáles son algunas buenas formas de administrar un registro de cambios con Git?](https://stackoverflow.com/questions/3523534/good-ways-to-manage-a-changelog-using-git/23047890#23047890).

Para obtener más información, consulta [https://chris.beams.io/posts/git-commit/](https://chris.beams.io/posts/git-commit/).
