---
id: set-up-gcp-secrets-manager
title:
description: ""
keywords:
  - docs
  - polygon
  - edge
  - gcp
  - secrets
  - manager
---

## Resumen {#overview}

Actualmente, el Polygon Edge se preocupa por mantener 2 importantes secretos de tiempo de ejecución:
* La **clave privada del validador** utilizada por el nodo, si el nodo es un validador
* La **clave privada de la red** utilizada por libp2p, para participar y comunicarse con otros pares

Para obtener información adicional, lea la [Guía Administrando Claves Privadas](/docs/edge/configuration/manage-private-keys)

Los módulos del Polygon Edge **no deberían saber cómo guardar secretos**. En última instancia, un módulo no debería preocuparse si un secreto se almacena en un servidor lejano o localmente en el disco del nodo.

Todo lo que un módulo necesita saber sobre cómo guardar secretos es **saber usar el secreto**, **saber qué secretos obtener,
 o guardar**. Los detalles de implementación más finos de estas operaciones se delegan lejos del`SecretsManager`, lo cual por supuesto es una abstracción.

El operador del nodo que está comenzando el Polygon Edge ahora puede especificar cual administrador de secretos quiere usar, y que tan pronto como el administrador de secretos correcto es instanciado, los módulos se ocupan de los secretos a través de la interfaz mencionada: sin preocuparse si los secretos se almacenan en un disco o en un servidor.



:::info guías anteriores

Es **altamente recomendable** que antes de pasar por este artículo, artículos sobre [**Configuración Local**](/docs/edge/get-started/set-up-ibft-locally)
 y [**Configuración de la Nube**](/docs/edge/get-started/set-up-ibft-on-the-cloud) se lean

:::


## Requisitos previos {#prerequisites}
###  {#gcp-billing-account}


###  {#secrets-manager-api}


###  {#gcp-credentials}


Información necesaria antes de continuar:
*
*

## Paso 1 Generar la configuración del administrador de secretos {#step-1-generate-the-secrets-manager-configuration}



Para generar la configuración, ejecuta el siguiente comando:

```bash
polygon-edge secrets generate --type gcp-ssm --dir <PATH> --name <NODE_NAME> --extra project-id=<PROJECT_ID>,gcp-ssm-cred=<GCP_CREDS_FILE>
```

Parámetros presentes:
* `PATH` es la ruta a la que se debe exportar el archivo de configuración. Por defecto `./secretsManagerConfig.json`
* Puede ser un valor arbitrario. Por defecto `polygon-edge-node`
*
*

:::caution Nombres de nodos
Ten cuidado cuando especifiques los nombres de los nodos.



Los secretos se almacenan en la siguiente ruta base: `projects/PROJECT_ID/NODE_NAME`

:::

## Paso 2: inicializa las claves secretas usando la configuración {#step-2-initialize-secret-keys-using-the-configuration}

Ahora que el archivo de configuración está presente, podemos inicializar las claves secretas necesarias con la configuración archivo configurado en el paso 1, usando `--config`

```bash
polygon-edge secrets init --config <PATH>
```

El `PATH`param es la ubicación del parámetro del administrador de secretos generado previamente en el paso 1.

## Paso 3: genera el archivo genesis {#step-3-generate-the-genesis-file}

El archivo génesis debe generarse de manera similar a la [**Configuración Local**](/docs/edge/get-started/set-up-ibft-locally)
 y [**Configuración de las guías de la nube**](/docs/edge/get-started/set-up-ibft-on-the-cloud), con cambios menores.


```bash
polygon-edge genesis --ibft-validator <VALIDATOR_ADDRESS> ...
```

## Paso 4: iniciar el cliente Polygon Edge {#step-4-start-the-polygon-edge-client}

Ahora que las claves están configuradas y el archivo génesis está generado, el paso final del proceso estaría comenzando al Polygon Edge con el comando`server`.

El comando `server`se usa de la misma manera que en las guías mencionadas anteriormente, con una pequeña adición - la bandera`--secrets-config`:
```bash
polygon-edge server --secrets-config <PATH> ...
```

El `PATH`param es la ubicación del parámetro del administrador de secretos generado previamente en el paso 1.