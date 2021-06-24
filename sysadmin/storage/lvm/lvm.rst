Arquitectura
------------

EL LVM funciona por capas:

.. code-block:: 

  -- Volúmen físico (PV)
  |
  |
  |---- Grupo de volúmenes lógicos (VG)
        |
        |
        |--------- Volumen lógico (LV)
                  |
                  |
                  |
                  |------ Tipo de partición (EXT4|XFS|REISERFS|BTRFS)


* **Volumen físico** es una unidad reservada para poder utilizar el LVM y se crea a partir de una partición del sistema.
* **Grupo de volúmenes:** Permite adherir volúmenes físicos al grupo incrementando/reduciendo el espacio y otras características.
* **Volumen lógico:** Se utiliza para gestionar las particiones que utilizaremos
* **Tipo de partición:** Es el formato que le daremos al volumen lógico y que utilizaremos de sistema de archivos

Volúmenes físicos
-----------------

Comprobar volúmenes físicos
###########################
  
* Para comprobarlos ejecutamos un :code:`sudo pvscan`
* Si no devuelve ningún resultado, es que no existen.

Crear volumen físico
###########################

* Identificar la partición que queremos trabajar, la podemos averiguar con: :code:`sudo fdisk -l /dev/UNIDAD_ALMACENAMIENTO`
  Por ejemplo: :code:`/dev/sdb1`
* Cuando la sepamos, creamos el volumen con: :code:`sudo pvcreate /dev/UNIDAD_ALMACENAMIENTO_N''
  Ejemplo: :code:`sudo pvcreate /dev/sdb1`
* Comprobar que se ha creado :code:`sudo pvscan`

Activar volúmenes físicos inactivos
###################################

* Falta proc

Desactivar volúmenes físicos
############################

* Falta proc

Visualizar información del volumen físico
#########################################

* Averiguar que PV queremos comprobar
  :code:`sudo pvdisplay /dev/PV_Nombre`

Grupo de volúmenes
------------------

Crear un grupo de volúmenes
###########################

* Hay que averiguar que volumen físico vamos a utilizar para poder crear el volumen
* Crear el volumen:
  :code:`sudo vgcreate **Nombre_GrupoVolumen** /dev/Unidad_AlmacenamientoN_partición`

Eliminar un grupo de volúmenes
##############################

* Averiguar que volumen vamos a eliminar
* Eliminándolo

.. code-block:: bash

  sudo vgchange -a n Nombre_GrupoVolumen
  sudo vgremove Nombre_GrupoVolumen

Averiguar la información de un grupo de volumen
###############################################

* Averiguar que VG queremos comprobar
  :code:`sudo vgdisplay /dev/VG_Nombre`

Volúmenes lógicos y particiones
-------------------------------

Comprobar volúmenes lógicos
###########################

* Para comprobarlos ejecutamos un :code:`sudo lvscan`
* Comprobar el tipo de FS que usa el volumen lógico :code:`sudo mount |grep Nombre_Volumen`
* Si no devuelve ningún resultado, es que no existen.

Crear volumen lógico
####################

* Paso anterior
* Ocupar todo el espacio disponible del Grupo de Volúmen (:code:`VolGroupXY`): :code:`sudo lvcreate -l 100%FREE -n NOMBRELV VOLGROUPXY`
* Coger espacio medido (e.g 10G): :code:`sudo lvcreate -L 20G -n NOMMBRELV VOLGROUPXY`
 * Para EXT4: :code:`sudo mkfs.ext4 /dev/VolGroupXY/LVol`
 * Para XFS: :code:`sudo mkfs.xfs /dev/VolGroupXY/LVol`

Expandir volumen lógico con capacidad específica
################################################

* Realizar este punto
* Aumentar el volumen lógico a 20GB
  :code:`sudo lvextend -L +20GB /dev/VolGroupXY/LVol`
   * Para EXT4
     :code:`sudo resize2fs /dev/VolGroupXY/vol`
   * Para XFS
     :code:`sudo xfs_growfs /dev/VolGroupXY/vol`

Aumentar un volumen lógico con todo el espacio disponible
#########################################################

*   Para incrementar el espacio del volumen lógico para que consuma todo el espacio libre del grupo de volúmenes
    :code:`sudo lvextend -l +100%FREE /dev/VolGroupXY/LVol`
    * Para EXT4
      `:code:`sudo resize2fs /dev/VolGroupXY/vol`
    * Para XFS
      :code:`sudo xfs_growfs /dev/VolGroupXY/vol`

Reducir el espacio de un volúmen lógico (Procedimiento NO probado)
##################################################################

*   **Procedimiento no válido para particiones XFS**
*   Una vez identificado el volumen lógico, lo reducimos:
    :code:`sudo lvreduce --size X(GB|MB|KB) /dev/VolGroupXY/LVol`
*   Hay que redimensionar el espacio de la partición utilizada

Averiguar la información de un volumen lógico
#############################################

* Averiguar que LV queremos comprobar
  :code:`sudo lvdisplay /dev/VG_Nombre`

Renombrar un volúmen lógico
###########################

.. code-block:: bash

  sudo umount -lf /dev/VolGroup02/VOL
  sudo lvrename /dev/VolGroup02/VOL /dev/VolGroup02/VOL_NUEVO_NOMBRE

Referencias
-----------

[[https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/logical_volume_manager_administration/index|LVM - Red Hat Doc]] 
