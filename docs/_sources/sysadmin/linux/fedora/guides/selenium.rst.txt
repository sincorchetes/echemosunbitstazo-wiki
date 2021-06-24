Selenium
--------

Google Chrome y Python
######################

* Requisitos:
  * Tener instalado Google Chrome
  * Tener instalado el plugin de `Selenium IDE <https://chrome.google.com/webstore/detail/selenium-ide/mooikfkahbdckldjjndioackbalphokd>`_
  * Realizar una grabación o acciones en una página
  * Exportar el :code:`.side` a :code:`.py` desde el plugin de Chrome

.. code-block:: bash

  sudo dnf install chromedriver

Crear `Virtualenv`

.. code-block:: bash

  python -m venv selenium

Instalar dependencias

.. code-block:: bash

  source selenium/bin/active
  pip install selenium pytest

Editar el archivo exportado :code:`*.py` y añadir lo siguiente:

.. code-block:: python

  o = CLASE()
  o.setup_method('get')
  o.METODO()

Hay que cambiar CLASE y METODO según lo que hay en el archivo y ejecutar el script

.. code-block:: bash

  python NombreArchivo.py

 
