Instalando CRI-O
----------------

Introducción
############
CRI-O es un ''container runtime'' que permite ejecutar contenedores.
Pendiente de editar esta parte

Instalación
###########

Añadimos los siguientes repositorios
**************************************************

.. code-server:: bash
  
  sudo curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable.repo https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/CentOS_8_Stream/devel:kubic:libcontainers:stable.repo
  sudo curl -L -o /etc/yum.repos.d/devel:kubic:libcontainers:stable:cri-o:v1.20.repo https://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable:/cri-o:/1.20/CentOS_7/devel:kubic:libcontainers:stable:cri-o:1.20.repo
  sudo dnf install cri-o conntrack -y


Configuración
###########

Crear el archivo /etc/cni/net.d/10-crio-bridge.conf
*****************************************************
.. code-server:: json

  {
    "cniVersion": "0.3.1",
    "name": "crio",
    "type": "bridge",
    "bridge": "cni0",
    "isGateway": true,
    "ipMasq": true,
    "hairpinMode": true,
    "ipam": {
      "type": "host-local",
      "routes": [
        {
          "dst": "0.0.0.0/0"
        },
        {
          "dst": "1100:200::1/24"
        }
      ],
      "ranges": [
        [
          {
            "subnet": "10.85.0.0/16"
          }
        ],
        [
          {
            "subnet": "1100:200::/24"
          }
        ]
      ]
    }
  }


Habilitando al inicio del arranque
**********************************

.. code-server:: bash

  sudo systemctl enable --now crio.service


Recursos
########

* Parte de la guía utilizada de `cri-o <https://github.com/cri-o/cri-o/blob/master/tutorials/kubeadm.md>`_
 
