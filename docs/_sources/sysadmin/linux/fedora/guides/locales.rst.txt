Codificación/idioma
---------------------------------------

Instalar otras codificaciones/locales
#####################################

.. code-block:: bash

  sudo dnf install glibc-langpack-ny

* :code:`ny` representa las dos letras del idioma, es por ejemplo para el español.

Ver la configuración actual
###########################

.. code-block:: bash

  localectl status 

Listar las codificaciones e idiomas instalados
##############################################
.. code-block:: bash

  localectl list-locales

Configurar
##########

.. code-block:: bash

  sudo localectl set-locale aa_bb.codificación

Idiomas de teclado tanto para X11 (X.org) y para tty o modo consola

.. code-block:: bash

  localectl list-keymaps

Configurar un idioma de teclado tanto para X11 (X.org) y para tty o modo consola

.. code-block:: bash

  localectl set-keymap

Reiniciar el sistema

.. code-block:: bash

  systemctl reboot

Páginas de documentación, man
-----------------------------

Instalar traducciones
#####################

Buscar traducciones disponibles
###############################

.. code-block:: bash

  sudo dnf search man-pages

Instalar una traducción
#######################

.. code-block:: bash

  sudo dnf install man-pages-es man-pages-es-extra


Realizar consultas en otros idiomas
###################################

.. code-block:: bash

  man -L es man


Libreoffice
-----------

Buscar los idiomas de interfaz disponibles
##########################################

.. code-block:: bash

  sudo dnf search libreoffice-langpack

Instalar el paquete idiomático
##############################

.. code-block:: bash

  sudo dnf install libreoffice-langpack-es

.. note::

  Este detectará tambień el idioma que falta en el entorno de escritorio y el corrector ortográfico (Hunspell) utilizado por el proyecto.

Plasma (KDE)
------------

Ver los idiomas disponibles
###########################

.. code-block:: bash

  sudo dnf search kde-l10n


Instalar el soporte idiomático en español
#########################################

.. code-block:: bash

  sudo dnf install kde-l10n-es

 
