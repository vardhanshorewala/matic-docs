---
id: set-up-aws-ssm
title: Configura AWS SSM (administrador de sistemas)
description: "Configura AWS SSM (administrador de sistemas) para Polygon Edge."
keywords:
  - docs
  - polygon
  - edge
  - aws
  - ssm
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

Este artículo detalla los pasos necesarios para que el Polygon Edge se ponga en marcha y se ejecute con [AWS Almacén de parámetros del administrador de sistemas](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html).

:::info guías anteriores

Es **altamente recomendable** que antes de pasar por este artículo, artículos sobre [**Configuración Local**](/docs/edge/get-started/set-up-ibft-locally)
 y [**Configuración de la Nube**](/docs/edge/get-started/set-up-ibft-on-the-cloud) se lean

:::


## Prerrequisitos {#prerequisites}
### Política de IAM {#iam-policy}
El usuario necesita crear una Política de IAM que permita operaciones de lectura/escritura para AWS Almacén de parámetros del administrador de sistemas. Después de crear con éxito la política de IAM, el usuario necesita adjuntarla a la instancia EC2 que está ejecutando el servidor Polygon Edge. La Política de IAM debería verse así:
```json
{
  "Version": "2012-10-17",
  "Statement" : [
    {
      "Effect" : "Allow",
      "Action" : [
        "ssm:PutParameter",
        "ssm:DeleteParameter",
        "ssm:GetParameter"
      ],
      "Resource" : [
        "arn:aws:ssm:<aws_region>:<aws_account_id>:parameter<ssm-parameter-path>*"
      ]
    }
  ]
}
```
Más información en los roles AWS SSM IAM que puedes encontrar en el [AWS docs](https://docs.aws.amazon.com/systems-manager/latest/userguide/setup-instance-profile.html).

Información necesaria antes de continuar:
* **Región** (la región en la que residen los administradores de sistemas y los nodos)
* **Ruta de Parámetro** (ruta arbitraria en la que se colocará el secreto, por ejemplo`/polygon-edge/nodes`)

## Paso 1 Generar la configuración del administrador de secretos {#step-1-generate-the-secrets-manager-configuration}

Para que Polygon Edge pueda comunicarse sin problemas con AWS SSM, necesita analizar un archivo de configuración generado, que contiene toda la información necesaria para el almacenamiento secreto en AWS SSM.

Para generar la configuración, ejecuta el siguiente comando:

```bash
polygon-edge secrets generate --type aws-ssm --dir <PATH> --name <NODE_NAME> --extra region=<REGION>,ssm-parameter-path=<SSM_PARAM_PATH>
```

Parámetros presentes:
* `PATH` es la ruta a la que se debe exportar el archivo de configuración. Por defecto `./secretsManagerConfig.json`
* `NODE_NAME`es el nombre del nodo actual para el que se establece que la configuración de AWS SSM. Puede ser un valor arbitrario. Por defecto `polygon-edge-node`
* `REGION` es la región en que AWS SSM reside. Esta debe ser la misma región en la que el nodo utiliza AWS SSM.
* `SSM_PARAM_PATH` es el nombre de la ruta en la que se almacenará el secreto. Por ejemplo, si`--name node1` y `ssm-parameter-path=/polygon-edge/nodes`
 están especificadas, el secreto se almacenará como `/polygon-edge/nodes/node1/<secret_name>`

:::caution Nombres de nodos
Ten cuidado cuando especifiques los nombres de los nodos.

El Polygon Edge utiliza el nombre del nodo especificado para mantener un registro de los secretos que genera y utiliza en el AWS SSM. Especificar el nombre del nodo existente puede tener consecuencias como la de no poder escribir el secreto en AWS SSM.

Los secretos se almacenan en la siguiente ruta base: `SSM_PARAM_PATH/NODE_NAME`

:::

## Paso 2: inicializa las claves secretas usando la configuración {#step-2-initialize-secret-keys-using-the-configuration}

Ahora que el archivo de configuración está presente, podemos inicializar las claves secretas necesarias con la configuración archivo configurado en el paso 1, usando `--config`

```bash
polygon-edge secrets init --config <PATH>
```

El `PATH`param es la ubicación del parámetro del administrador de secretos generado previamente en el paso 1.

:::info Política de IAM
Este paso fallará si la política de IAM que permite las operaciones de lectura/escritura no está configurada correctamente o no se adjunta a instancia EC2 que ejecuta este comando.
:::

## Paso 3: genera el archivo genesis {#step-3-generate-the-genesis-file}

El archivo génesis debe generarse de manera similar a la [**Configuración Local**](/docs/edge/get-started/set-up-ibft-locally)
 y [**Configuración de las guías de la nube**](/docs/edge/get-started/set-up-ibft-on-the-cloud), con cambios menores.

Dado que se utiliza AWS SSM en lugar del sistema de archivos local, las direcciones de validación deben agregarse a través de la`--ibft-validator` bandera:
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