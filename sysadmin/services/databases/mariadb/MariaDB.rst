MariaDB
----

Instalación
####

Exportando base de datos
####

* Todas las bases de datos en formato plano

  .. code-block:: bash
    mysqldump -u root --all-databases -p  > dump.sql

  * :code:`-u root`: Usuario root
  * :code:`--all-databases`: Todas las bases de datos
  * :code:`-p`: Pregunta por la contraseña
  * :code:`>` : Redirige el flujo hacia el fichero salida :code:`dump.sql` 

* Especificando las bases de datos

  .. code-block:: bash
    mysqldump -u root -p --databases [db1 db2 db3] > dump.sql

  * :code:`-u root`: Usuario root
  * :code:`--databases []`: Las bases de datos que queremos exportar
  * :code:`-p`: Pregunta por la contraseña
  * :code:`>` : Redirige el flujo hacia el fichero salida :code:`dump.sql`

Importando la base de datos
####

* Todas las bases de datos en formato plano

  .. code-block:: bash
    mysqldump -u root -p  < dump.sql

  * :code:`-u root`: Usuario root
  * :code:`-p`: Pregunta por la contraseña
  * :code:`<` : Redirige el flujo del fichero salida :code:` dump.sql` hacia el sistema gestor de base de datos

* Una base de datos

  .. code-block:: bash
    mysqldump -u root -p [basededatos1] < dump.sql

  * :code:`-u root`: Usuario root
  * :code:`-p`: Pregunta por la contraseña
  * :code:`[basededatos1]`: El nombre de la base de datos a restaurar
  * :code:`<` : Redirige el flujo del fichero salida :code:` dump.sql` hacia el sistema gestor de base de datos