Obtener datos introducidos por el usuario
-----------------------------------------

Tenemos una función que es `input()` y podemos solicitar al usuario que introduzca un dato y que este se almacene en una variable, esto nos puede ayudar a dinamizar los programas interactuando con los usuarios:

.. code-block:: python
  
  input('Aquí va un mensaje')

.. note::

  Los datos introducidos se almacenan como un :code:`str`, por lo que si quieres almacenar datos tipo :code:`float`, :code:`int` tendrás que usar la función de conversión que hemos hablado en el apartado de Tipos de datos en Python.

Vamos hacer este ejemplo:

.. code-block:: python

  nombre = input("¿Cómo te llamas? ")
  edad = int(input("¿Qué edad tienes? "))
  print("Me llamo %s y tengo %i años." % (nombre,edad))

Imprimirá un resultado como:

.. code-block::

  ¿Cómo te llamas? Alvaro
  ¿Qué edad tienes? 26
  Me llamo Álvaro y tengo 26 años.


Control de excepciones
######################

¿Qué ocurre si queremos ejecutar un código y depende de una serie de datos que no se han inicializado? No pasa nada, tenemos un mecanismo que controla las excepciones.

try-except
**********

.. code-block:: python

  try:
    # Bloque de código que se probará antes de ejecutar
  except:
    # Bloque de código que se ejecutará si ocurre algún error.


Por ejemplo:

.. code-block:: python

  try:
      print(a)
  except:
      print("Hubo un problema.")


Esto nos imprimirá :code:`Hubo un problema.` pero no nos dice en ningún momento dónde está el error. Evidentemente, el error es que la variable :code:`a` no contiene ningún tipo de valor. Pero, ¿Qué ocurre si quiero personalizar estos errores y mostrar información según convenga?

No pasa nada, podemos añadir excepciones por error, por ejemplo, si la variable :code:`a` no existía, podemos crear una excepción que permita decir que no existe porque no está creada de la siguiente forma.

1. Primero identificamos como se llama el error en Python:

.. code-block:: python

  print(A)
  Traceback (most recent call last):

    File "/tmp/untitled0.py", line 9, in <module>
      print(a)

  NameError: name 'a' is not defined

El nombre del error que tenemos que utilizar es :code:`NameError`.

2. Definimos el :code:`try-except` de la siguiente manera:

.. code-block:: python

  try:
    print(a)
  except NameError:
    print("La variable no se ha asignao, por favor, revisa el programa.")
  except:
    print("Hubo un problema, contacte con el desarrollador de la aplicación.")


¿Se pueden definir múltiples errores y que impiman un mensaje?
Sí que se puede, esto además nos permite ahorrar mucho código.

.. code-block:: python

  try:
    pass
  except(NameError, TypeError, ValueError):
    pass
  except:
    pass


También podemos usar un alias e imprimir solo el mensaje de error:

.. code-block:: python

  try:
    print(a)
  except(NameError, TypeError, ValueError) as EstoEsUnError:
    print(EstoEsUnError)
  except:
    pass


¿Para qué nos sirve esto? Para tener un mayor control en la validación e impresión de nuestro código. :code:`EstoEsUnError` imprimirá: :code:`NameError: name 'a' is not defined`, con este :code:`str` podemos iniciar una validación on :code:`if-elif-else`.

with
****

:code:`with` es un método que permite realizar acciones que posteriormente necesitan limpiarse para que no queden restos en memoria, un ejemplo muy común y extendido es cuando se trabaja con archivos.

.. code-block:: python

  with open('nombreArchivo.ext', modo') as fichero:
    # Bloque de código

Cuando abrimos el archivo de esta forma, aunque hayan problemas con el archivo, este termina cerrándose y dejando de existir en la memoria. Sin embargo, si trabajamos con el archivo de la siguiente forma, el archivo quedará en la memoria de forma casi indefinida en el tiempo generando datos basura:

.. code-block:: python

  fichero = open('nombreArchivo.ext','modo')

Además, de que hay que cerrarlo debidamente:

.. code-block:: python

  fichero.close()

En el siguiente punto trabajaremos más con los archivos, no nos alarmemos.

Puedes consultar más información sobre este apartado en este `hilo <https://docs.python.org/3/tutorial/errors.html>`_ de la documentación.

Trabajando con archivos en Python
#################################

¿Qué podemos hacer en Python con los archivos? ¿Podemos trabajar con ellos?
La cuestión es que sí, podemos abrir, leer, escribir o crear y eliminar archivos, las operaciones básicas que nos deja hacer un SO si estuvieramos en una shell como :code:`bash` o :code:`zsh`.

Abriendo un archivo
*******************

La sintaxis que se utiliza es:

.. code-block:: python

  fichero = open("ruta del archivo", modo)

La sintaxis **correcta**, que **debe usarse** y que utilizaremos en estos ejemplos es:

.. code-block:: python

  with open("ruta del archivo", modo) as nombreFichero:
    # Bloque de código

+----------+-----------------------------------------------------------------------------------------------------------------+
| Modo     | Descripción                                                                                                     |
+==========+=============+===================================================================================================+
|:code:`r` | Lectura, es el valor por defecto, abre el archivo para que se pueda leer y da un error si el archivo no existe. |
+----------+-----------------------------------------------------------------------------------------------------------------+
|:code:`a` | Abre un archivo para agregarle información al final, si no existe el archivo lo crea.                           |
+----------+-----------------------------------------------------------------------------------------------------------------+
|:code:`w` | Sobreescribe cualquier contendio que haya en el archivo que esté abierto y/o crea el archivo si no existe.      |
+----------+-----------------------------------------------------------------------------------------------------------------+
|:code:`x` | Crea el archivo, si devuelve error quiere decir que ya existe.                                                  |
+----------+-----------------------------------------------------------------------------------------------------------------+

Leer archivo
************

Creamos este archivo:

.. code-block:: bash

  $ cd /home/$USER/
  $ cat << EOF >> hola.txt
  > Hola Mundo
  > EOF

Si hacemos un :code:`cat hola.txt` nos mostrará :code:`Hola Mundo`.
Bien, abrimos el archivo con Python

.. code-block:: python

  >>> with open("hola.txt","r") as fichero:
  >>>   fichero.read()
  Hola Mundo

Este método también permite decirle que nos imprima los n caracteres del principio del texto con :code:`.read(4)`.

Devuelve una línea
******************

Si tenemos un archivo con más líneas, podemos imprimirlas con :code:`.readline()` en vez de :code:`.read()`. Sin embargo, si queremos imprimir mas líneas, tenemos que llamar varias veces al método.

.. code-block:: python

  >>> fichero.readline()
  >>> fichero.readline()


Leer el archivo completo
************************

Con ayuda de un bucle :code:`for` lo hacemos:

.. code-block:: python

  >>> with open("ejemplo.txt", "r") as fichero:
  >>> for linea in fichero:
  >>>   print(linea)

Creando un archivo nuevo
************************

Si el archivo existe, dará error.

.. code-block:: python
  
  >>> with open("ejemplo.txt", "x") as fichero:

Cuando terminemos de escribir en un archivo, lo cerramos para que no quede en memoria.

.. code-block:: python

  fichero.close()

Añadir información al archivo
*****************************

En esta línea añadimos el siguiente texto.

.. code-block:: python

  >>> with open("hola.txt","a") as fichero:
  >>> fichero.write("Esta es una línea de ejemplo")

Cuando terminemos de escribir en un archivo, lo cerramos para que no quede en memoria.

.. code-block:: python
  
  fichero.close()

Sobreescribir en el archivo
***************************

Sobreescribimos el archivo si lo abrimos con el modo :code:`w`:

.. code-block:: python

  >>> with open("hola.txt","w") as fichero:
  >>> fichero.write("Te he sobreescrito el contenido con esta línea")

Cuando terminemos de escribir en un archivo, lo cerramos para que no quede en memoria.

.. code-block:: python

  fichero.close()


Eliminar un archivo
*******************

Hay que importar un módulo llamado :code:`os`:

.. code-block:: python

  import os
  os.remove("hola.txt")


