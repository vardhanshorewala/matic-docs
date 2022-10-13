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
| CPU |  | <ul><li></li><li></li><li>Límite de gas del bloque</li><li>Tiempo del bloque</li></ul> |
|  |  | <ul><li></li><li></li><li>Límite de gas del bloque</li></ul> |
|  | <ul><li></li><li></li></ul> | <ul><li></li></ul> |


##  {#service-configuration}




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

###  {#binary}



:::



###  {#data-storage}




###  {#log-files}



:::


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




###  {#additional-dependencies}



##  {#maintenance}



###  {#backup}





*


*





###  {#logging}


-
-



:::info

:::
###  {#os-security-patches}



##  {#metrics}

###  {#system-metrics}





|  |  |
|-----------------------|-------------------------------|
|  |  |
|  |  |
|  |  |
|  |  |

###  {#validator-metrics}







-
-
-

##  {#security}



###  {#api-services}

-

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
