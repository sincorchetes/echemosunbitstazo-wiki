systemd
-------

Configuración
#############

Codificación del sistema
************************

Obtener un resumen de la codificación del sistema
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  localectl

Obtener un listado de las codificaciones disponibles
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: bash

  localectl list-locales

Configurar una codificación del sistema
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: bash

  sudo localectl set-locale en_US.utf8

Huso horario
************

Obtener un resumen de la fecha-hora del sistema
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  timedatectl

Obtener lista de husos horarios
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  timedatectl list-timezones

Configurar huso horario
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash
  
  sudo timedatectl set-timezone Atlantic/Canary


Hostname
########

Configurar el hostname de la máquina:

.. code-block:: bash

  sudo hostnamectl set-hostname NOMBRE_MAQUINA


Troubleshooting
###############

No encuentro la codificación que quiero
***************************************

Revisar los locales instalados
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  rpm -qa |grep glibc-langpack
  dnf list installed langpacks*


Instalar el idioma específico
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash
  
  sudo dnf install glibc-langpack-IDIOMA


La pantalla del portátil entra en suspensión con AC y conectada a otro monitor
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

:code:`/etc/systemd/logind.conf`

.. code-block::

  HandleLidSwitch=ignore
  HandleLidSwitchExternalPower=ignore
  HandleLidSwitchDocked=ignore


Reiniciar el servicio (no hacer SIGHUP como dice)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  systemctl restart systemd-logind

Fuentes
#######

https://unix.stackexchange.com/questions/597360/how-to-disable-suspending-the-system-when-the-lid-is-closed
