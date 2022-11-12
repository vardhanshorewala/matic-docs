---
id: what-is-proof-of-stake
title: ¿Qué es la prueba de participación?
description: "Es un algoritmo de consenso que depende de validadores."
keywords:
  - docs
  - matic
  - polygon
  - stake
  - delegate
  - validate
  - pos
image: https://matic.network/banners/matic-network-16x9.png
---

La prueba de participación (PoS) es una categoría de algoritmos de consenso para cadenas de bloques públicas que dependen de un validador de [participación](/docs/maintain/glossary#staking) económica de la red.

En cadenas de bloques públicas basadas en prueba de trabajo (PoW), el algoritmo recompensa a los participantes que descifran criptogramas para validar transacciones y crear nuevos bloques. Ejemplos de cadenas de bloques con PoW: Bitcoin, Ethereum actual.

En cadenas de bloques públicas basadas en PoS, un conjunto de validadores se turna para proponer y votar en el bloque siguiente. El peso del voto de cada validador depende del tamaño de su depósito ([participación](/docs/maintain/glossary#staking)). Las importantes ventajas de la PoS incluyen la seguridad, un menor riesgo de centralización y la eficiencia energética. Ejemplos de cadenas de bloques PoS: Eth2, Polygon.

En general, un algoritmo PoS luce como se muestra a continuación. La cadena de bloques guarda un registro de un conjunto de validadores y, cualquier persona que tiene la criptomoneda base de la cadena de bloques (Ether, para el caso de Ethereum) puede convertirse en un validador si envía un tipo especial de transacción que bloquea su Ether en un depósito. El proceso de crear y aceptar nuevos bloques se realiza a través de un algoritmo de consenso del que todos los validadores actuales pueden participar.

Existen muchos tipos de algoritmos de consenso y muchas maneras de asignar recompensas a los validadores que participan en el algoritmo de consenso, por lo que hay de pruebas de participación “para todos los gustos”. Desde una perspectiva algorítmica, existen dos tipos principales: PoS basados en cadena y PoS estilo [BFT](https://en.wikipedia.org/wiki/Byzantine_fault_tolerance).

En **una prueba de participación**, el algoritmo selecciona un validador de forma pseudoaleatoria durante cada intervalo de tiempo (por ejemplo, cada periodo de 10 segundos puede un ser un intervalo de tiempo) y le asigna al validador el derecho de crear un bloque único, y dicho bloque debe estar unido a otro bloque anterior (en general, al bloque del final de la cadena anterior más larga) y, de esta manera, con el transcurso del tiempo, la mayoría de los bloques convergen en una única cadena en constante crecimiento.

En **la prueba de participación BTF**, a los validadores se les asigna **de manera aleatoria** el derecho de *proponer* bloques, pero *el acuerdo sobre qué bloque es canónico* se realiza a través de un proceso de múltiples rondas en la que cada validador envía un “voto” para algún bloque específico durante cada ronda y, al final del proceso, todos los validadores (honestos y en línea) están en permanente acuerdo sobre si un bloque determinado forma parte de la cadena o no. Ten en cuenta que los bloques pueden seguir estando *encadenados*; la diferencia fundamental es que el consenso sobre un bloque puede provenir de un bloque y no depende de la longitud o del tamaño de la cadena que lo continúa.

Para obtener más información, consulta [https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ](https://github.com/ethereum/wiki/wiki/Proof-of-Stake-FAQ).

Consulta también:

* [Delegador](/docs/maintain/glossary#delegator)
* [Validador](/docs/maintain/glossary#validator)
