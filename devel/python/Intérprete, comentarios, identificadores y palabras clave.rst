¿Cómo usar Python?
####

Sin duda un elemento imprescindible para poder trabajar con Python son los modos en los qué podemos trabajar con él. Podemos hacerlo de dos formas, mediante intérprete de comandos o elaborando un archivo de Python.

Intérprete de comandos
####

Si estas en Linux o BSD, puedes ver las múltiples (si hay), versiones instaladas en tu sistema si haces un simple: `whereis python` verás una salida como esta:
.. code-block:: bash

  python: /usr/bin/python3.7-config 
  /usr/bin/python2.7 
  /usr/bin/python3.7m-x86_64-config 
  /usr/bin/python /usr/bin/python3.7 
  /usr/bin/python3.7m 
  /usr/bin/python3.7m-config 
  /usr/lib/python2.7 
  /usr/lib/python3.7 
  /usr/lib64/python2.7 
  /usr/lib64/python3.7 
  /usr/include/python2.7 
  /usr/include/python3.7m

Como podemos ver, en mi sistema tengo instalados una versión de Python 3.7 como una 2.7. Es importante destacar que en el curso SIEMPRE trabajaremos con la rama 3.7 o superior porque la versión 2.7 quedó fuera de soporte desde el 31 de diciembre de 2019 y que prestaré más atención a SO Linux que *BSD.

¿Cómo sé que versión tengo por defecto en el sistema?
^^^^

Si hacemos un :code:`ls /usr/bin |grep python` veremos que un enlace simbólico está apuntado a una versión concreta.

.. code-block:: bash
  lrwxrwxrwx.  1 root root              9 Jan 30 10:18 python -> ./python3
  lrwxrwxrwx.  1 root root              9 Oct 21 15:13 python2 -> python2.7
  -rwxr-xr-x.  1 root root          16072 Oct 21 15:13 python2.7


También se puede saber desde el gestor de paquetes que utilices a menudo en tu distribución de Linux o sistemas *BSD y/o ejecutando `python -V` que este te devolverá la versión:

.. code-block:: bash

  $ python -V
  Python 3.7.6


Acceder al intérprete de Python
^^^^
Basta con que ejecutemos el comando :code:`python` para ^`empezar a trabajar <https://docs.python.org/3.8/tutorial/interpreter.html>`_

.. code-block:: bash

  $ python
  Python 3.7.6 (default, Jan  8 2020, 19:59:22) 
  [GCC 7.3.0] :: Anaconda, Inc. on linux
  Type "help", "copyright", "credits" or "license" for more information.
  >>>

Vemos una información de todo un poco, con qué compilador fue compilado Python, qué versión estamos utilizando...etc

Hay una sintaxis mínima que tenemos que entender del promp cuando usamos el intérprete:
:code:`>>>` se refiere a un código que puede ejecutarse sin identación por ejemplo cuando definimos una variable, una función...

.. code-block:: python
  >>> variable = 1

`...` aquí está mencionando que tenemos que indentar, es decir, añadir los espacios (4) correspondientes para respetar la sintaxis de Python.

.. code-block:: python

  >>> def func():
  ...    variable = 1

`'SALIDA'`: Cuando solo salen estas comillas simples, está informando de un valor o imprimiendo la salida de una función, variable...etc

.. code-block:: python

  >>> import sys
  >>> sys.version
  '3.7.6 (default, Jan  8 2020, 19:59:22) \n[GCC 7.3.0]'

Usarlo como calculadora
^^^^

Se pueden realizar operaciones aritméticas (*ya las veremos más adelante*) como suma, resta, división, multiplicación...

.. code-block:: python

  >>> 3 + 2
  5


¿Cómo salir de la terminal?
^^^^
Para salir podemos usar la función :code:`exit()` o pulsar la combinación de teclas <kbd>Ctrl</kbd> + <kbd>C</kbd>

REPL tu intérprete en línea
####

`REPL.it <https://repl.it>`_ es una página que utilizaré mucho para dinamizar los ejemplos, se trata de un intérprete en línea que permite crear un entorno pequeño de Python y poder trabajar con él. En casi todos los ejemplos pondré un enlace para aquellas personas que quieran probar el código y no dispongan de intérprete.

Creando un archivo Python
####

Los archivos de Python tienen la extensión :code:`.py`, y comienzan siempre declarando la ruta del intérprete, a esto se le conoce como `SheBang <https://es.wikipedia.org/wiki/Shebang>`_. Por lo general, se suele utilizar la siguiente cabecera para evitar solapamientos con la versión 2.7.

.. code-block:: bash

  `#!/usr/bin/env python3`

Python 3 utiliza la codificación `UTF-8 por defecto <https://docs.python.org/3/howto/unicode.html#unicode-literals-in-python-source-code>`_, por lo que si queremos trabajar con otro tipo de codificación tendremos que especificarla justamente debajo del SheBang.

.. code-block:: bash

  #!/usr/bin/env python3
  # -*- coding: latin-1 -*-

A partir de aquí añadimos nuestro código.

También es importante, que se le den permisos de escritura al archivo de Python para poderlo ejecutar desde terminal, si no obtendremos el error de permisos:

.. code-block:: bash

  $ ./hola.py
  bash: ./hola.py: Permission denied
  $ chmod +x hola.py
  $ ./hola.py
  Hello world


Ya que sabemos esto, cuando en los comandos de ejemplo haga referencia a los diferentes tipos de prompt (:code:`>>>`, :code:`...` o :code:`' '`) usamos directamente el intérprete y cuando no lo haga, estamos haciendo un archivo en Python. 

¡Una vez que sabemos esto, adelante!

Comentarios
----

Algo muy importante sobre todo en nuestro código es comentar. Comentar nos permite recordar los cambios que hemos hecho en el código o tener al menos un punto de retorno porque cuando llevas muchas horas programando y programando, y revisando... dejas el código unos días, y te costará mucho entender y comprender todo el código de nuevo sin tener una ayuda de por qué decidimos hacer un cambio en la estructura, en el flujo del código...etc

¿Cómo se comenta en Python?
####

Si quieres `comentar <https://docs.python.org/3.8/reference/lexical_analysis.html#comments>`_ una línea, puedes usar:

.. code-block:: python

  # Comentamos con la almohadilla

Cuando queremos comentar múltiples líneas, utilizaremos esta sintaxis:

.. code-block:: python

  """
  Este es un comentario multilínea.
  :D
  """

`Ver ejemplo dinámico aquí <https://repl.it/@sincorchetes/comentarios>`_

Identificadores
----

Los identificadores son el nombre que se utilizan para identificar una variable, función, clases o un objeto.
Las principales reglas que se deben respetar son las siguientes:

* No se utilizan caracteres especiales o numéricos menos ( _ ) que se puede utilizar como un identificador
* Las palabras clave no se utilizan
* Python discrimina de mayúsculas y minúsculas por lo que no es lo mismo llamar a una función o variable :code:`var` si está definida como :code:`Var`.
* Indentar es obligatorio, hay que respetar los espacios cuando se crean funciones, clases o métodos.

Variable
####

Las variables permiten almacenar un valor que le asignes como una cadena, un dato númerico, listas, tuplas... el tipo de valor lo veremos con más profundidad en entregas posteriores, pero hay que saber lo que hace este identificador y para que nos puede servir.

.. code-block:: python

  >>> variable = "Hello world"

Funciones 
####

Permiten ejecutar un fragmento de código específico el cuál puede solicitar o no datos para la ejecución de dicho código.

.. code-block:: python

  >>> def nombre_funcion(argumentos):
  ...    # Bloque de código

Los argumentos se separan por comas.

Bucles
----

Permiten recorrer un conjunto de datos como un :code:`set|lista|tupla|collection`...etc o ejecutarse desde un rango específico como por ejemplo, de 0 a 100 o de 1 a 5...etc

Bucle for
^^^^

.. code-block:: python
  >>> for x in a:
  ...    # Bloque de código

Es el más común.

Clases
####

Las clases son la plantilla de los objetos, Python es un lenguaje de programación orientado a objetos, por lo que es indispensable este identificador.

Propiedades
^^^^

Son los atributos que tiene una clase, a fin de cuentas es como usar variables en otro contexto de programación.

Métodos
^^^^

Son las funciones o acciones que tiene una clase.

Módulo
####

Son fragmentos de códigos externos o integrados en Python que realizan una serie de cosas, se puede conocer en otros lenguajes como librerías.

Pero no nos alarmemos, todos estos identificadores los veremos más adelante de una forma más profunda.

Palabras clave
----

Python como otros lenguajes, tienen una serie de palabras que no se deben utilizar bajo ningún concepto para utilizarlos como identificadores. Podemos averiguar cuáles son desde su `documentación oficial <https://docs.python.org/3/reference/lexical_analysis.html#keywords>`_ o importando el módulo :code:`keyword` y su propiedad :code:`.kwlist`

.. code-block:: python

  >>> import keyword
  >>> print(keyword.kwlist)

Nos devolverá esta salida:

.. code-block:: python

  ['False', 'None', 'True', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']

.. note::
Ver `ejemplo dinámico aquí <https://repl.it/@sincorchetes/palabrasclave>`_
Todas estas palabras no se podrán utilizar como variables, nombres de lista, tuplas, diccionarios... porque su uso está reservado para otras finalidades.

También podemos averiguar si la palabra que estamos utilizando puede estar dentro de esta lista con su método :code:`.iskeyword()`.

.. code-block:: python

  >>> keyword.iskeyword('pass')

Esto devolverá como resultado :code:`True` porque es una palabra reservada.
