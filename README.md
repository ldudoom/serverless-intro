# INTRODUCCION A SERVERLESS

Este repositorio contiene codigo referente a mi primer proyecto usando el framework serverless y el cual sera desplegado en AWS Lambdas.

#### Credenciales de AWS

Antes de seguir, vamos a generar las credenciales en AWS, para lo cual, vamos a:

1. Iniciar sesion en la [Consola de AWS](https://console.aws.amazon.com/console/home?region=us-west-2 "https://console.aws.amazon.com/console/home?region=us-west-2").
2. A continuacion vamos a ingresar a la seccion de "**[Credenciales de Seguridad](https://us-east-1.console.aws.amazon.com/iam/home?region=us-west-2#/security_credentials "https://us-east-1.console.aws.amazon.com/iam/home?region=us-west-2#/security_credentials")**".
3. Seleccionamos el apartado de **Claves de Acceso (*Access Keys*)**.
4. Y damos click en el boton de "**Crear una clave de acceso**".
5. AWS nos entregara una clave de acceso que esta compuesta de un ID y de una clave que tendran una estructura como esta:
    - *ID de clave de acceso:* AKNYQRTNXOMSL3MNT7PF
	- *Clave de acceso secreta:* KARTHY0Sp+0GQjmCA0987Pj8j7kvXvxUosCTxAtjS
6. Nos dará la opcion de descargar esta clave en un archivo CSV, podemos descargarlo o simplemente copiar y pegar estas credenciales en un lugar seguro.

## INSTALACION

A continuación vamos a explicar los pasos para realizar la instalacion del framework para, posteriormente, iniciar el desarrollo del pequeño proyecto que se va a construir.

Para eso vamos a seguir las [instrucciones de instalacion](https://www.serverless.com/framework/docs/getting-started "https://www.serverless.com/framework/docs/getting-started") que se encuentran en el sitio oficial de Serverless.

Por lo que, el primer comando que vamos a ejecutar es:

```bash
$ sudo npm install -g serverless
```

Con este comando se instaló de manera global en nuestro equipo el <abbr title="Command Line Interface">CLI</abbr> de Serverless. Por ese motivo ejecutamos el comando anterior como **"sudo"**

Ahora ya podemos utilizar los comandos de serverless, de la siguiente manera por ejemplo:

```bash
$ serverless --help

# o utilizando la manera abrebiada
$ sls --help
```

Ahora vamos a agregar las credenciales de AWS, que generamos en un paso anterior, a nuestro computador usando el <abbr title="Command Line Interface">CLI</abbr> de <abbr title="Serverless Framework">Serverless</abbr> de la siguiente manera:

```bash
$ serverless config credentials --provider aws --key AKIAIOSFODNN7EXAMPLE --secret wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
```

> Reemplaza los datos de --key y de --secret por las credenciales que generaste en la consola de AWS

> En caso de que necesites utilizar mas de un perfil en el CLI de AWS puedes revisar esta documentacion [Named profiles for the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html "https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html")
