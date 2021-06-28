Migrar a Rocky Linux
--------------------

Introducción
############
Rocky Linux es un proyecto que salió como resultado de una decisión que tomó Red Hat con la distribución de Linux CentOS. Decidieron que CentOS Release pasaría a formar parte de CentOS Stream derivando a una rama no estable, aunque Red Hat se escude con que todo se prueba a fondo y pasan unos controles de calidad, no es lo mismo algo que es puramente certificado como estable. Otro problema con estas ramas es que hay continuas actualizaciones que no permiten mantener una línea o ciclo de actualizaciones internos controlados. Ya que una actualización puede solventar el problema de un parche anterior...etc.

.. note::

  Procedimiento solo probado con CentOS 8 Release y con el repositorio a terceros :code:`epel-release` habilitado.

.. warning::

  Realizar un snapshot o copia de seguridad previa a este procedimiento.

Migrando
########

.. note::

  Los siguientes pasos se ejecutan en el servidor que quieres actualizar y como superusuario :code:`root` o utilizando :code:`sudo` en su defecto.

Actualizar los paquetes del sistema
***********************************

.. code-block:: bash
  
  dnf upgrade -y

Descargar el script de migración
********************************

.. code-block:: bash

  curl -LO https://raw.githubusercontent.com/rocky-linux/rocky-tools/main/migrate2rocky/migrate2rocky.sh


Añadir permisos de ejecución
****************************

.. code-block:: bash

  chmod +x migrate2rocky.sh

Realizar la migración
*********************

.. code-block:: bash

  ./migrate2rocky.sh -r

A continuación se realizarán una serie de procesos en los que no hay que interactuar a menos que den error.

Reiniciar el sistema
********************

.. code-block:: bash

  systemctl reboot

Comprobar que se actualizó
**************************

.. code-block:: bash

  cat /etc/os-release

Verás que ya estás utilizando Rocky Linux.

Recursos
########

* `Rocky Linux Tools <https://github.com/rocky-linux/rocky-tools/tree/main/migrate2rocky>`_
 
