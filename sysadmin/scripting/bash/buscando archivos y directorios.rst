Buscando archivos y directorios
-------------------------------

Diferencias
###########

:source:`find(1)` a diferencia de :source:`locate(1)` es un comando que busca a tiempo real y tiene muchísimas funcionalidades añadidas como filtrar por nombre, tipo de ejecutable, fecha, hora.... e incluso, eliminar los ficheros que hemos querido encontrar, mientras que :source:`locate(1)` trabaja junto con una base de datos generada por :source:`updatedb(8)` reduciendo drásticamente la actualización puntera de la ubicación de los ficheros y directorios además de no tener la afinidad que posee :source:`find(1)`.

.. image:: https://asciinema.org/a/182400.png
   :target: https://asciinema.org/a/182400

Trabajando con find(1)
######################

En este artículo vamos a guiarnos más por los ejemplos que por explicar la sintaxis o los parámetros de uno en uno.

Encontrar todos aquellos ficheros y directorios que se encuentren en el directorio :source:`/etc`, y que aquellos directorios a los que no no podamos acceder a su contenido, no nos muestre el error de permisos.

.. code-block:: bash

  find /etc 2>/dev/null

Encontrar todos aquellos archivos en :source:`/var/` cuya extensión sea .log, y que por supuesto, no muestre aquellos directorios que requieran permisos para su acceso.

.. code-block:: bash

  find /var -name "*.log" 2>/dev/null

Mostrar todos los directorios de nuestro :source:`/home` sin contar los archivos

.. code-block:: bash

  find ~ -type d

Encontrar archivos vacíos en nuestro :source:`/home` y eliminarlos todos

.. code-block:: bash

  find ~ -empty -type f -exec rm -rf {} \;

Encontrar ficheros con extensión .log y copiarlos en una carpeta dentro de nuestro home con permisos de superusuario

.. code-block:: bash
  
  sudo find /var -name ".log" -exec cp {} /home/sincorchetes/LOGS \;

Buscando archivos cuya fecha de modificación sea de hace un minuto en nuestro :source:`/home`

.. code-block:: bash

  find ~ -cmin 1 

Ficheros que han sido accedidos hace 10 minutos

.. code-block:: bash

  find ~ -amin 10

Visualizar archivos que contengan .log de extensión, contengan permisos 644

.. code-block:: bash

  sudo find /var -name "*.log" -perm 644

Ver archivos que pesen igual o redondeando den 2GB en nuestro directorio

.. code-block:: bash

  find ~ -size 2G

Buscar directorios que contengan nuestro nombre de usuario, con permisos 777.

.. code-block:: bash

  find / -user sincorchetes -type d -perm 777

Mostrar todos los archivos o directorios simbólicos que se encuentren en el directorio :source:`/dev` y mostrarlo como si ejcutásemos un :source:`ls(1)`

.. code-block:: bash

  sudo find /dev -type l -ls

Listando aquellos archivos de nuestro :source:`/home` cuya extensión contenga "*.avi" y sean iguales o superiores a 1G

.. code-block:: bash

  find ~ -name "*.avi" -a -size 1G

Suprimiendo los .rpm que encontremos que lleguen a 10 megas

.. code-block:: bash

  sudo find /var/cache/rpm -name "*.rpm" -a -size 10M -exec rm -rf {} \;

Podemos seguir ejemplos del manpages de :source:`find(1)` o imaginarnos lo que se nos ocurra que podamos hacer en un futuro, estos son solo pequeños ejemplos de lo que podemos hacer con esta fantástica utilidad.

Trabajando con locate(1)
########################


Bien, como hemos dicho anteriormente, este comando hace uso de una base de datos que por lo general suele ubicarse en :source:`/var/lib/mlocate/mlocate.db`, y su fichero de configuración suele encontrarse en :source:`/etc/updatedb.conf` todo depende de la distribución que utilicemos.

También podemos hacer un indexado que es registrar todos los archivos y directorios que queramos y se almacenen por un cierto orden en la base de datos de locate, sin tener que hacer uso de superusuario o creando un daemon en el sistema.

Regenerando las bases de datos
******************************

Podemos hacer que nos indexe todo lo que contenga el sistema y que lo puedan ver tod@s l@s usuari@s.

.. code-block:: bash

  sudo updatedb

O bien, podemos generar una base de datos para nosotr@s.

.. code-block:: bash

  mkdir .locateupdatedb -l 0 -U /DIR -o .locate/db_file

* :source:`-l 0`: Permite entre otras cosas, crear el fichero de la base de datos utilizando nuestro usuario.
* :source:`-U /DIR`: Directorio a idnexar
* :source:`-o nombre_fichero`: El nombre que le pondremos a la db

Si queremos añadir más directorios, tendremos que ejecutar el comando modificando :source:`/DIR`

Buscando archivos o directorios
*******************************

Basta con ejecutar :source:`locate nombre_archivo/nombre_dir` y el comando nos arrojará una salida completa con las coincidencias que encuentre en la db.

Sin embargo, si queremos ejecutar nuestro fichero, tendremos que especificárselo a :source:`locate(1)`

.. code-block:: bash

  locate nombre_directorio/nombre_archivo -d .locate/db_file

Visualizando estadísticas
*************************

Se pueden ver cuántos archivos y directorios tenemos actualmente registrados en cada db.

.. code-block:: bash

  locate -S 

ó 

.. code-block:: bash

  locate -Sd .locate/db_file

El comando whereis(1)
#####################

Este comando nos viene de fábula cuando queremos encontrar algún binario, archivo fuente o incluso páginas de manual de :source:`man(1)`, para hacerlo, este lleva una búsqueda en aquellos directorios que se encuentren declarados en la variable :source:`$PATH` y :source:`$MANPATH`. Estas variables las podemos encontrar en :source:`/etc/profile` o en :source:`~/.bash_profile`
 (en nuestro caso)

.. code-block:: bash

  echo $PATH

Nuestra salida:

.. code-block:: bash

  echo $PATH/usr/lib/qtchooser:/usr/local/bin:/usr/bin:/bin:/usr/local/sbin:/usr/sbin:/home/sincorchetes/.composer/vendor/bin:/home/sincorchetes/.local/bin:/home/sincorchetes/bin:/home/sincorchetes/.bin/scripts

Vamos a visualizar un par de ejemplos.

Buscando una página con la coincidencia cat(1)
**********************************************

.. code-block:: bash
whereis -m cat

Encontrando la ubicación del binario
************************************

.. code-block:: bash
whereis -b cat

Buscando la fuente de un kernel de Fedora 28
********************************************

.. code-block:: bash
whereis -s 4.16.8-300.fc28.

Comando whatis(1)
#################

Este comando nos permite buscar en las páginas de :source:`man(1)` y nos devuelve una descripción del mismo en una sola línea, en caso de que encuentre varios resultados, mostrará ambos o más y su categoría dentro de :source:`man(1)`.

.. code-block:: bash

  whatis cat

Salida:

.. code-block:: bash

  cat (1p)             - concatenate and print filescat (1)              - concatenate files and print on the standard output

Podemos especificar un directorio diferente para que busque en otras páginas de :source:`man(1)` pues que no tengamos instaladas en el directorio raíz o no se encuentren registradas en :source:`~/.bash_profile`

.. code-block:: bash

  whatis -M ~/.man/ cat

Entre otras cosas

Comando apropos(1)
###################

Este comando es parecido al anterior, lo que utiliza directamente :source:`mandb(1)`, también permite utilizar otra ruta de directorio para los manpages...etc

.. code-block:: bash

  apropos whatis

Salida:

.. code-block:: bash

  whatis (1)           - display one-line manual page descriptions

Referencias
###########

* manpages
  * :source:`find(1)`
  * :source:`locate(1)`
  * :source:`updatedb(1)`
  * :source:`whereis(1)`
  * :source:`whatis(1)`
  * :source:`apropos(1)`

 
