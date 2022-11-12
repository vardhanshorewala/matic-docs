---
id: faq
title: Preguntas frecuentes
description: Desarrolla tu próxima app de cadena de bloques en Polygon.
keywords:
  - docs
  - matic
image: https://matic.network/banners/matic-network-16x9.png
---
## ¿Qué es Polygon? {#what-is-polygon}

Polygon es una solución de escalabilidad basada en cadenas laterales para las cadenas de bloques públicas. Polygon ofrece escalabilidad, además de
 garantizar una experiencia superior al usuario de una manera segura y descentralizada. Cuenta con una implementación de trabajo
 para Ethereum en la red de prueba Kovan. Polygon tiene previsto ser compatible con otras cadenas de bloques en el futuro, lo cual le permitirá
 ofrecer características de interoperabilidad, además de ofrecer escalabilidad a las cadenas de bloques públicas existentes.

## ¿En qué se diferencia Polygon de las demás implementaciones de Plasma? {#how-is-polygon-different-from-other-implementations-of-plasma}

La implementación de Plasma por parte de Polygon se basa en las cadenas laterales basadas en estado que se ejecutan en la máquina virtual de Ethereum (EVM), mientras que las otras implementaciones de Plasma utilizan principalmente las transacciones de salida no gastadas (UTXO), que restringen que sean específicamente de pagos. Contar con cadenas laterales basadas en estado permite a Polygon ofrecer escalabilidad para los contratos inteligentes genéricos también.

En segundo lugar, Polygon utiliza una capa de punto de verificación pública que publica puntos de verificación después de intervalos regulares (a diferencia de los puntos de verificación después de cada bloque de Plasma Cash) que les permite a las cadenas laterales operar a altas velocidades mientras publica los puntos de verificación en lotes. Estos puntos de verificación, junto con las pruebas de fraude, aseguran que las cadenas laterales de Polygon operen de manera segura y que se pueda detectar cualquier actividad fraudulenta en la cadena principal de Ethereum y se penalice mediante la reducción de las participaciones de los protagonistas desleales. Esta seguridad de la cadena principal es complementaria a la seguridad del protocolo de la PoS (prueba de participación) en las cadenas laterales.

## Tu proyecto aporta escalabilidad a Ethereum mediante las cadenas de Plasma, ¿es un protocolo o una cadena de bloques nativa en sí misma? {#your-project-provides-scalability-for-ethereum-using-plasma-chains-is-it-a-protocol-or-a-native-blockchain-in-itself}

La red de Polygon es una solución de “cadena lateral” en donde los activos de la cadena principal de Ethereum, es decir, todas las aplicaciones descentralizadas, los tokens y los protocolos de la cadena principal se pueden trasladar o migrar a las cadenas laterales de Polygon y, cuando resulta necesario, se pueden retirar los activos y regresarlos a la cadena principal.

## ¿Cuáles son las ventajas competitivas de Polygon con respecto a su competencia? {#what-are-the-competitive-advantages-of-polygon-over-its-competitor}

- Soluciones de escalamiento de capa dos

Polygon está abocado a lograr escalar con la descentralización. Polygon utiliza puntos de verificación periódicos y pruebas de fraude. Cuando los usuarios quieren retirar sus activos, utilizan los puntos de verificación para probarlos en la cadena lateral, mientras que se necesitan pruebas de fraude para evaluar si existió fraude o cualquier comportamiento perjudicial y para reducir a los participantes.

Otros proyectos, como Loom, también están ofreciendo soluciones de escalamiento de capa dos. Loom anunció recientemente sus planes de Zombiechain que podrían compartir similitudes con Polygon. Pero existen los siguientes dos elementos clave en los que diferimos:

En primer lugar, el enfoque es diferente. Loom se centra en los juegos y las aplicaciones sociales (que requieren relativamente menos descentralización), mientras que Polygon se centra no solo en transacciones y operaciones financieras, sino también en los juegos y otras aplicaciones descentralizadas e informales. También tenemos planes para servicios financieros de gran escala, como las aplicaciones descentralizadas de préstamos y operaciones comerciales (intercambios de tokens, operaciones con márgenes y mucho más)

En segundo lugar, Plasma Cash, que es lo que creemos que Loom quiere utilizar “en el futuro”, tendrá tiempos de bloques mejores que los de Ethereum, debido a que se necesita llevar cada bloque de la cadena lateral a la cadena principal, mientras que Polygon utiliza puntos de verificación por un tiempo de bloque de 1 segundo (con la capa de PoS).

Debido a que Plasma Cash funciona con los toques no Fungibles (NFT), es excelente con tarjetas de juegos y cambios de estado social, en los que ya estableciste los cargos previamente (incluidos como NFT, por ejemplo, “20 tokens” para videojuegos que equivalgan a 1 moneda de NFT en Plasma Cash). Para las transferencias de token normales, es posible que necesites intercambiar tokens (como billetes y cambio de divisas), además de Plasma Cash que dificulta implementar, aunque ofrece una experiencia de usuario sencilla. Se sigue debatiendo en las llamadas de Plasma, mientras que Polygon utiliza Plasma basado en estado (más cercanas a la MVP de Plasma).

- Soluciones de escalamiento de capa uno

Aparte de eso, entre otros proyectos de escalamiento, como Ziliqa y Quarkchain, Polygon se destaca debido a su capacidad de lograr escalar, además de mantener un excelente nivel de descentralización.

Más importante aún, estos proyectos de escalabilidad lograron aportar una nueva perspectiva. Crean nuevas cadenas de bloques donde la comunidad de desarrolladores, el ecosistema de los productos, la documentación técnica y, lo que es más importante, las empresas deben construirse desde “cero”. Por el contrario, Polygon es una cadena habilitada por EVM, el lenguaje de programación, la documentación de desarrolladores, etc. está disponible fuera de la plataforma de Polygon. Todas las aplicaciones descentralizadas y los activos creados en la cadena principal de Ethereum cuentan con escalabilidad disponible con hacer clic en un botón. Esto es posible gracias a que Polygon es una cadena lateral basada en EVM.

- Pagos

En lo que respecta a pagos, Raiden Network puede ser un competidor. Raiden implementó Lightning Network en Ethereum. Un problema importante es la capacidad o liquidez en los hubs. Pero este problema se agrava aún más para Raiden, ya que Lightning Network solo cuenta con un activo (Bitcoin) para que los hubs mantengan la liquidez, mientras que Raiden Network tendría que lograr liquidez por la cantidad ilimitada de activos (Ether, tokens ERC-20)

Consideramos que Polygon tiene una ventaja en cuanto a la facilidad del uso, ya que en Raiden, tanto el remitente como el receptor tienen que crear sus canales de pago. Esto es muy engorroso para los usuarios. Mientras que con la tecnología subyacente de Polygon, para recibir tokens, los usuarios no necesitan canales de pago, sino solo tener una dirección Ethereum válida. Esto también coincide con nuestra visión a largo plazo de mejorar la experiencia del usuario para las aplicaciones descentralizadas.

- Comercio y finanzas

Polygon tiene la intención de habilitar un exchange descentralizado (DEX) (por ejemplo, 0x), fondos de liquidez (por ejemplo, Kyber Network) y demás clases de protocolos financieros, como los protocolos de préstamos (protocolo Dharma) en su plataforma que permitirán a los usuarios de Polygon acceder a diversas aplicaciones de servicios financieros, como DEX, aplicaciones descentralizadas de préstamos y muchas otras

- Otros

Además, el enfoque central de Polygon en crear aplicaciones que tengan una experiencia de usuario mejorada, contribuirá a la adopción masiva de las aplicaciones descentralizadas. Con el mismo objetivo final, tenemos también la intención de crear herramientas de ecosistemas. Nuestros productos como Dagger (que es muy renombrado en la comunidad Ethereum) y Opensigner (implementación del protocolo Walletconnect y la implementación completa de Node.js) dan muestra de ello. -

[WalletConnect](https://github.com/WalletConnect/walletconnect-monorepo)

[Dagger](https://github.com/maticnetwork/eth-dagger.js)

[Sol-Trace](https://github.com/maticnetwork/sol-trace.js)


## ¿Cómo se compara Polygon con otras soluciones de cadena lateral como POA o Go-Chain? {#how-does-polygon-compare-with-other-sidechain-solutions-like-poa-go-chain}

Los proyectos, como POA, utilizan productores de bloques certificados a nivel gubernamental y Go-Chain depende de instituciones de diversos países. Es muy probable que a dichos productores de bloques públicos los influyan organismos externos poderosos y sus propios intereses. Además, las transacciones de cadena lateral solo se aseguran mediante consenso de cadena lateral en donde la cantidad de participantes es muy reducida (3-25), mientras que en Polygon, todas las transacciones laterales están aseguradas mediante múltiples mecanismos en la cadena lateral, así como en la cadena principal.

En la cadena lateral, cualquier transacción realizada mediante una capa de productor de bloques se verifica y cuyos puntos de verificación se comprueban en la cadena principal mediante una capa de punto de verificación altamente descentralizada. De manera que, si se produce alguna transacción fraudulenta en la cadena lateral, se puede detectar y resolver en la capa del punto de verificación. Incluso en situaciones extremas y un escenario muy improbable en el que tanto una capa de productor de bloques, como la capa de punto de verificación se confabulen, hasta en la cadena principal quedan pruebas de fraude y cualquiera del público puede aparecer y pedir la comprobación de cualquier transacción que considere fraudulenta en la cadena lateral. Si la comprobación resulta cierta, existe un desincentivo económico o penalización financiera significativa para las partes que confabularon, ya que sus participaciones se reducen. Además, al que solicitó la comprobación del público se le recompensa con las participaciones reducidas de los protagonistas fraudulentos de la cadena lateral.

Esto hace que Polygon sea una red de cadena lateral con incentivo económico que tiene un alto grado de descentralización y la seguridad de las transacciones de la cadena lateral.

En segundo lugar, la capacidad y las transacciones por segundo (TPS) de las cadenas laterales de Polygon son mucho más elevadas que POA y Go-chain. En especial, Polygon que puede tener miles de transacciones, mientras que POA y Go-chain son cadenas laterales únicas que tienen un límite mayor de algunos miles de transacciones.

## ¿Por medio de qué principios se agregarán las nuevas cadenas laterales? ¿Habrá algún requisito especial para las cadenas laterales locales de las empresas privadas? {#via-what-principles-will-new-side-chains-be-added-will-there-be-any-special-requirements-for-private-companies-local-side-chains}

De manera similar a los canales de estado, Plasma representa una alternativa superior al marco de trabajo del escalamiento, debido principalmente a las garantías de seguridad provistas por el marco de trabajo, que básicamente afirman que los usuarios nunca perderán fondos bajo ninguna circunstancia. Sin dudas, podría existir un retraso a la hora de recuperar el dinero, pero un operador de Byzantine Plasma no puede crear el dinero de la nada, ni invertir dos veces en una transacción.

Polygon se esforzará por ser una infraestructura de cadena de bloques pública y totalmente abierta en el futuro, en la cual los incentivos o desincentivos económicos impulsen principalmente la seguridad y la estabilidad del sistema. De manera que cualquiera debería ser capaz de incorporarse al sistema y participar en el consenso. No obstante, en la primera etapa de la red, Polygon deberá en un principio ocupar un rol más importante para habilitar las cadenas laterales.

Asimismo, las cadenas laterales de Polygon deberían ser cadenas laterales principalmente públicas, es decir, cadenas laterales disponibles para que la use cualquiera del público, al igual que otras cadenas de bloques públicas. Aunque las cadenas Polygon para empresas procurarán ofrecer cadenas laterales especializadas (habilitadas de manera no privada) para las organizaciones particulares. La seguridad y la descentralización de dichas cadenas se mantendrían intactos mediante una capa de puntos de verificación y pruebas de fraude en la cadena principal. Sin embargo, mantener cadenas laterales habilitadas para la privacidad con validación de puntos de verificación y pruebas de fraude en la cadena principal sigue siendo un tema de investigación para nosotros. Estamos analizando nuevas tecnologías como son zkSNARK y zkSTARK.

## ¿En qué difiere Polygon de Celer Network? {#how-is-polygon-different-than-celer-network}

Tanto Polygon como Celer Network son soluciones diferentes al mismo problema: bajo rendimiento de las transacciones en las cadenas de bloques actuales. Ambos utilizan técnicas de escalamiento fuera de la cadena y dependen de la cadena principal para la seguridad final; sin embargo, la diferencia fundamental está en los enfoques: Polygon se basa en un conjunto de cadenas laterales de Plasma con el respaldo del consenso de prueba de participación (consultar https://plasma.io/ para obtener más información), mientras que Celer Network es una solución basada en canales de estado. Ambos proyectos tienen como objetivo las transiciones de estado generalizado fuera de la cadena, pero de muchas maneras diferentes.

Polygon tiene como objetivo crear un ecosistema para desarrolladores de aplicaciones descentralizadas. Debido a que utiliza una cadena lateral de Plasma basada en una cuenta y también emplea un tiempo de ejecución compatible con EVM, denominada VM de Polygon, sería relativamente más fácil para las aplicaciones descentralizadas basadas en Ethereum migrar a Polygon cuando esté en funcionamiento. En lo que a esto se refiere, Celer Network es diferente en términos de la interacción de los desarrolladores.

## ¿Las cadenas laterales también se sincronizarán con la cadena principal (Ethereum)? {#will-side-chains-also-be-synced-with-the-mainchain-ethereum}

Por supuesto. La capa de puntos de verificación pública validará todas las transacciones que se produzcan en las cadenas laterales y publicará las pruebas en la cadena principal. A fin de garantizar la seguridad infalible de las transacciones de la cadena lateral, el contrato de Plasma de la cadena principal contiene varias clases de pruebas de fraude donde cualquier transacción de cadena lateral se puede verificar que no tenga alguna actividad fraudulenta. Si alguien comprueba que sí existió, entonces las participaciones de los protagonistas de la cadena lateral implicados en el fraude se reducen y se transfieren a quien lo comprobó. Esto es equivalente a una recompensa por errores por una participación alta que esté siempre en funcionamiento A continuación, se incluye un diagrama práctico para entender esto:

![Captura de pantalla](../../static/img/matic/Architecture.png)

## ¿Implementarás intercambios atómicos? Si fuera así, ¿de qué manera? {#will-you-implement-atomic-swaps-if-yes-how}

Existen maneras de hacerlo, protocolo Swingyby, puentes de Doge/ETH, [consulta este artículo de Medium](https://medium.com/truebit/enter-the-rabbit-hole-the-doge-ethereum-art-project-31e8116043c4), contratos hash de tiempo limitado o trazabilidad simple. Elegiremos lo más adecuado en términos de interfaz y experiencia del usuario, y seguridad en lo sucesivo. Una vez que los activos de múltiples cadenas de bloques estén disponibles en la cadena lateral, los exchanges descentralizados (DEX) podrán ofrecer exchange entre activos que originalmente son de otras cadenas básicas.

## Al final del informe técnico, se encuentra una lista de “Posibles casos de uso”; ¿todo eso se implementará? ¿En qué orden? {#at-the-end-of-the-white-paper-there-is-a-list-of-potential-use-cases-will-all-of-that-be-implemented-in-what-order}

Polygon Foundation habilitará y ofrecerá soporte a los equipos de ecosistema para desarrollar estos posibles casos de uso. No pretendemos implementar todos estos proyectos por nuestra cuenta, y no queremos dar esa impresión. Pretendemos que Polygon sea una plataforma de aplicaciones descentralizadas, que ofrezca transacciones instantáneas a bajo coste. Una vez que Polygon esté en funcionamiento, seguiremos incorporando soporte para todos esos casos de uso. Todos nos apoyaríamos en que equipos comunitarios colaboren con nosotros en nuestra plataforma para crear estas aplicaciones.

La lógica básica es la siguiente: si existe una aplicación descentralizada o protocolo que funcione en Ethereum, pero está limitada por un rendimiento de transacciones bajo y cargos de transacciones altos, entonces podremos agregar soporte para estas aplicaciones descentralizadas o protocolos en Polygon.

El objetivo en definitiva es desarrollar un escalamiento de estado generalizado, sin embargo, esto llevará tiempo. Ya estamos trabajando con equipos como Parsec Labs, Truebit y Decentraland al respecto de esta iniciativa: encontrarás algunas menciones de MATIC de otros proyectos [aquí](https://parseclabs.org/blog/Development-Update-May-2018/) y [aquí](https://blog.decentraland.org/blockchain-security-will-it-scale-5d82c5df4640).

Pero antes de que eso suceda, agregaremos soporte para contratos y protocolos específicos. Una vez que el contrato esté protegido mediante garantías de prueba de fraude, se podrá implementar en Polygon y podrán utilizarlo aplicaciones descentralizadas.

El orden de prioridad sería: DEX, pagos, proveedores de liquidez, calificaciones de préstamos y crédito, intercambios atómicos.

Aunque la mayoría de estas funciones se ejecutarán en paralelo, estamos conversando con diversos equipos de alto nivel para que colaboren con nosotros para desplegar estos protocolos en las cadenas laterales de Polygon.

## ¿Por qué sería difícil replicar la implementación de Plasma de Polygon? {#why-will-it-be-difficult-to-replicate-polygon-s-plasma-implementation}

A pesar de que con las soluciones de cadena de bloques se trata más acerca del efecto de la red en cuanto a qué red puede escalar o facilitar el crecimiento de un ecosistema mejor que otras, PERO lo más importante acerca de las soluciones de cadenas es que tienen que ser obligatoriamente de código abierto, ya que implica los activos reales que se utilizan en ellas.

Este también es el caso con todos los proyectos de código abierto. Se aplica de igual manera a nosotros, como también a las otras implementaciones rivales, ya que tendremos nuestra licencia pública general (GPL) que exige a cualquiera que utilice nuestra implementación que haga obligatoriamente que su código sea abierto. Pero, reiteramos, el punto es que copiar el código se aplica de manera equitativa a Bitcoin, Ethereum y cualquier otro proyecto, importa más el efecto en la red que un proyecto pueda lograr.

## ¿Qué tiene de especial la implementación de Plasma en la red de Polygon? {#what-s-special-about-polygon-network-s-plasma-implementation}

De manera que, Plasma Polygon utiliza un sistema de modelo basado en cuentas, en lugar del sistema de la salida de una transacción no gastada (UTXO) que se utiliza en Plasma Cash, Plasma MVP y Plasma XT. Esto nos proporciona una gran ventaja de utilizar una EVM en la cadena de Polygon, ya que nos permite utilizar todo el ecosistema de Ethereum (las herramientas para los desarrolladores, bibliotecas de integración, etc.) para Polygon.

Las aplicaciones descentralizadas pueden utilizar de manera sencilla el sistema de Polygon sin realizar cambios en sus tokens ERC-20. Además, la capa de puntos de verificación nos permite tiempos ultrarrápidos en comparación con otras implementaciones de Plasma, ya que combinamos las pruebas de los bloques individuales en los puntos de verificación, mientras que otras implementaciones de Plasma tienen que enviar cada prueba de bloque a la cadena principal

## ¿Cómo vais a resolver los problemas con la centralización? {#how-are-you-going-to-solve-the-issues-with-centralization}

A continuación, encontrarás un diagrama para darte un poco de contexto:

![Captura de pantalla](../../static/img/matic/Merkle.png)

En primer lugar, los nodos de PoA que viste serán Delegados (con prueba de solvencia, es decir, tienen que depositar una gran cantidad de la participación) y se seleccionan básicamente por medio del conocimiento del cliente (KYC) por parte de la capa de PoS, como un nodo de DPoS o DBFT tipo EOS.

En segundo lugar, supongamos que todos los delegados (o dos tercios de ellos) resultan ser fraudulentos y producen bloques defectuosos, entonces los participantes de la capa PoS que validarán todos los bloques y, si se comete algún fraude, se reduce la participación de los delegados, se detiene el punto de verificación para tomar medidas correctivas.

En tercer lugar, digamos que incluso la capa de PoS del participante (que sería una gran cantidad de nodos) también resulta fraudulenta y se confabulan para producir puntos de verificación defectuosos. Es decir, todos los PoA son corruptos y la PoS es corrupta, incluso entonces, conforme la filosofía de Plasma, escribimos una de las cosas codiciadas del escalamiento de la cadena lateral, **pruebas de fraude**, las cuales se observan en muchos proyectos grandes (los observadores pueden considerarse nuestros observadores del repositorio en GitHub). Este mecanismo a prueba de fraude permite que cualquiera del público cuestione alguna transacción en la cadena principal, si estaba en lo cierto, obtiene recompensas de los recortes de las participaciones de todas las partes que participaron en el fraude cometido.

## ¿Por qué se requiere token MATIC? {#why-is-matic-token-required}

Las siguientes razones refuerzan la necesidad de tener token MATIC

### Polygon pretende ser una solución de escalabilidad de propósito general para cadenas de bloques públicas: {#polygon-intends-to-be-a-general-purpose-scaling-solution-for-public-blockchains}
Comenzamos por Ethereum como nuestra primera cadena de base, pero en el futuro, Polygon se podrá desplegar en múltiples cadenas básicas. Pronto se agregarán otras cadenas básicas, de manera que no tendrá sentido tener una moneda (Ether) que se utilice para pagar comisiones en las cadenas laterales. Si hay una preocupación existencial con respecto a cualquier cadena básica en el futuro, contar con la moneda de esas cadenas básicas como activo nativo para Polygon perjudicaría la red en proceso de escalamiento. Por lo tanto, es importante construir el ecosistema del participante en el propio token de la red de Polygon.

### Modelo de seguridad de Appcoin: {#appcoin-security-model}
Polygon pretende habilitar las aplicaciones descentralizadas para pagar las comisiones de Polygon en las monedas de las aplicaciones descentralizadas, por medio de la abstracción del mecanismo de intercambio de token para el que se utiliza un fondo de liquidez como Kyber. El usuario simplemente utiliza las monedas de las aplicaciones descentralizadas para pagar comisiones, en el fondo, la moneda de las aplicaciones descentralizadas se intercambia por tokens MATIC. Por lo tanto, los desarrolladores de aplicaciones descentralizadas que quieren ofrecer una experiencia de usuario fluida contribuirán a mantener el fondo de liquidez de Polygon.

### Cómo abastecer la red en las primeras etapas: {#seeding-the-network-in-nascent-stages}
Es prácticamente imposible abastecer el sistema cuando prácticamente no hay transacciones en la red en un comienzo, de la misma manera que no podemos distribuir ETH a la capa de validadores ni a los productores de bloque altamente descentralizados. Mientras que, con los tokens MATIC hemos suministrado un gran porcentaje de tokens para distribuirlos y abastecer a los productores de bloques, los participantes de puntos de verificación y, por consiguiente, ofrecimos recompensas de bloque. Este suministro garantiza que los participantes reciban recompensas, incluso si la red demora un tiempo en asumir los efectos de la red. De manera similar, es el motivo por el que las recompensas de la Minería de bloques se mantuvieron para Bitcoin, los participantes y los productores de bloques pueden recibir incentivos de esta manera para mantener la red segura.

Si tu preocupación es sobre las operaciones de desarrollo, uno de los pilares de nuestra estrategia es mantener la barrera de entrada de las operaciones de desarrollo muy bajas. Nos hemos asegurado de que todas las herramientas de desarrollo de Ethereum funcionen de inmediato en Polygon. En lo que respecta a los tokens que se necesitan para pagar comisiones en la red de prueba, no difiere de las de los desarrolladores que utilizan Ethereum. Las operaciones de desarrollo reciben tokens gratuitos de la red de prueba de un grifo de Polygon y se pone en marcha, al igual que en Ethereum. Necesitas tokens MATIC solo cuando quieres desplegar en la red principal de Polygon donde la comisión de gas es mucho más baja que Ethereum, alrededor de 1/100 de una comisión de transacción que pagas en Ethereum.

## ¿Qué impulsa el uso y la demanda de tokens MATIC? {#what-drives-the-use-and-demand-for-matic-tokens}

Existen dos usos principales del token:

1. El token se utiliza para pagar comisiones de transacciones en la red
2. El token se utiliza para el apilamiento para participar en el mecanismo de consenso de la prueba de participación para la capa de puntos de verificación y la capa de producción de bloques

**Estos son algunos de los motivos secundarios para la demanda de tokens**:

* La red de Polygon pretende habilitar las aplicaciones descentralizadas para pagar las comisiones de Polygon en las monedas de las aplicaciones descentralizadas, por medio de la abstracción del mecanismo de intercambio de token para el que se utiliza un fondo de liquidez como Kyber. El usuario simplemente utiliza las monedas de las aplicaciones descentralizadas para pagar comisiones, en el fondo, la moneda de las aplicaciones descentralizadas se intercambia por tokens MATIC. Por lo tanto, los desarrolladores de aplicaciones descentralizadas que quieren ofrecer una experiencia de usuario fluida contribuirán a mantener el fondo de liquidez de Polygon.

* A fin de habilitar salidas más rápidas, implementamos un mecanismo de préstamo que utiliza el protocolo Dharma en el que un prestamista o suscriptor puede recibir el token de salida y desembolsar la cantidad de salida con una comisión pequeña de interés. El prestamista luego reclama los tokens después de una semana, utilizando el token de salida. Por lo tanto, el usuario recibe retiros casi inmediatos, mientras que los prestamistas pueden ganar interés por el servicio que prestan.

**Quema de token a nivel del protocolo**

Pretendemos quemar un porcentaje de la comisión de la transacción por cada bloque. Esto hace que los tokens sean deflacionarios por naturaleza y le proporcionamos un soporte constante en términos de valor a nivel del protocolo.

**Baja barrera de entrada (y, por lo tanto, mayores posibilidades de adopción rápida)**

Nos apoyaremos profundamente en las aplicaciones descentralizadas para lograr la adopción del usuario final. Una de las funciones clave es que mantenemos una arquitectura que es totalmente compatible con el ecosistema de desarrollo de Ethereum, es decir, todos los contratos inteligentes, billeteras, IDE, herramientas para operaciones de desarrollo, etc. son directamente compatibles con Polygon. Cualquiera de las aplicaciones descentralizadas de Ethereum se pueden trasladar a Polygon, casi sin cambios significativos. De manera que, las barreras de entrada para los desarrolladores de Ethereum existentes para la transición a Polygon son insignificantes, lo que puede impulsar una adopción masiva de las aplicaciones descentralizadas. Esto ofrece el potencial de aportar más demanda orgánica debido a los efectos de la red que se producen en torno a Polygon.


## ¿Tenéis un prototipo o demostración para mostrarle al público? {#do-you-have-prototype-or-demo-to-show-to-the-public-yet}

Sí. La demostración está disponible [aquí](https://www.youtube.com/watch?v=l1vb5pjezJ8)

## ¿Qué es la transacción por segundos? {#what-is-the-transaction-per-seconds}

Actualmente, “una única cadena lateral de Polygon” puede manejar en teoría 2^16 (más de 65 000) transacciones por segundo

## ¿Es del tipo de token ERC-20? {#is-token-type-erc20}

Sí. Y el token mismo también se aplicará a la cadena de MatPolygonic también, es decir, sin necesidad de pasar a un token nativo en el futuro

## ¿Tenéis un plazo para el lanzamiento de Alpha Mainnet? {#do-you-have-a-timeline-on-the-alpha-mainnet-launch}

Muy probablemente el tercer trimestre o principios del cuarto.

## ¿Podríais describir vuestros planes, cuán avanzados estáis con el desarrollo y cuándo esperáis lanzar una implementación de MATIC en funcionamiento? {#could-you-outline-your-roadmap-how-far-are-you-with-development-and-when-do-you-expect-a-live-implementation-of-matic-to-be-launched}

Ya tenemos una implementación en funcionamiento. Recientemente, la hemos subido a YouTube. Además, llevamos a cabo Consensys BSIC en Mumbai, en cuya ocasión demostramos Polygon en la red de prueba de Kovan.
 En términos de planes, pronto los publicaremos en forma detallada.

## ¿Cuál es la TPS prevista que aportaréis a la red de Ethereum? ¿Qué estáis ejecutando ahora en la red de prueba? {#what-is-the-expected-tps-you-ll-be-able-to-bring-to-the-ethereum-network-what-are-you-running-at-now-on-testnet}

Una única cadena lateral tiene la capacidad de 2^16 (más de 65 000) transacciones por segundo. Polygon tiene la capacidad de agregar múltiples cadenas laterales, pero en la actualidad, nuestro enfoque estaría en estabilizar la red con una cadena lateral.

## “Elegimos Ethereum como la primera plataforma en mostrar nuestra escalabilidad” ¿A qué otras plataformas apuntáis en el futuro? ¿Existe un plazo de implementación? {#we-have-chosen-ethereum-as-the-first-platform-to-showcase-our-scalability-what-other-platforms-are-you-aiming-toward-and-is-there-a-timeline-for-implementation}

Poner en funcionamiento nuestra red principal Ethereum es la primera prioridad por el momento. Cuando logremos una implementación estable de nuestra red de prueba, anunciaremos nuestros planes para otras cadenas de bloques.

## “También tenemos previsto lanzar la versión alpha de nuestra red principal con aplicaciones descentralizadas en funcionamiento antes de la venta de tokens”. {#we-also-intend-to-launch-the-alpha-version-of-our-mainnet-with-working-dapps-before-the-token-sale}

La información de nuestros socios es confidencial por el momento. Pronto lo haremos público. Contaremos con 4 equipos que creen sus soluciones en Polygon. Uno de ellos es una billetera bancaria de India, uno del segmento de videojuegos, uno de marketing de recomendación (que publicará acerca de Polygon en su documentación técnica) y uno en la red de anuncios. Existen otros en preparativos, pero todavía no está finalizado.

## ¿Tenéis un plazo para la venta de tokens? ¿Tenéis información acerca de estas aplicaciones descentralizadas? {#do-you-have-a-timeline-on-the-token-sale-any-information-on-these-dapps}

Por el momento, también los detalles relacionados con la venta de token es confidencial.
