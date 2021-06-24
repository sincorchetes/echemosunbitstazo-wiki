Bash
----

¿Qué es Bash?
#############

Bash es un intérprete de comandos también conocido en inglés como una "*shell*" desarrollada el 8 de junio de 1989 por Brian Fox en el lenguaje C como alternativa y mejora de SH (*Bourne Shell*). Hoy en día es multiplataforma ya que puede correr tanto en Linux como en Mac OS X (de hecho es shell por defecto), en Windows mediante `Cygwin https://www.cygwin.com?target=_blank>`_ o mediante la instalación oficial desde su apartado de añadir nuevas características de software.

Actualmente existen multitudes de I.C pero mencionaremos las más destacadas como:

 * csh: C Shell creada por Bill Joy, 1978
 * tcsh: TENEX C Shell desarrollada por Ken Greer, 1981
 * fish: Shell interactiva liberada el 13 de febrero de 2005 por Axel Liljencrantz
 * zsh: Z Shell elaborada por Paul Falstad en 1990
 * ksh: KornShell creada por David Korn en 1983

Cada una de ellas contiene ciertos matices a la hora de desarrollar scripts que son un serie de ficheros que suelen contener comandos e intrucciones adicionales para que se puedan ejecutar sin tener que escribir grandes bloques de comandos, variables...

Entrada/Salida
##############

Las entradas y salidas es algo que debemos tener claro desde el principio. Una entrada se produce cuando introducimos un comando y pulsamos ejecutar o un programa automatizado ejecuta un programa X.

La salida es el resultado producido al ejecutar dicho comando. Más adelante veremos, que podemos trabajar con salidas para que trabajen como entradas y viceversa.

Modificadores
#############

Son las opciones con las que cambiaremos el comportamiento de los comandos y programas. Se identifican con un guión delante de una letra que hace referencia a una modificación.

Por ejemplo, :code:`ls -l` lista todos los nombres de los directorios y de los archivos junto con información adicional como:

* Permisos
* Cantidad de dir hijos que hay dentro del directorio padre incluyendo así mismo y el padre
* Grupo que gestiona el archivo/directorio 
* Usuario propietario
* Nº de inodo
* Fecha de modificación

Sin embargo, un :code:`ls` (que es :code:`ls -a` por defecto), mostrará solo el nombre de los archivos y directorios situados en el dir actual.

.. code-block::

  En artículos posteriores veremos con más profundidad qué son estos parámetros en los archivos.

Trabajando con Bash
###################

A continuación veremos una recopilación de comandos básicos para poder trabajar con nuestra shell antes de poder seguir. Quizás nos pueda parecer un poco abrumador así de entrada todos los comandos, los modificadores, tipos de rutas...etc etc etc. Pero desde Echemos un bitstazo apostamos por el dicho de "la práctica hace al maestro". Y es así, mucho de nosotros que desarrollamos sufrimos una pérdida de memoria cuando dejamos de hacerlo. Así que... ¡Ha llegado la hora de practicar!

Directorios y archivos
**********************

En este apartado veremos como trabajar con los directorios dentro del sistema. Tenemos que tener en cuenta, de que la arquitectura estandar del sistema de ficheros en Linux (FHS) está organizada en modo de árbol. Esto quiere decir que todo cuelga de un directorio raíz llamado (/), del que cuelga el resto de ellos.

.. note:: 
  
  Comentaremos los directorios más básicos y relevantes para este artículo, ya que debe dedicársele un post solamente para explicar qué funciones realiza cada directorio del sistema.**

El directorio dónde por defecto se generan las carpetas para los nuevos usuarios del sistema se encuentra ubicado en :code:`/home`. Por defecto, nuestra shell nos sitúa en el directorio principal de nuestro usuario, con lo que no tendremos que desplazarnos a niveles superiores dentro del sistema de archivos.

Archivos ocultos
****************

Los archivos ocultos se representan por llevar un :code:`.` como prefijo al nombre del archivo o directorio y no aparecerán listados con ningún comando por defecto. No necesita ningún tipo de modificador adicional para generarlos o para leerlos.

Rutas absolutas y relativas
***************************

Las rutas absolutas son aquellas que contienen la dirección completa dentro de la jerarquía del sistema de archivos.
:code:`/home/sincorchetes/Videos/Echemosunbitstazo/capitulo1.ogg`

Mientras que las rutas relativas, solo contienen una dirección breve que se muestra desde la propia carpeta. Imaginemos que estamos en el directorio :code:`/home/sincorchetes/` y queremos llegar hasta el :code:`capitulo1.ogg`. Para ello tendríamos que apuntar de la siguiente manera:
:code:`Echemosunbitstazo/capitulo1.ogg` ó bien :code:`./Echemosunbitstazo/capitulo1.ogg`

Escalado entre directorios
**************************

Nosotros podemos aprovecharnos de algunos "alias" que nos provee la shell para agilizar la gestión o administración de directorios haciendo uso de las rutas relativas. Estos son algunos trucos:

* :code:`.`: Significa, el directorio actual. :code:`ls .` devuelve una salida en la que mostrará todos los directorios y archivos en el directorio actual
* :code:`..`: Sube un nivel superior, :code:`ls ..` mostrará los directorios y archivos del directorio padre.

Obtener la ruta del directorio actual
*************************************

Si queremos saber en qué directorio nos encontramos actualmente, bastará con ejecutar el comando:

.. code-block :: bash
  
  $ pwd

:code:`pwd(1)` proviene del inglés "print name of current/working directory", imprimir el nombre del directorio actual.

Creando un directorio
*********************

Con el siguiente comando generamos un directorio nuevo sin ningún tipo de contenido. Existe una sintaxis para crear directorios.
No se puede empezar por caracteres especiales, aunque, dentro de los caracteres especiales se puede utilizar el espacio, pero se puede utilizar números, mayúsculas o minúsculas.

.. code-block:: bash

  $ mkdir nombre_directorio

.. note::

  En caso de que queramos crear un subdirectorio sin existir primero el directorio padre, nos dará error si lo ejecutamos tal cual. Para ello, deberemos aplicar la opción :code:`-p`.

Desplazarnos entre directorios
******************************

Para poder desplazarnos entre directorios tenemos dos formas de hacerlo, mediante el comando UNIX por excelencia :code:`cd(1)` o :code:`pushd(1)` y :code:`popd(1)`.

Desplazándonos con :code:cd(1)
******************************

Simplemente deberemos ejecutar el comando y la ruta ya sea relativa o absoluta a la que queramos acceder como en los siguientes ejemplos:

* Situándonos en el directorio raíz del sistema: :code::code:`cd /`
* Subiendo un nivel del directorio actual: :code:`cd ..`
* Accediendo a :code:`/usr/local/share`: :code:`cd /usr/local/share`

Desplazándonos mediante pushd(1) y popd(1)
******************************************

Uno de estos comandos tienen la ventaja de almacenar en la sesión de :code:`bash(1)` actual el directorio y además, nos ubica en él como es el caso de :code:`pushd(1)`. Mientras que :code:`popd(1)`, nos permite volver hacia atrás en caso de no querer seguir estando en él.

Moviéndonos al directorio raíz:

.. code-block:: bash

  $ pushd .themes/
  ~/.themes ~
  $ pwd
  /home/sincorchetes/.themes

Volviendo hacia atrás:

.. code-block:: bash
  
  $ popd
   popd
  ~
  $ pwd
  /home/sincorchetes


Estos comandos tienen algunas características especiales que podemos consultarlas en el manual de cada uno de ellos.

Renombrando 
***********

Para cambiar de nombre, solo será necesario ejecutar el comando `mv(1)` junto con el directorio que queramos cambiar y el directorio con nuevo nombre. Se pueden emplear rutas relativas, absolutas o una combinación de ambas:

* :source:`mv dir dir_nuevo_nombre`
* :source:`mv dir /home/sincorchetes/nuevo_nombre`
* :source:`mv /home/sincorchetes/dir /home/sincorchetes/nuevo_nombre`

.. note::

  Hay que tener cuidado con utilizar :source:`mv(1)` porque también sirve para mover directorios.**

Moviendo
********

Para desplazar directorios o archivos, tan solo tendremos que hacer uso de nuevo del comando :source:`mv(1)`.

* :source:`mv archivo.ogg /home/sincorchetes/Videos/Echemosunbitstazo`
* :source:`mv archivo.ogg Videos/Echemosunbitstazo`
* :source:`mv /home/sincorchetes/archivo.ogg Videos/Echemosunbitstazo`

También se puede aplicar un renombre más traslado:

* :source:`mv archivo.ogg /home/sincorchetes/Videos/Echemosunbitstazo/nuevo_nombre.ogg`
* :source:`mv archivo.ogg Videos/Echemosunbitstazo/nuevo_nombre.ogg`
* :source:`mv /home/sincorchetes/archivo.ogg Videos/Echemosunbitstazo`
* :source:`mv /home/sincorchetes/archivo.ogg /home/sincorchetes/Videos/Echemosunbitstazo`

Copiando
********

En el caso de copiar archivos, tenemos el comando :source:`cp(1)`. También puede aplicarse el uso de rutas absolutas, relativas o un conjunto de las mismas.
:source:`cp archivo directorio_a_copiar`

Es importante destacar, que para copiar un directorio completo a pesar de que esté vacio. Hagamos uso del modificador :source:`-r` o :source:`-R` (_recursivo_)

También dispone de un modo interactivo utilizando el modificador :source:`-i`

Listar archivos y directorios
*****************************

El comando por excelencia en estos casos es :source:`ls(1)` Nos permite listar con multitudes de opciones si utilizamos los modificadores.

* Listar todos los archivos incluyendo los ocultos con la información que muestra :source:`ls -l`: :source:`ls -al`
* Mostar el nombre de todos los archivos incluyendo la representación del espacio como caracter escapado: :source:`ls -b`
* Mostrar el nombre de todos los archivos en una sola columna: :source:`ls -w 1`

Tipo de archivo
***************

En contra posición de sistemas como Windows, en Linux se puede tener un archivo sin ningún tipo de extensión. El sistema se encarga de averiguar que tipo de archivo es y abrirlo con la aplicación correspondiente.

Si queremos saber algún día si nos han enviado un ejecutable o un audio realmente, haremos uso del comando :source:`file(1)`

Crear un fichero vacío
**********************

Aunque la auténtica utilidad del comando :source:`touch(1)` es modificar la fecha y hora de los archivos. También se puede utilizar para crear un fichero vacío y añadir texto posteriormente.

.. code-block:: bash

  touch fichero_nuevo

Mostrando información de un fichero
***********************************

Si queremos leer un archivo de texto plano como la configuración de un servidor Apache, haremos uso del comando :source:`cat(1)`.

:source:`cat /etc/profile`

Salida truncada:

.. code-block:: bash

  # /etc/profile

  # System wide environment and startup programs, for login setup
  # Functions and aliases go in /etc/bashrc

  # It's NOT a good idea to change this file unless you know what you
  # are doing. It's much better to create a custom.sh shell script in
  # /etc/profile.d/ to make custom changes to your environment, as this
  # will prevent the need for merging in future updates.

  pathmunge () {
    case ":${PATH}:" in
      *:"$1":*)
      ;;
      *)
      if [ "$2" = "after" ] ; then
        PATH=$PATH:$1
      else
        PATH=$1:$PATH
      fi
      esac
  }

Trabajando con texto
####################

Mostrar o redireccionar texto
*****************************

Bash nos permite mostrar una frase, un texto que queramos gracias al comando :source:`echo(1)`.

.. code-block:: bash

  echo "¡No nos perderemos los nuevos artículos de Echemosunbitstazo!"

También podemos redirigir el texto a un archivo nuevo

.. code-block:: bash

  echo "¡No nos perderemos los nuevos artículos de Echemosunbitstazo!" > /home/sincorchetes/Documentos/archivo_nuevo

Añadir información a un archivo ya existente

.. code-block:: bash

  echo "¡No te pierdas él próximo día otro capítulo más sobre Bash en echemosunbitstazo.es" >> /home/sincorchetes/Documento/existente

Crear un archivo y añadir texto directamente
********************************************

Podemos hacer uso del comando :source:`cat(1)` para finalizar la edición, tendremos que finalizarla pulsando la combinación de teclas :source:`CTRL+D` y para ello de la siguiente manera:

.. code-block:: bash

  cat >fichero_de_ejemplo
  Esto es un ejemplo.


Copias de seguridad
###################

El comando por excelencia para elaborar copias de seguridad en Linux es haciendo uso del comando :source:`tar(1)`

Elaborando copias de seguridad
******************************

Elaborando una copia de un directorio
*************************************

.. code-block:: bash

  tar cfv copia_seguridad.tar dir1 dir2 archivo1 archivo2...

Comprimir con bzip2
*******************

.. code-block:: bash

  tar cfvj copia_Seguridad.tar.bz2 dir1 dir2 arch1 arch2...

Utilizar compresión gzip
************************

.. code-block:: bash

  tar cfvz copia_seguridad.tar.gz dir1 dir2 arch1 arch2...

Crear una copia de seguridad con formato xz
*******************************************

.. code-block:: bash

  tar cfvJ copia_seguridad.tar.xz dir1 dir2 arch1 arch2...

Descomprimiendo copias de seguridad
***********************************

A la hora de descomprimir las copias de seguridad no tenemos que declarar el tipo de formato en el que está comprimido, con lo que ganamos más tiempo para dedicarlo a otras cosas.

Descomprimir una copia de seguridad
***********************************

.. code-block:: bash

  tar xfv copia_seguridad.tar

Fuentes
#######

* Ediciones ENI - LPI I Tercera edición
* Man pages 
