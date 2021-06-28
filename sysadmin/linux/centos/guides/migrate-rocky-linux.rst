Migrar a Rocky Linux
--------------------

Introducción
############
Rocky Linux es un proyecto que salió como resultado de la decisión que tomó RedHat con la distribución de Linux CentOS. Decidieron que CentOS Release pasaría a formar parte de CentOS Stream derivando a una rama no estable, pero tampoco muy problemática ya que el equipo de Red Hat prueba mucho todo antes de introducir cambios nuevos. No obstante, las contínuas actualizaciones hacen que no pueda llevarse a cabo un control de versionado y se pueda producir un desajuste en todos los servidores de los que puedas encargarte a menos que, tengas un repositorio adaptado utilizando ya sea :code:`createrepo` o el plugin de Katello de 'The Foreman' y hayas establecido un ciclo de actualizaciones interno.

De todos modos, el resultado sería provocar problemas en aquellas actualizaciones que puedan corregir o mejorar el software y al final termines remezclando las cosas de nuevo, y al final tengas que establecer unos parcheos automatizados que lo subsanen... creo que es un sin sentido.

.. note::

  Procedimiento solo probado con CentOS 8 Release y con el repositorio a terceros :code:`epel-release` habilitado.

.. warning::

  Realizar un snapshot o copia de seguridad previa a este procedimiento.

Migrando
########

Actualizamos los paquetes del sistema
*************************************

.. code-block:: bash
  
  sudo dnf upgrade -y

Descargamos el script de migración
**********************************

.. code-block:: json

  curl -LO https://raw.githubusercontent.com/rocky-linux/rocky-tools/main/migrate2rocky/migrate2rocky.sh


Añadiendo permisos de ejecución
*******************************

.. code-block:: bash

  chmod +x migrate2rocky.sh

Ejecutando la migración
***********************

.. code-block:: bash

  ./migrate2rocky.sh -r

A continuación se realizará una serie de procesos en los que no tendremos que interactuar a menos que den error, reiniciamos el sistema, y si haces :code:`cat /etc/os-release` verás que ya estás utilizando Rocky Linux.

Recursos
########

* `Rocky Linux Tools <https://github.com/rocky-linux/rocky-tools/tree/main/migrate2rocky>`_
 
