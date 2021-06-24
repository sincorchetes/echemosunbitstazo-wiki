FirewallD
---------

Habilitar un puerto específico TCP de forma temporal
####################################################

.. code-block:: bash
  
  firewall-cmd --add-port XXX/tcp

Habilitar un puerto específico TCP de forma permanente
######################################################

.. code-block:: bash

  firewall-cmd --add-port XXX/tcp --permanent
  firewall-cmd --reload

Habilitar un puerto específico UDP de forma temporal
####################################################

.. code-block:: bash

  firewall-cmd --add-port XXX/udp


Habilitar un puerto específico UDP de forma permanente
######################################################

.. code-block:: bash

  firewall-cmd --add-port XXX/udp --permanent
  firewall-cmd --reload
