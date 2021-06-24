Docker
------

Instalar dependencias y Docker
##############################

.. code-block:: bash

  sudo dnf -y install dnf-plugins-core
  sudo dnf config-manager --add-repo https://download.docker.com/linux/fedora/docker-ce.repo
  sudo dnf install docker-ce docker-ce-cli containerd.io
  sudo grubby --update-kernel=ALL --args="systemd.unified_cgroup_hierarchy=0"

Reiniciar el equipo
###################

.. code-block:: bash

  sudo systemctl reboot

Habilitar y arrancar el servicio al arranque
############################################

.. code-block:: bash

  sudo systemctl enable --now docker.service


Ejecutar Docker sin necesitar privilegios
#########################################

Añadir el usuario que necesites al grupo :code:`docker`

.. code-block:: bash

  sudo gpasswd -a USUARIO docker

Salir y entrar de la sesión o ejecutar

.. code-block:: bash

  newgrp docker

Instalar Docker Compose
#######################

.. code-block:: bash

  sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  sudo chmod +x /usr/local/bin/docker-compose

* Realizar cualquier operativa basta con que ejecutes :code:`docker-compose`

Fuentes
#######

* `Documentación de Docker <https://docs.docker.com/engine/install/fedora/>`_
* `Instalación de Docker Compose doc oficial <https://docs.docker.com/compose/install/>`_

