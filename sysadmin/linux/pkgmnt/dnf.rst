DNF
----

Gestión de paquetería
####

Refrescar la base de datos de DNF
****

.. code-block:: bash

  dnf check-update


Actualizar el sistema con los últimos parches
****

.. code-block:: bash

  dnf upgrade


Sincronizar los últimos paquetes instalados

.. note::

  Solo cuando se actualiza de versión.

.. code-block:: bash

  dnf distro-sync


Instalar software
****

.. code-block:: bash

  dnf install [paquete1 paquete2...]


Desinstalar software
****

.. code-block:: bash

  dnf remove [paquete1 paquete2...]


Buscar software
****

.. code-block:: bash

  dnf search [palabra_a_buscar]


Buscar paquetes mediante un archivo
****

.. code-block:: bash

  dnf provides /bin/bash


Descargar solo paquetes
****

.. code-block:: bash

dnf download [paquete1 paquete2...]


Obtener información del paquete
****

.. code-block:: bash

dnf info [paquete]


