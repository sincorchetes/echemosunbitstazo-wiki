Repositorio a terceros
----------------------

RPM Fusion
##########

¿Qué es RPM Fusion?
*******************
Son unos repositorios que se crearon para suplir todo el software que no se distribuye en Fedora por no seguir el licenciamiento acorde a los valores que difunde el proyecto, que es sobre todo Software Libre y Open Source antes que el software privativo o con licencias que sean incompatibles. Son repositorios completamente mantenidos por terceras personas.

* :code:`free`: Contiene software con licencias más cercanas al SL u OS.
* :code:`non-free`: Software privado como códecs o drivers de NVIDIA, Broadcom...

Instalar repositorios free
**************************
.. code-block:: bash

  sudo dnf install https://mirrors.rpmfusion.org/free/fedora/rpmfusion-free-release-$(rpm -E %fedora).noarch.rpm
  sudo dnf check-update

Instalar repositorios non-free
******************************
.. code-block:: bash

  sudo dnf install https://mirrors.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-$(rpm -E %fedora).noarch.rpm
  sudo dnf check-update

Fuentes
#######

* `Instalación de RPM Fusion <https://rpmfusion.org/Configuration>`_
