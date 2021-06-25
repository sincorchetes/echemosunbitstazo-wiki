Zabbix
------

Software de monitorización elaborado en PHP....

Instalación en CentOS 8
#######################

Actualizar el sistema
*********************

.. code-block:: bash

  dnf upgrade

Instalar el repositorio
***********************

.. code-block:: bash

  rpm -Uvh https://repo.zabbix.com/zabbix/5.0/rhel/8/x86_64/zabbix-release-5.0-1.el8.noarch.rpm
  dnf clean all 

Instalar el software necesario
******************************

.. code-block:: bash

  dnf install zabbix-server-mysql zabbix-web-mysql zabbix-nginx-conf zabbix-agent mariadb-server

Configurando por primera vez la base de datos
*********************************************

Habilitando al arranque y arrancando MariaDB
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  systemctl enable --now mariadb.service


Configurando la base de datos
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. note::

  Solo hay que seguir los pasos.

.. code-block:: bash

  mysql_secure_installation

Configurando la base de datos para Zabbix
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: sql

  mysql
  mysql -u root -p
  mysql> CREATE DATABASE zabbix CHARACTER SET utf8 COLLATE utf8_bin;
  mysql> CREATE USER zabbix@localhost identified BY 'AQUI_UNA_CONTRASEÑA';
  mysql> GRANT ALL PRIVILEGES ON zabbix.* TO zabbix@localhost;
  mysql> QUIT; 

Importando el esquema de base de datos
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  zcat /usr/share/doc/zabbix-server-mysql*/create.sql.gz | mysql -u zabbix -p AQUI_UNA_CONTRASEÑA 


Configurando la base de datos para el servidor
**********************************************

Editar el archivo :code:`/etc/zabbix/zabbix_server.conf` y cambiar la contraseña de BBDD:

.. code-block::
  
  DBPassword=AQUI_UNA_CONTRASEÑA


Editar archivo :code:`/etc/nginx/conf.d/zabbix.conf`
****************************************************

.. note::
  
  Descomentar y configurar las directivas :code:`listen` y :code:`server_name`

.. code-block::
  
  # listen 80;
  # server_name example.com; 


Escoger el huso horario :code:`/etc/php-fpm.d/zabbix.conf`
**********************************************************

.. code-block:: php

  php
  php_value[date.timezone] = Atlantic/Canary 


Arrancando y habilitando Zabbix en el sistema
*********************************************

.. code-block:: bash

  systemctl enable --now zabbix-server.service zabbix-agent.service nginx.service php-fpm.service


Accediendo al portal de configuración
*************************************

Accedemos mediante el dominio que hemos configurado anteriormente:

* Usuario: Admin
* Contraseña: zabbix

Let's Encrypt
#############

Instalar el software necesario
******************************

.. code-block:: bash

  dnf install epel-release
  dnf install certbot python3-certbot-nginx

.. note::

  Teniendo el dominio apuntando al servidor y certificando en `DNS Checker <https://dnschecker.org>`_ que el resultado del registro es la IP del dominio, procedemos a generar el certificado.

Generando el certificado
************************

.. code-block:: bash

  certbot --nginx -d DOMINIO -m TU_EMAIL --agree-tos --non-interactive

Reiniciando el servidor web
***************************

.. code-block:: bash

  systemctl restart nginx.service


Ya tendremos nuestro servidor web protegido via SSL.

Firewalld
#########

Instalar firewalld
******************

.. code-block:: bash

  dnf install firewalld

Habilitando al arranque e iniciándolo
*************************************

.. code-block:: bash

  systemctl enable --now firewalld.service


Abriendo los puertos para Zabbix
********************************

.. code-block:: bash

  firewall-cmd --add-service http --add-service https --zone public --permanent
  firewall-cmd --reload

Procedimiento de backup
#######################

Exportar todas las bases de datos
*********************************

.. code-block:: bash

  mysqldump -u root --all-databases -p  > dump-$(date +%d-%m-%y).sql

  * :code:`-u root`: Usuario root
  * :code:`--all-databases`: Todas las bases de datos
  * :code:`-p`: Pregunta por la contraseña
  * :code:`>` : Redirige el flujo hacia el fichero salida :code:`dump-$(date +%d-%m-%y).sql` 

Comprimir los directorios esenciales
************************************

.. code-block:: bash

  tar zcfv /root/zabbix-$(date +%d-%m-%y).tar.gz /etc/zabbix /usr/share/zabbix --acls --xattrs --selinux


