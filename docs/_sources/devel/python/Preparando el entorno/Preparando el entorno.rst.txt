Historia
--------

Python es un lenguaje de programación interpretado, de alto nivel y de interés general. Este lenguaje tiene una filosofía de programación que se centra en la legibilidad del código, para ello implementa una serie de declaraciones y estándares que ha de respetarse para que el código funcione como es la indentación. Python es un lenguaje orientado a objetos que facilitan a los desarrolladores escribir un código limpio, eficaz, lógico y pequeño que sirve tanto para pequeños, como medianos y grandes proyectos.

La primera versión de Python se publicó en el año 1991 por Guido van Rossum un programador holandés graduado en matemáticas y ciencias computacionales en la universidad de Amsterdam en 1982. Posteriormente se publicó la versión 2.0 el día 16 de octubre del año 2000 y la versión 3.0 que se liberó el 3 de diciembre de 2008. Actualmente las versiones 1.0 y 2.0 ya no están soportadas, esta última dejó de tener soporte el día 31 de diciembre de 2019.

Notas importantes
#################

Antes de seguir con este artículo es muy importante que sepamos que la versión con la que trabajaremos en las siguientes entragas es *Python 3*. Python 2.7 no tiene más soporte desde el **31 de diciembre del 2019**.

A parte de la versión, conviene saber que tenemos que leer mucho la `documentación oficial <https://docs.python.org/3>`_ si no queremos perder horas y horas con las clásicas pruebas de Error/Acierto (*pruebo cosas al azar y lo que salga salió*).

También tenemos muchos recursos en línea como `Real Python <https://realpython.com>`_ que contienen muchos recursos bastante bien explicados; `Full Stack Python <https://www.fullstackpython.com/best-python-resources.html>`_ tiene tambień muchos recursos, ayudas...

Instalación
###########

Python por norma general está instalado por defecto en el 99% de distribuciones de Linux por lo que no te hará falta tener que instalar nada. Sin embargo, hay distribuciones que a pesar de que Python 2.* se encuentre obsoleto, la mayor parte de librerías y programas que contienen en su sistema operativo hacen uso de la versión 2.7.* que fue la última en mantenerse. Por lo que, quizás necesites realizar unos pasos adicionales para tener Python 3.* instalado en tu Linux.

Algunas distribuciones pueden ser:

* CentOS 6/7
* Debian Stable
* RHEL 6/7
* Gentoo

En FreeBSD y OpenBSD hay que instalarlo con su respectiva paquería, puedes utilizar estas guía oficial de Python para `hacerlo <https://docs.python.org/3/using/unix.html#on-freebsd-and-openbsd>`_

En Windows tenemos dos formas de hacerlo, una es utilizando el subsistema de Linux para Windows haciendo uso de un sistema Linux ejecutándose en un Windows, o bien, la forma oficial que es utilizar el instalador oficial elaborado por la comunidad de Python. Para descarganos el instalador hay que dirigirse a la página de descargas pulsando `aquí <https://www.python.org/downloads/>`_

Una vez descargado, ejecutamos el instalador y seguimos los pasos como tenemos en las imágenes:

.. image:: paso1.png

Desmarcamos la opción de instalar para todos y marcamos la opción de añadir a la variable PATH, después "Install Now":

.. image:: paso2.png

Vemos como se está instalando:

.. image:: paso3.png

En este paso, deshabilitamos el path lenght limit:

.. image:: paso4.png

Y desde PowerShell podemos abrir el ejecutable directamente, veremos la versión que estamos utilizando.

IDEs
####

Hay una gran selección de IDEs bastante buenos que podemos utilizar para aprender, hay tanto de pago, gratuitos, libres y no libres... hay un gran abanico para decidir.

IDLE
****

Un IDE que viene integrado con Python (*incluyendo en la instalación de Windows en la que hemos hablado más arriba*). Permite ejecutar código directamente, depurarlo y tiene un pequeño editor dónde realizar nuestras modificaciones.

.. image:: idle.png

Spyder
******

Es un IDE gratuito y libre que contiene multitud de funciones desde depuración, ejecución y redacción de un archivo en Python todo en una misma ventana. Pues ver más info en su `páginas web <https://www.spyder-ide.org>`_

.. image:: spyder.png

Jupyter Notebook
****************

Es un servidor web que mediante estilos, javascripts y html5 genera un IDE web con el que poder interactuar, al igual que todos permite depurar, crear archivos, navegar por los directorios del sistema operativo...etc `Jupyter <https://jupyter.org>`_

Navegando por los directorios del SO desde su interfaz web

.. image:: jupyternotebook.png

Ejecutando comandos de Python en un archivo nuevo

.. image:: jupyternotebook2.png

Abriendo una sesión de SO desde Web

.. image:: jupyternotebook3.png

Jupyter labs
************

Basado en Jupyter Notebook y Arquitecture contiene más características, como especificar qué versión de Python lanzar, ejecutar una consola directamente de Python o de SO... `Más info en Jupiter <https://jupyter.org>`_

.. image:: jupyterlabs.png

Anaconda
********

Anaconda es un software que contiene todo lo necesario para desplegar un entorno de desarrollo de Python tanto en Linux como en Windows. No solo contiene el intérprete, si no que también tienen varios editores que puedes seleccionar desde su panel "Anaconda Navitator". Más info `en su página <https://www.anaconda.com>`_

.. image:: anaconda.png

PyCharm
*******

PyCharm es un software elaborado por la empresa JetBrains, es bastante conocido porque tiene un potente interfaz de desarrollo que permite hacer carga de espacios de nombres, módulos, referencias... y es muy potente. Aunque es de pago, si eres estudiante y tienes la `ISIC <https://isic.org>`_ puedes obtener una licencia anual gratuita para todos los productos de la empresa como DataGrid, PhpStorm, CLion... y poder hacer tus desarrollos (*siempre personales y no comerciales*) con él.
No obstante, si no eres estudiante, y no quieres comprar la licencia, puedes hacer uso de la versión comunitaria. `Más info <https://www.jetbrains.com/es-es/pycharm/download/>`_

.. image:: pycharm.png

Editores
********

Si no te gusta utilizar un IDE, siempre puedes hacer uso de editores como `vim <https://www.vim.org>`_, `Sublime Text <https://www.sublimetext.com>`_, `VS Code <https://code.visualstudio.com>`_ con sus correspondientes plugins.
