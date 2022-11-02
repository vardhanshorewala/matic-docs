---
id: staking
title: Staking
description: Desarrolla tu próxima app de cadena de bloques en Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---

Para la red de Polygon, cualquier participante puede calificar para convertirse en validador de Polygon al ejecutar un nodo completo. Para los validadores, el incentivo principal para ejecutar un nodo completo es ganar recompensas y la comisión de la transacción. Los validadores que participan en el consenso de Polygon se ven incentivados a participar, ya que reciben recompensas por bloque y comisión por transacción.

Dado que en la red los espacios para validadores son limitados, el proceso para ser seleccionado como uno implica participar en un proceso de subasta en cadena, el cual ocurre en intervalos regulares, tal como se define [aquí](https://www.notion.so/maticnetwork/State-of-Staking-03e983ed9cc6470a9e8aee47d51f0d14#a55fbd158b7d4aa89648a4e3b68ac716).

## Participación {#stake}

Si el espacio está abierto, la subasta se inicia para los validadores interesados:

- Ofertarán más que en la última oferta que hicieron para el espacio.
- El proceso para participar en la subasta se describe aquí:
    - La subasta inicia automáticamente una vez que se abra el espacio.
    - Para empezar a participar en la subasta, llama a `startAuction()`
    - Esto bloqueará tus activos en el Administrador de Stack.
    - Si otro validador potencial apuesta una participación mayor a la tuya, recibirás los tokens bloqueados de regreso.
    - Nuevamente, puedes apostar más para ganar esta subasta.
- Al final del periodo de subasta, el postor más alto gana y se convierte en un validador en la red de Polygon.

> Si participas en la subasta, mantén el nodo completo funcionando si se reduce la participación debido a un nodo inactivo como validador.

Este es el proceso para convertirse en un validador después de que el mayor oferente ganó el espacio:

- Llama `confirmAuction()`para confirmar tu participación.
- `Bridge` en Heimdall, escucha este evento y lo transmite a Heimdall
- Después de alcanzar el consenso, `Validator` se añade a `heimdall`, pero no se activa.
- `Validator` comienza a validar solo después de `StartEpoch` (definido [aquí](https://www.notion.so/maticnetwork/State-of-Staking-03e983ed9cc6470a9e8aee47d51f0d14#c1c3456813dd4b5caade4ed550f81187))
- Tan pronto `startEpoch` alcanza al validador, se añade a `validator-set` y comienza a participar en la mecánica del consenso.

> Para asegurar la seguridad de las participaciones de los validadores, les sugerimos que proporcionen una dirección de `signer` diferente desde la cual se pueden gestionar las firmas de verificación de `checkPoint`. Esto es para mantener la clave de firma separada de la clave de la billetera del validador, de modo que los fondos estén protegidos en caso de un hackeo de nodos.

### Cancelar la participación {#unstake}

Cancelar la participación permite que el validador esté fuera del grupo activo de validadores. Pero para asegurar una buena participación, la participación se bloquea durante los próximos 21 días.

- Cuando el validador quiere salir del sistema y detener la validación de los bloques y los puntos de verificación, puede hacer `unstake.`
- Esta acción es inmediata a partir de ahora.
- Después de esta acción, el validador se considera fuera del conjunto activo de validadores.

### Volver a participar {#restake}

- Los validadores pueden agregar más participación dentro de su cantidad para ganar más recompensas y ser competitivos para su lugar de validador.
- Mantén tu posición
