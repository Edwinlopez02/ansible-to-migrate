Creación de una pila LAMP sencilla e implementación de la aplicación mediante Ansible Playbooks.
-------------------------------------------
Pasos:
-------------------------------------------
Estos Playbooks requieren Ansible 1.2.

Paso 1: Se necesita generar imagen de los dockers
-------------------------------------------
Estos Playbooks de ejercicios están destinados a ser una guía de referencia y de inicio para la construcción de Playbooks de ejercicios Ansible. Estos Playbooks fueron probados en CentOS 6.x por lo que se recomienda utilizar CentOS o RHEL para probar estos módulos.

Para esto es necesario crear los dockers personalizados, en los que estan el servidor openssh depende la imagen que se base el contener, para ellos realizaremos el siguiente comando: ``$ (sudo) docker build -t {{ nombre imagen }}.``

Paso 2: Generamos los Containers de Ubuntu, para el despliegue, donde se crearan maquinas de un servidor Web (Apache), y uno de bases de datos (MySQL) 
--------------------------------------------
```
  [webservers]
  ubuntu_main
  
  [dbservers]
  ubuntu_db
  ```
Paso 3: Se configuran los hosts que se tienen.
----------------------------------------
Para esto, se debe editar los hosts adicionando los alias, donde podemos hacerlo de dos formas:
1. ``localhost 127.0.0.1 ubuntu_main ubuntu_db``

2. ``127.0.0.1 ubuntu_main ubuntu_db | sudo tee -a /etc/hosts``

Paso 3: Se le dan los permisos para hacer la conexion con la llave 
---------------------------------------
Se necesita tener una conexion con la llave, para eso debemos darle los permisos necesarios 

``chmod 0600 ../authorized_keys``

Luego de esto, realizamos una prueba de conexion a las maquinas que hemos creado anteriormente, las cuales se crearon en el puerto 2221 y 2222 los cuales, estan abiertos para la conexion:

``ssh root@ubuntu_main -p 2221 -i ../key.private ssh root@ubuntu_db -p 2222 -i ../authorized_keys``

Paso 4: Continuamos con Ansible:
--------------------------------------
Aquí el servidor web sería configurado en el host local y el dbserver en un
servidor llamado "bensible". La pila se puede desplegar utilizando las siguientes
mando:
```
  ansible-playbook -i hosts site.yml
```
---------------------------------------
Una vez hecho esto, puede comprobar los resultados consultando http: //localhost/index.php.
Debería ver una página de prueba simple y una lista de bases de datos
servidor de base de datos.
