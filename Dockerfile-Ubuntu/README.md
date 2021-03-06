Configuracion de los Dockerfile
--------------------
Para utilizar este directorio se creó la carpeta Dockerfile para la creación de la imagen
la cual permitirá crear los contenedores de docker y el archivo **authorized_keys**
para la Configuracion de la autenticacion por llaves en el servicio SSH de cada contedenor.

Crear Contenedor
---------------------

Para este paso ya hemos creado la imagen entonces configuraremos el HOST anfitrion para la identificación correcta de estos.

Para ello realizaremos los siguientes pasos:

Paso 1. Creación de la imagen en la que se basará el contenedor.
--------------------------
Se ejecuta el siguiente comando para la realización del pasos

```
$ docker build -t server .
```

Y tenemos creado nuestra imagen con CentOS 6 y ssh activo.

Paso 2. Creacion de contenedores.
-------------------------------
Se van a utilizar 2 contenedores, los cuales serán nuestos hosts en el sistema, por lo tanto para poder realizar la conexion correcta con los contenedores, se les debe configurar un *alias* a cada uno, pero antes se deben crear con las siguientes instrucciones:

```
Nombre del contenedor main = server_main

$ docker run -d -P --name ubuntu_main -p 2221:22 -p 80:80 server

Nombre del contenedor mysql = ubuntu_db

$ docker run -d -P --name ubuntu_db -p 2222:22 -p 3306:3306 server
```

Luego de esto registramos los alias con el siguiente comando

` $ echo "127.0.0.1 ubuntu_main ubuntu_db" | sudo tee -a /etc/hosts `

Y con esto contamos con los contenedores creados y con posibilidad de identificación.

Conexion por SSH 
-----------------------------
En este paso configuraremos el HOST anfitrion para la conexion por SSH con los contenedores de docker, siguiendo los siguientes pasos

Paso 3. Configuracion de la llave privada.
-----------------------------------------
Para realizar nuestra conexion nuestra llave privada debe contar con los permisos de esta forma **[-xw-------]** lo que equivale a **0600**.

Por tal razon ejecutamos el siguiente comando

```
$ chmod 0600 ../ansible-to-migrate/llaves/key

```

