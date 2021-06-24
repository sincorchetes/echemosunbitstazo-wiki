dpkg, APT, aptitude
-------------------

Introducción
############

APT o aptitude es el software de alto nivel utilizado por distribuciones basadas en Ubuntu o Debian, ambas también inclusive. Mientras que dpkg es el gestor de paquetes a bajo nivel del sistema.

Troubleshoot
############

E: dpkg was interrupted, you must manually run 'sudo dpkg --configure -a' to correct the problem. 
*************************************************************************************************

Solución:

.. code-block:: bash

  sudo dpkg --configure -a

package is in a very bad inconsistent state
*******************************************

Solución:

.. code-block:: bash

  sudo apt-get remove [paquete_en_cuestión]
  sudo dpkg --remove --force-remove-reinstreq [paquete_en_custión]

E: Sub-process /usr/bin/dpkg exited unexpectedly
************************************************

Solución:

Reinstalar...

El problema de APT/dpkg... es que no puede reconstruir su base de datos y queda corrupta.

Se intentó con:

.. code-block:: bash

  sudo dpkg --force-all -r sudo
  sudo apt-get install -f sudo
  sudo dpkg --configure -a
  sudo mv /var/lib/dpkg/info/<packagename>.* /tmp/
  sudo dpkg --remove --force-remove-reinstreq <packagename>
  sudo apt-get remove <packagename>
  sudo apt-get autoremove && sudo apt-get autoclean

Sin éxito

