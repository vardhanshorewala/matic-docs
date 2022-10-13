---
id: validator-hosting
title:
description: ""
keywords:
- docs
- polygon
- edge
- hosting
- cloud
- setup
- validator
---



##  {#knowledge-base}



-
-
-
-
-
-
-
-

##  {#minimum-system-requirements}

|  |  |  |
|------|------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|  |  | <ul><li></li><li></li><li></li><li></li></ul> |
|  |  | <ul><li></li><li></li><li></li></ul> |
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
