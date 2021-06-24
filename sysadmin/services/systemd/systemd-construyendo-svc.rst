Diferencias entre gestores de servicios
---------------------------------------

Introducción
############

Red Hat 6 y 7 tienen gestores de servicio diferentes. La versión 6 utiliza Upstart, sin embargo, el equipo de Red Hat lo implementó como reemplazo de SysVinit por su modo de arranque que es más cómodo y más moderno, no obstante, ellos utilizan para todo el sistema scripts de SysVinit por su compatibilidad con Upstart.

En Red Hat 7, utilizan el gestor de servicios de systemd, este gestor de servicios es una síntesis de todos los gestores que habían en el ecosistema UNIX incluyendo el de OS X, y Lennart Poettering, voluntario del proyecto Fedora elaboró un gestor de servicios con cada una de las ideas de cada gestor (SysVinit, Upstart, runit, rc.d...). Este soportaba paralelización de procesos en el arranque acelerando las cargas del sistema operativo, también permite una mayor escritura en logs porque no usa texto si no, binarios. Hoy en día, es el gestor de servicios estándar después de que los demás proyectos comunitarios como OpenSUSE, ArchLinux, el proyecto Debian y por consiguiente Ubuntu lo hubiesen adoptado por defecto.

Breves diferencias a nivel de servicios
#######################################

SysVinit
********

* Directorio de scripts de arranque: :code:`/etc/init.d`
* Los logs son específicos de cada servicio, por lo general se almacenan en :code:`/var/log/` (el texto es más difícil de procesar a nivel de servicio)
* No existe paralelización al arranque/parada de servicios
* La elaboración de servicios es más enrrebesada y compleja de mantener, las funciones de arranque, parada, reinicio o consulta del servicio están definidos como funciones dentro del script del servicio.

Elaborando servicios para SysVinit (RHEL6)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Vamos a elaborar un ejemplo de servicio que monitorice el servicio nfs y que lo reinicie en caso de que esté caído. Para ello, verificamos si el archivo :code:`/var/lock/subsys/nfs` existe, si no existe, reiniciaremos el servicio.

Creando el servicio (o demonio) /etc/init.d/check_nfs_working
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  #!/bin/bash
  #
  # checking_nfs        Check NFS is working on system
  #
  # chkconfig: 2345 12 88
  # description: System would be check if NFS service is loaded
  ### BEGIN INIT INFO
  # Provides: $checking_nfs
  # Required-Start: $local_fs
  # Required-Stop: $local_fs
  # Default-Start:  2 3 4 5
  # Default-Stop: 0 1 6
  # Short-Description: System would be check if NFS service is loaded
  # Description: System would be check if NFS service is loaded
  ### END INIT INFO

  # Source function library.
  . /etc/init.d/functions
  
  prog=checking_nfs
  script=/admin/bin/checking_nfs
  lockfile=/var/lock/subsys/$prog

  start() {
    echo -n "Starting NFS is working: "
    ${script} &
    touch /var/lock/subsys/checking_nfs
    success $"Checking NFS is started"
    echo    
  }

  stop() {
    echo -n "Stopping NFS is working: "
    killproc checking_nfs
    rm -f /var/lock/subsys/checking_nfs
    echo
    }

  restart() {
    stop
    start
  }

  case "$1" in
    start)
      start
      ;;
    stop)
      stop
      ;;
    restart)
      restart
      ;;
    reload)
      exit 3
      ;;
    force-reload)
      restart
      ;;
    status)
      status checking_nfs
      ;;
    condrestart|try-restart)
      rhstatus >/dev/null 2>&1 || exit 0
      restart
      ;;
    *)
      echo $"Usage: $0 {start|stop|restart|condrestart|try-restart|reload|force-reload|status}"
      exit 3
  esac

  exit $?


El contenido de arriba sería todo lo que necesitaríamos para elaborar el objetivo que tenemos, vamos a explicar un poco qué es cada parte:

.. code-block:: bash

  #!/bin/bash

Declaramos el BashGang para que, al leer el script lo interprete con la Shell Bash y no con otra como SH, KSH, Fish...etc

.. code-block:: bash

  #
  # checking_nfs        Check NFS is working on system
  #
  # chkconfig: 2345 12 88
  # description: System would be check if NFS service is loaded


Definimos algunos datos necesarios para que podamos identificar que hace este servicio, también es importante incluir esta cabecera porque si no no se podrá configurar al arranque del inicio del sistema operativo. Si nos fijamos en el comando chkconfig, tenemos 3 argumentos con solo números enteros, lo explicamos:

* :code:`2345` – Se refiere a los runlevels en el que el servicio se habilitará por defecto.
* :code:`12` – Es la prioridad para que arranque, si el valor es muy bajo tendrá una prioridad más alta para que se arranque en el inicio del sistema.
* :code:`88` – Es la prioridad para que se detenga el servicio, si el valor es muy bajo tendrá una prioridad más alta para que se detenga en el apagado del sistema.

.. code-block:: bash

  ### BEGIN INIT INFO
  # Provides: $checking_nfs
  # Required-Start: $local_fs
  # Required-Stop: $local_fs
  # Default-Start:  2 3 4 5
  # Default-Stop: 0 1 6
  # Short-Description: System would be check if NFS service is loaded
  # Description: System would be check if NFS service is loaded
  ### END INIT INFO


Este bloque, es la parte de Linux Standard Base, se definen las dependencias necesarias para el arranque o inicio del servicio incluyendo información adicional, incluyendo los runlevels de ejecución y de parada.

.. code-block:: bash

  # Source function library.
  . /etc/init.d/functions


Permite cargar funciones adicionales como :code:`daemon`, :code:`killproc`... que se pueden utilizar en otros scripts, sin embargo, principalmente utilizaremos :code:`killproc`.

.. code-block:: bash

  prog=checking_nfs
  script=/admin/bin/checking_nfs
  lockfile=/var/lock/subsys/$prog


Definimos como se llama el programa, dónde está ubicado el script, y el archivo que se bloqueará para que no haya una ejecución descontrolada del servicio (se ejecuten 2,3, 4 a la vez)

.. code-block:: bash

  start() {
    echo -n "Starting NFS is working: "
    ${script} &
    touch /var/lock/subsys/checking_nfs
    success $"Checking NFS is started"
    echo
  }

  stop() {
    echo -n "Stopping NFS is working: "
    killproc checking_nfs
    rm -f /var/lock/subsys/checking_nfs
    echo
  }

  restart() {
    stop
    start
  }

Definimos las funciones que hará nuestro servicio, por lo general son los comandos que ejecutaremos para que funcione en sí el servicio.

.. code-block:: bash

  case "$1" in
    start)
      start
      ;;
    stop)
      stop
      ;;
    restart)
      restart
      ;;
    reload)
      exit 3
      ;;
    force-reload)
      restart
      ;;
    status)
      status checking_nfs
      ;;
    condrestart|try-restart)
      rhstatus >/dev/null 2>&1 || exit 0
      restart
      ;;
    *)
      echo $"Usage: $0 {start|stop|restart|condrestart|try-restart|reload|force-reload|status}"
      exit 3
  esac

  exit $?

Este switch funciona cuando ejecutemos el comando :code:`service check_nfs_working start|status|restart`, el parámetro recibido. :code:` ` **¡No olvides asignarle permisos de ejecución!**

Elaborando el script que comprueba el servicio nfs

.. code-block:: bash

  #!/bin/bash

  while :
  do
    if [ -f /var/lock/subsys/nfs ]
    then
      echo "El servicio NFS está funcionando" >> /var/log/checking_nfs
    else
      echo "Ha fallado el servicio NFS, se va a reiniciar" >> /var/log/checking_nfs
      service nfs restart
    fi
    sleep 5
  done

Este script permite comprobar si el fichero que genera el servicio de nfs está creado, si lo está vuelca en un archivo de log que existe y está funcionando (para revisiones futuras). En caso de que no exista el archivo, se reiniciará todo el servicio. Esta comprobación es infinita, **es importante que el bucle sea infinito pero que contenga un :code:`sleep` para que no sature los recursos del sistema.** Con el `sleep` definimos el tiempo (en segundos) que queremos que se compruebe. **¡No olvides asignarle permisos de ejecución!**

Arrancando el servicio
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo service check_nfs_working start
  Starting NFS is working:                                   [  OK  ]

Consultando el servicio
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo service check_nfs_working status
  checking_nfs (pid 9599 7158) is running...

Parando el servicio
^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo service check_nfs_working stop
  Stopping NFS is working:                                   [  OK  ]

Habilitando el servicio en el arranque
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo chkconfig check_nfs_working on

Comprobando que los runlevels son los que hemos configurado en el servicio (o demonio)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo chkconfig --list check_nfs_working
  check_nfs_working       0:off   1:off   2:on    3:on    4:on    5:on    6:off


.. note::

  Si los comparamos con el servicio, veremos que coinciden.

Desactivando el servicio al arranque
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo chkconfig check_nfs_working off

Systemd
*******

* Directorio de servicios locales: :code:`/etc/systemd/`
* Directorio de servicios específicos por RPM instalados: :code:`/usr/lib/systemd`
* Los logs se leen mediante :code:`journalctl`, el resultado o salida de la ejecución de los servicios se almacenan en formato binario (más rápidez de lectura/escritura)
* Existe paralelización al arranque/parada de servicios disminuyendo el tiempo de encendido/apagado
* Elaborar un servicio es más fácil, no hay que definir los bloques de :code:`start`, :code:`stop`, :code:`restart`, status como en SysVinit facilitando más la rápidez y legibilidad cuando se crea un servicio.

Elaborando un servicio (no demonio) para systemd (RHEL7)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

En systemd el concepto de demonio (daemon) se pierde, no se menciona, solo se comenta el uso de servicio.

Creando el servicio /etc/systemd/system/check_nfs_working.service
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  [Unit]
  Description=Checking if NFS is working
  After=network.target

  [Service]
  Type=simple
  
  User=root
  ExecStart=/admin/bin/check_nfs_working.sh
  Restart=on-failure
  
  [Install]
  WantedBy=multi-user.target

Como ves, la diferencia está muy clara. Vamos a explicar este bloque declarativo.

En :code:`systemd`, los :code:`Units` pueden contener servicios abstractos, recursos de red, dispositivos, sistemas de archivos montados, y recursos aislados, por lo que es más que una definición.

.. code-block::

  [Unit]
  Description=Checking if NFS is working
  After=network.target


Por ejemplo, aquí decimos que se arranque este servicio después de que el :code:`network.target` se haya completado, que quiere decir, cuando la red esté lista, arranca este servicio.

.. note::

  Los targets vienen siendo un símil a los runlevels.

.. code-block:: bash

  [Service]
  Type=simple

  User=root
  ExecStart=/admin/bin/check_nfs_working.sh
  Restart=on-failure

Definimos la información del servicio, ¿Cómo debe ejecutarse? ¿Qué tiene que hacer? ¿Qué ocurre si se reinicia? ¿Se crean hilos o subprocesos?

.. code-block::

  [Install]
  WantedBy=multi-user.target

Definimos en qué runlevel debe arrancar este servicio.

Elaborando el script que comprueba el servicio nfs /admin/bin/check_nfs_working.sh
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  #!/bin/bash

  while :
  do
    checkProcess=$(systemctl status nfs |grep Active |awk '{print $2}')

    if [ "${checkProcess}" == "active" ]
    then
      echo "El proceso está funcionando correctamente."
    else
      systemctl restart nfs
      echo "El proceso no está funcionando correctamente."

    fi
    sleep 5
  done


Este script permite comprobar si el servicio nfs está funcionando, si lo está vuelca en un archivo de log que existe y está funcionando (para revisiones futuras). En caso de que no exista el archivo, se reiniciará todo el servicio. Esta comprobación es infinita, **es importante que el bucle sea infinito pero que contenga un sleep para que no sature los recursos del sistema.** Con el sleep definimos el tiempo (en segundos) que queremos que se compruebe. **¡No olvides asignarle permisos de ejecución!**

Arrancando el servicio
^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo systemctl start_nfs_working

Consultando el servicio
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo systemctl status checking_nfs_working.service
  ● check_nfs_working.service - Checking if daemon is working
     Loaded: loaded (/etc/systemd/system/check_nfs_working.service; disabled; vendor preset: disabled)
     Active: active (running) since Fri 2019-10-04 11:19:02 CEST; 1s ago
   Main PID: 24600 (check_nfs_worki)
     CGroup: /system.slice/check_nfs_working.service
             ├─24600 /bin/bash /admin/bin/check_nfs_working.sh
             └─24605 sleep 5

  Oct 04 11:19:02 server systemd[1]: Started Checking if daemon is working.
  Oct 04 11:19:02 server check_nfs_working.sh[24600]: El proceso está funcionando correctamente.


Parando el servicio
^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo systemctl stop check_nfs_working.service


Habilitando el servicio en el arranque
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo systemctl enable check_nfs_working.service


Comprobando si está habilitado al arranque
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo systemctl is-enabled check_nfs_working.service
  disabled

.. note::

  Si los comparamos con el servicio, veremos que coinciden.

Desactivando el servicio al arranque
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  sudo systemctl disable check_nfs_working.service


Fuentes
#######

* [[https://www.devdungeon.com/content/creating-systemd-service-files|DevDungeon - Creating systemd service files]]
* [[https://wiki.debian.org/LSBInitScripts/|Debian Wiki LSB Init Scripts]]
* [[https://www.cyberciti.biz/tips/linux-write-sys-v-init-script-to-start-stop-service.html|Cybercity - Linux Write Sys V init to start stop service]]