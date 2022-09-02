# INTRODUCCION A SERVERLESS

Este repositorio contiene codigo referente a mi primer proyecto usando el framework serverless y el cual sera desplegado en <abbr title="Amazon Web Services">AWS</abbr> Lambda.

## CREDENCIALES DE <abbr title="Amazon Web Services">AWS</abbr>

Antes de seguir, vamos a generar las credenciales en <abbr title="Amazon Web Services">AWS</abbr>, para lo cual, vamos a:

1. Iniciar sesion en la [Consola de <abbr title="Amazon Web Services">AWS</abbr>](https://console.aws.amazon.com/console/home?region=us-west-2 "https://console.aws.amazon.com/console/home?region=us-west-2").
2. A continuacion vamos a ingresar a la seccion de "**[Credenciales de Seguridad](https://us-east-1.console.aws.amazon.com/iam/home?region=us-west-2#/security_credentials "https://us-east-1.console.aws.amazon.com/iam/home?region=us-west-2#/security_credentials")**".
3. Seleccionamos el apartado de **Claves de Acceso (*Access Keys*)**.
4. Y damos click en el boton de "**Crear una clave de acceso**".
5. <abbr title="Amazon Web Services">AWS</abbr> nos entregara una clave de acceso que esta compuesta de un ID y de una clave que tendran una estructura como esta:
    - **ID de clave de acceso:** *AKNYQRTNXOMSL3MNT7PF*
	- **Clave de acceso secreta:** *KARTHY0Sp+0GQjmCA0987Pj8j7kvXvxUosCTxAtjS*
6. Nos dará la opcion de descargar esta clave en un archivo CSV, podemos descargarlo o simplemente copiar y pegar estas credenciales en un lugar seguro.

## INSTALACION DEL CLI DE SERVERLESS

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

# o utilizando la manera abreviada
$ sls --help
```

Ahora vamos a agregar las credenciales de <abbr title="Amazon Web Services">AWS</abbr>, que generamos en un paso anterior, a nuestro computador usando el <abbr title="Command Line Interface">CLI</abbr> de <abbr title="Serverless Framework">Serverless</abbr> de la siguiente manera:

```bash
$ serverless config credentials --provider aws --key AKIAIOSFODNN7EXAMPLE --secret wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
```

> Reemplaza los datos de "**--key**" y de "**--secret**" por las credenciales que generaste en la consola de <abbr title="Amazon Web Services">AWS</abbr>

> En caso de que necesites utilizar mas de un perfil en el <abbr title="Command Line Interface">CLI</abbr> de <abbr title="Amazon Web Services">AWS</abbr> puedes revisar esta documentacion [Named profiles for the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html "https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html")


## HOLA MUNDO CON SERVERLESS

Ahora vamos a crear nuestro Hola Mundo con Serverless, para lo cual vamos a crear un nuevo directorio dentro de nuestro directorio de trabajo, para este ejemplo lo vamos a llamar hola-mundo, y luego ingresamos al nuevo directorio.

```bash
$ mkdir hola-mundo

$ cd hola-mundo
```

Ahora vamos a crear el proyecto de <abbr title="Serverless Framework">Serverless</abbr> utilizando su <abbr title="Command Line Interface">CLI</abbr> de la siguiente manera:


```bash
$ sls create -t aws-nodejs -n proyecto-sls-hola-mundo
```

El comando anterior consta de lo siguiente:

- **sls:** Es la abreviacion de "serverless", sirve para empezar a utilizar todo el <abbr title="Command Line Interface">CLI</abbr> del framework
- **create:** Para indicarle al <abbr title="Command Line Interface">CLI</abbr> que queremos crear un nuevo proyecto
- **-t:** Es la abrebiación de *"--template"*, y sirve para definir el template que vamos a utilizar
- **aws-nodejs:** Le indicamos al <abbr title="Command Line Interface">CLI</abbr> que cree un proyecto utilizando el template de aws-nodejs
- **-n:** Es la abrebiación de *"--name"* y sirve para asignarle un nombre a nuestro servicio
- **proyecto-sls-hola-mundo:** Es simplementa el nombre que decidi ponerle al proyecto para este ejemplo.

Luego de la ejecución del comando, veremos un mensaje como el siguiente:

```bash
✔ Project successfully created in "./" from "aws-nodejs" template (4s)
```

Por último vamos a realizar el despliegue en el servicio **Lambda** de <abbr title="Amazon Web Services">AWS</abbr> uilizando el siguiente comando:

```bash
$ sls deploy
```

> **NOTA:** En caso de tener mas de un perfil de <abbr title="Amazon Web Services">AWS</abbr> configurado, podemos hacer el despliegue utilizando el comando deploy de la siguiente manera:
    
    $ sls deploy --aws-profile devProfile


Obtendremos un mensaje parecido al siguiente:

```bash
Deploying proyecto-sls-hola-mundo to stage dev (us-east-1)

✔ Service deployed to stack proyecto-sls-hola-mundo-dev (99s)

functions:
  hello: proyecto-sls-hola-mundo-dev-hello (392 B)

Want to ditch CloudWatch? Try our new console: run "serverless --console"
```

En <abbr title="Amazon Web Services">AWS</abbr>, se generará una funcion con el nombre **proyecto-sls-hola-mundo-dev-hello**, esto debido a que nosotros le pusimos el nombre de *"proyecto-sls-hola-mundo"*, y se concatenó el entorno o stage y el nombre de la funcion, datos que estan configurados por defecto en el archivo **"serverless.yml"**.

Para probar nuestra funcion vamos a ejecutar el siguiente comando:

```bash
$ sls invoke -f hello -s dev
```

Este comando consta de:

- **sls:** Abreviacion de *"serverless"*, con esto accedemos al <abbr title="Command Line Interface">CLI</abbr> del framework.
- **invoke:** Parámetro para realizar la invocacion de la funcion que vamos a probar
- **-f hello:** Este parámetro sirve para identificar la funcion que vamos a ejecutar, en este caso la funcion que vamos a probar se llama *"hello"*
- **-s dev:** Por último, este parámetro nos indica que vamos a ejecutar la funcion en el stage dev que es el stage en el que se desplegó nuestra función.

> **NOTA:** En caso de tener mas de un perfil de <abbr title="Amazon Web Services">AWS</abbr> configurado, podemos hacer la prueba de la funcion utilizando el comando invoke de la siguiente manera:
    
    $ sls invoke -f hello -s dev --aws-profile devProfile


> **NOTA:** Para probar la funcion en nuestro entorno local, vamos a ejecutar el comando de la siguiente manera:
    
    $ sls invoke local -f hello -s dev