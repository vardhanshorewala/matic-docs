---
id: validator-hosting
title: Hosting de validador
description: "Requisitos de hosting para Polygon Edge"
keywords:
- docs
- polygon
- edge
- hosting
- cloud
- setup
- validator
---

A continuación, te acercamos sugerencias Presta especial atención a todos los elementos que se indican abajo para asegurarte
 de que tu configuración de validador se realizó de forma adecuada para que sea segura, estable y eficiente.

## Base de conocimiento {#knowledge-base}

   Antes de intentar ejecutar el nodo validador, lee a fondo este documento.
 Documentos adicionales que podrían resultarte útiles:

- [Instalación](get-started/installation)
- [Configuración en la nube](get-started/set-up-ibft-on-the-cloud)
- [Comandos CLI](get-started/cli-commands)
- Servidor del archivo config
- [Claves privadas](configuration/manage-private-keys)
- Indicadores de Prometheus
- [Secrets manager](/docs/category/secret-managers)
- [Copia de seguridad/restauración](working-with-node/backup-restore)

## Requisitos de sistema mínimos {#minimum-system-requirements}

| Tipo | Valor | Influenciado por |
|------|------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| CPU | 2 núcleos | <ul><li>Número de consultas JSON-RPC</li><li>Tamaño del estado de la cadena de bloques</li><li>Límite de gas del bloque</li><li>Tiempo del bloque</li></ul> |
| RAM | 2 GB | <ul><li>Número de consultas JSON-RPC</li><li>Tamaño del estado de la cadena de bloques</li><li>Límite de gas del bloque</li></ul> |
| Disco | <ul><li>Partición raíz de 10 GB</li><li>Partición raíz de 30 GB CON LVM para extensión del disco</li></ul> | <ul><li>Tamaño del estado de la cadena de bloques</li></ul> |


## Configuración del servicio {#service-configuration}

`polygon-edge`El  binario necesita ejecutarse como un servicio de sistema de forma automática sobre la conectividad de una red establecida y debe tener las funcionalidades
 iniciar/detener/reiniciar. Recomendamos utilizar un service manager como `systemd.`

Ejemplo de archivo de configuración de sistema `systemd`:
```
[Unit]
Description=Polygon Edge Server
After=network.target
StartLimitIntervalSec=0

[Service]
Type=simple
Restart=always
RestartSec=10
User=ubuntu
ExecStart=/usr/local/bin/polygon-edge server --config /home/ubuntu/polygon/config.yaml

[Install]
WantedBy=multi-user.target
```

### Binario {#binary}

En cargas de trabajo de producción el `polygon-edge`binario de solo se debería implementar desde la versión de binarios GitHub preconstruida, no mediante la compilación manual:::info.


Al compilar de forma manual la branch    GitHub  , puede introducir cambios críticos a tu entorno.
 Por esta razón se recomienza desplegar el binario Polygon Edge solo desde versiones, ya que contendrán
 información sobre cambios críticos y sobre cómo superarlos.

:::

Consulta [Instalación](/docs/edge/get-started/installation) para un resumen completo del método de instalación.

### Almacenamiento de datos {#data-storage}

La carpeta `data/` que contiene todo el estado de la cadena de bloques se debe montar sobre un disco o volumen dedicados, lo que permite realizar
 copias de seguridad del disco automáticas, extensión de volumen y montaje opcional del disco/volumen hacia otra instancia en caso de fallo.


### Archivos de registro {#log-files}

Los archivos de registro se deben rotar de forma diaria (con una herramienta como `logrotate`).
:::warning

Si se configurara sin rotación de registro, los archivos de registro podrían utilizar todo el espacio en disco disponible, lo que podría alterar el tiempo de funcionamiento de un validador.

:::

Ejemplo de configuración `logrotate`:
```
/home/ubuntu/polygon/logs/node.log
{
        rotate 7
        daily
        missingok
        notifempty
        compress
        prerotate
                /usr/bin/systemctl stop polygon-edge.service
        endscript
        postrotate
                /usr/bin/systemctl start polygon-edge.service
        endscript
}
```


Consulta la sección [Registro](#logging) que está abajo para acceder a recomendaciones sobre almacenamiento de registro.

### Dependencias adicionales {#additional-dependencies}

`polygon-edge` se compila de forma estadística y no requiere dependencias adicionales del sistema operativo del host.

## Mantenimiento {#maintenance}

A continuación te presentamos las mejores prácticas para mantener un nodo validadorde la red Polygon Edge operativo.

### Copia de seguridad {#backup}

Hay dos tipos de procedimientos de copia de seguridad que se recomiendan para los nodos de Polygon Edge.

La sugerencia es usar ambos, siempre que sea posible, con la copia de seguridad de Polygon Edge como una opción siempre disponible.

* ***Copia de seguridad del volumen***    
 Copia de seguridad incremental diaria del volumen `data/` del nodo Polygon Edge o de la VM, de ser posible.


* ***Copia de seguridad de Polygon Edge***    
   Se recomienda hacer CRON job diarios que generan copias regulares de Polygon Edge y mueven los archivos `.dat` para hacia ubicación fuera del sitio o el almacenamiento de un objeto en la nube seguro.

Es ideal que la copia de seguridad de Polygon Edge no se superponga con la copia de seguridad de volumen que se describió anteriormente.

Consulta [la instancia de nodo copia](working-with-node/backup-restore) de seguridad/restaurar para obtener instrucciones sobre cómo realizar copias de seguridad de Polygon Edge.

### Registro {#logging}

Los registros que se generan mediante Polygon Edge deben cumplir los siguientes requisitos:
- enviarse a un almacén de datos externo con indexación y capacidades de búsqueda
- tener un período de retención de registro de 30 días

Si es la primera vez que configuras un validador Polygon Edge, te recomendamos comenzar el nodo
 con la opción `--log-level=DEBUG` para poder depurar cualquier problema que pueda presentarse.

:::info

El     hará que los el resultado del registro del nodo sea lo más detallado posible. Los registros de depuración aumentaría de forma drástica el tamaño del archivo de registro, por lo que es algo que se debe tener en cuenta a la hora de configurar
 una solución de rotación de registro.

:::
### Parches de seguridad del sistema operativo {#os-security-patches}

Los administradores deben asegurarse de que el sistema operativo de la instancia validadora se actualice siempre con los últimos parches al menos una vez al mes.

## Indicadores {#metrics}

### Indicadores del sistema {#system-metrics}

Es necesario que los administradores configuren algún tipo de monitor del sistema de indicadores (como Telegraf, InfluxDB, Grafana o una aplicación SaaS externa).

Estos son los indicadores que se necesita monitorear y que  deben tener una configuración de las notificaciones de alarma:

| Nombre del indicador | Umbral de alarma |
|-----------------------|-------------------------------|
| Uso de la CPU (%) | > 90 % por más de 5 minutos |
| Utilización de la RAM (%) | > 90 % por más de 5 minutos |
| Utilización del disco raíz | > 90 % |
| Utilización de datos del disco | > 90 % |

### Indicadores de validador {#validator-metrics}

Los administradores deben configurar una serie de indicadores de la API Prometheus de Polygon Edge para poder
 supervisar el rendimiento de la cadena de bloques.

Consulta [Indicadores Prometheus](configuration/prometheus-metrics) para comprender qué métricas se están exponiendo y cómo configurar la serie de indicadores Prometheus.


Se debe prestar atención adicional a los siguientes indicadores:
- ***Tiempo de producción de bloque***: si es mayor que lo normal existe un problema potencial con la red
- ***El número de rondas de consenso***: si hay más de 1 ronda, existe un problema potencial con el conjunto de validadores de la red
- ***Número*** de pares: si el número de pares caen, hay un problema de conectividad en la red

## Seguridad {#security}

A continuación te presentamos las mejores prácticas para asegurar un nodo validador de la red Polygon Edge operativo.

### Servicios API {#api-services}

- ***JSON-RPC*** -
    Solo el servicio API que se necesite exponer al público (

:::


-

:::


-

###  {#polygon-edge-secrets}



##  {#update}



###  {#update-procedure}

-
-
-
-
-
-
-

:::warning





:::

##  {#startup-procedure}



-
-
-
-
-
-
-
-
-
-
-
-
-
