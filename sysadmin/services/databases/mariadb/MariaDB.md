# MariaDB

## Instalación

## Exportando base de datos

* Todas las bases de datos en formato plano

  ```bash
  mysqldump -u root --all-databases -p  > dump.sql
  ```

  * `-u root`: Usuario root

  * `--all-databases`: Todas las bases de datos

  * `-p`: Pregunta por la contraseña

  * `>` : Redirige el flujo hacia el fichero salida `dump.sql` 

* Especificando las bases de datos

  ```bash
  mysqldump -u root -p --databases [db1 db2 db3] > dump.sql
  ```

  * `-u root`: Usuario root
  * `--databases []`: Las bases de datos que queremos exportar

  * `-p`: Pregunta por la contraseña

  * `>` : Redirige el flujo hacia el fichero salida `dump.sql`

## Importando la base de datos

* Todas las bases de datos en formato plano

  ```bash
  mysqldump -u root -p  < dump.sql
  ```

  * `-u root`: Usuario root

  * `-p`: Pregunta por la contraseña

  * `<` : Redirige el flujo del fichero salida ` dump.sql` hacia el sistema gestor de base de datos

* Una base de datos

  ```bash
  mysqldump -u root -p [basededatos1] < dump.sql
  ```

  * `-u root`: Usuario root

  * `-p`: Pregunta por la contraseña
  * `[basededatos1]`: El nombre de la base de datos a restaurar

  * `<` : Redirige el flujo del fichero salida ` dump.sql` hacia el sistema gestor de base de datos