Ajustando la apariencia en aplicaciones Qt
------------------------------------------

¿Cuál es el problema?
#####################

Seguro que muchas veces nos ha pasado que hemos instalado aplicaciones que utilizan Qt y se ven muy feas en entornos de escritorio ajenos a Plasma (aka KDE) o LXQT. En este post descubriremos cómo ponerle fin a este suceso, y cómo afrontarlo.

¿Qué es Qt?
###########
Qt es un framework multiplataforma orientado a objetos utilizado para desarrollar aplicaciones que utilicen interfaz grafica. Actualmente este framework es el que utiliza el equipo de Plasma (antes KDE) para su desarrollo y continuación en todo su software de escritorio; la suite de ofimática Calligra Suite (antes llamado KOffice) también lo utiliza; el famoso reproductor multimedia VLC; reproductor y conversor de archivos de audio Clementine...etc.

¿Existe algún método para solucionarlo?
#######################################

Sí, efectivamente, tenemos varios métodos, uno de ellos es hacer uso de scripts, pero vamos a simplificarlo haciendo de la herramienta gráfica que nos proporciona el equipo de Qt llamada `qt5ct` para obtenerla en nuestro sistema bastará con instalarla.

Instalación
###########

En este proceso tenemos la instalación mediante binarios que se obtienen mediante los repositorios de los gestores de paquetes, o bien, mediante código fuente.

Binarios
********

Distribuciones más populares:

* Fedora:
  :code:`# dnf install qt5ct`
* Archlinux
  :code:`# pacman -S qt5ct`
* Ubuntu y Debian
  :code:`# apt-get install qt5ct`
* Gentoo
  :code:`# emerge -av qt5ct`

Código fuente
*************

Para poder compilar el código fuente, hay una serie de pasos que debemos seguir:

.. note::

  Dependiendo de la distribución, pueden variar algunos nombres respecto al qmake porque puede haber más de una versión de Qt instalada en nuestro sistema como es el caso de Fedora que tiene :code:`qmake-qt5` para Qt5 y qmake para Qt4.

#. Descargar el archivo comprimido que contiene el código fuente desde `aquí <https://sourceforge.net/projects/qt5ct/files/latest/download?target=_blank>`_
#. Descomprimirlo en el directorio que queramos
#. Instalar software adicional requerido para el proceso de compilación
#. Compilar el código fuente
#. Instalar en nuestro sistema
#. Ejecutar dicho software.

#### Paquetes necesarios

Esta es la lista de los paquetes que necesitaremos para compilar :code:`qt5ct`, a la izquierda, el nombre común, a la derecha, el nombre de los paquetes en Fedora.

.. code-block::

  qttools-devel => qt5-qttools-devel
  qtbase-devel => qt5-qtbase-devel
  qtbase-static => qt5-qtbase-static
  qtsvg-devel => qt5-qtsvg-devel
  g++ => gcc-c++
  make => make
  gcc => gcc

Compilando
**********

Según el README:

.. code-block:: bash

  $ qmake PREFIX=/DIRECTORIO_A_INSTALAR
  $ make
  # make install

Para instalarlo en el sistema (Fedora)
***************************************

.. code-block:: bash

  $ qmake-qt5 PREFIX=/usr
  $ make
  # make install

Ya lo tendremos instalado, sin embargo, actualizamos la base de datos de los ficheros .desktop para que aparezca en los menús de nuestro entorno de escritorio :code:`update-desktop-database(1)`.

.. code-block:: bash

  # update-desktop-database

Troubleshooting
###############

No puedo iniciar el programa porque obtengo este error
******************************************************

.. code-block::

  > The QT_QPA_PLATFORMTHEME environment variable is not set correctly.

Para solucionarlo, añadimos el siguiente código a un archivo nuevo dentro del directorio :code:`/etc/profile.d/` , guardamos con extensión :code:`.sh` y salimos de la sesión, ya debería estar arreglado.

.. code-block:: bash

  export QT_QPA_PLATFORMTHEME=qt5ct

Referencias
###########

* `Archlinux wiki <https://wiki.archlinux.org/index.php/Uniform_look_for_Qt_and_GTK_applications?target=_blank>`_
* Qt5ct README 
