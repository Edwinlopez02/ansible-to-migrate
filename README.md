Creación de una pila LAMP sencilla e implementación de la aplicación mediante Ansible Playbooks.
-------------------------------------------
-Pasos:
-------------------------------------------
Estos Playbooks requieren Ansible 1.2.

Primer Paso: Se necesita generar imagen de los dockers
-------------------------------------------
Estos Playbooks de ejercicios están destinados a ser una guía de referencia y de inicio para la construcción de Playbooks de ejercicios Ansible. Estos Playbooks fueron probados en CentOS 6.x por lo que se recomienda utilizar CentOS o RHEL para probar estos módulos.
------------------------------------------
Segundo Paso: Generamos los Containers de Ubuntu, tales como: 

  [webservers]
  localhost

  [dbservers]
  bienesible
----------------------------------------
Tercer Paso: Se configuran los hosts que se tienen.
----------------------------------------

Cuarto Paso: Se configuran los Ansibles.
---------------------------------------

Aquí el servidor web sería configurado en el host local y el dbserver en un
servidor llamado "bensible". La pila se puede desplegar utilizando las siguientes
mando:

  ansible-playbook -i hosts site.yml

---------------------------------------
Una vez hecho esto, puede comprobar los resultados consultando http: //localhost/index.php.
Debería ver una página de prueba simple y una lista de bases de datos
servidor de base de datos.
