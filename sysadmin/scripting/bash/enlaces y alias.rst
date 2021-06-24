Enlaces simbólicos o duros y alias
----------------------------------

Alias
#####

Los alias nos permiten reducir la longitud de una sentencia que queramos ejecutar en nuestro sistema y atajarla con una simple palabra. Por ejemplo, si queremos acceder a un directorio muy concurrido desde terminal.

.. code-block:: bash

  cd ~/Documentos/Archivos/2018/05/10/10-11/Sector/1/ficheros_importantes/Codigo054/Area_51/

No nos imaginamos en absoluto tener que teclear toda esta ruta cada vez que queramos acceder al directorio Area_51. Pues podemos generar un alias, a nivel de sistema o a nivel de nuestro usuario.

A nivel de sistema, tenemos que añadirlo en :source:`/etc/bashrc` si es que queremos que ese alias también lo tengan el resto de usuarios o si solo lo queremos para el nuestro, en ese caso, :source:`~/.bashrc` es el que debemos tocar de la siguiente manera:

.. code-block:: bash

  alias nombre_alias='cd ~/Documentos/Archivos/2018/05/10/10-11/Sector/1/ficheros_importantes/Codigo054/Area_51/'

Posteriormente aplicamos los cambios:

.. code-block:: bash

  source /etc/bashrc

o si es a nivel usuario:

.. code-block:: bash

  source ~/.bashrc

Enlaces
#######

Los enlaces vienen a ser lo que en Windows tenemos como "Accesos directos" pero a nivel de terminal, podemos especificar un directorio o un archivo que se encuentre en un directorio X pero teniendo un acceso más rápido en un directorio en el que trabajemos. También tenemos enlaces simbólicos que son accesos que si es borrado el archivo o directorio original solo queda el enlace y por lo tanto, no funciona y no es útil, o tenemos lo que denominamos enlaces duros, en los que se conserva una copia del fichero o directorio.

Simbólicos
**********

Para poderlos generar, simplemente tenemos que hacer uso del comando :source:`ln(1)` con el parámetro :source:`-s` de soft.

.. code-block:: bash
  
  ln -s /directorio_a_enlazar /directorio_donde_quiero_ver_el_enlace

Por ejemplo:

.. code-block:: bash

  ln -s /usr/src ~

Nos genera un enlace simbólico hacia el directorio :source:`/usr/src` de nuestro :source:`/home`.

¿Cómo averiguar si dispongo del enlace simbólico? Cuando hacemos un :source:`ls(1)` para listar documentos y directorios, veremos en una de las líneas de salida un dato similar:

.. code-block:: bash

  lrwxrwxrwx.  1 sincorchetes sincorchetes         9 May 20 17:37  src -> /usr/src/

* "l" al principio de esta entrada identifica un enlace simbólico.
* :source:`src -> /usrc/src`: Nos dice hacia dónde apunta.

Duros
*****

Los enlaces duros permiten crear "una copia" de lo enlazado, de tal forma, que si se destruye el archivo o directorio original contínua funcionando. 

.. code-block:: bash

  ln /directorio_a_enlazar /directorio_donde_quiero_ver_el_enlace

De hecho, si hacemos un :source:`ls(1)`, no veremos añadida una :source:`l` en los permisos o en acceso tipo :source:`src -> /usr/src`.

Referencias
###########

* manpages, :source:`ln(1)` y :source:`ls(1)` 