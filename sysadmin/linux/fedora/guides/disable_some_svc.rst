Deshabilitando servicios
------------------------

Introducción
############

Cuando Fedora se instala hay servicios que podemos prescindir de ellos o deshabilitarlos si no los utilizamos, así evitamos problemas de seguridad y reduciremos en consumo, a pesar de que puede que el sistema  no se inicie con todos los servicios que he expuesto aquí, es recomendable desactivar los que no necesitemos.

fprintd - Lector de huellas
***************************

Si no utilizamos un lector de huellas, es mejor deshabilitarlo

.. code-block:: bash
  
  sudo systemctl disable --now fprintd.service


livesys/livesys-late - Servicios LiveCD/DVD/USB
***************************

Estos servicios se utilizan para configuraciones mientras se instala la distribución pero no nos hace más falta una vez instalada

.. code-block:: bash

  sudo systemctl disable --now livesys
  sudo systemctl disable --now livesys-late


Bluetooth - Sistema de conexion PAN
***********************************

Si no tienes un dispositivo de Bluetooth o lo quieres utilizar solo bajo demanda, conviene desactivarlo y activarlo cuando guste.

.. code-block:: bash

  sudo systemctl disable --now bluetooth.service
  sudo systemctl disable --now bluetooth.target


Avahi - Autodescubrimiento
**************************

Si no utilizas autodescubrimiento en la red local, no hace falta que los tengas

.. code-block:: bash

  sudo systemctl disable --now avahi-daemon.service
  sudo systemctl disable --now avahi-daemon.socket


CUPS - Impresoras
*****************

Si no tienes impresoras, ¿para qué lo necesitas?

.. code-block:: bash
  
  sudo systemctl disable --now cups.service


NFS - Sistema de archivos en red
********************************

Si no usas NFS cliente/servidor, desactívalo:

.. code-block:: bash
  sudo systemctl disable --now nfs-blkmap.service
  sudo systemctl disable --now nfs-client.target
  sudo systemctl disable --now nfs-server.service
  sudo systemctl disable --now nfs-convert.service


scsi - Sistemas de detección y manipulación SCSI
************************************************

Si solo usas pendrives, discos SATA/IDE, SSD... no hace falta tener este servicio

.. code-block:: bash

  sudo systemctl disable --now iscsid.service
  sudo systemctl disable --now iscsid.socket
  sudo systemctl disable --now iscsi.service
  sudo systemctl disable --now iscsiuio.service
  sudo systemctl disable --now iscsiuio.socket   


RAID - Sistema de replicación de discos/disp almacenamiento
***********************************************************

Si no lo usamos

.. code-block:: bash

  sudo systemctl disable raid-check.timer


LVM - Gestor de Volúmenes de Linux
**********************************

.. note:: 

  DESACTIVAR SOLO SI NO USAMOS LVM O PROVOCARÁ UN SISTEMA INSERVIBLE**

.. code-block:: bash
  
  sudo systemctl disable lvm2-lvmpolld.socket
  sudo systemctl disable lvm2-monitor.service