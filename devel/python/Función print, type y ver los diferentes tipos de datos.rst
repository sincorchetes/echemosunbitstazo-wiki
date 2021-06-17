Función print()
----

Esta función se utiliza para imprimir valores por lo que nos podemos imaginar lo que podemos imprimir, resultados de funciones, valores asignados a variables, textos...etc.

.. code-block:: python

  print("Hello World")

Esta sentencia imprime en pantalla `Hello World`. Más adelante, veremos distintos usos de cómo utilizar esta función como por ejemplo, sustituciones de valores por variables...

Función type()
----

Esta función nos permite averiguar el tipo de dato que estamos tratando.

.. code-block:: python

  >>> type("Hello World")

O asignándolo en una variable y después imprimirlo:

.. code-block:: python
  >>> type("Hello World")

Esto nos devolverá un mensaje como: :code:`<class 'str'>` indicando que es un :code:`str` o cadena.
Si probamos con un nº entero como el 2 nos devolverá :code:`<class 'int'>`:

.. code-block:: python

  >>> type(2)

:code:`type()` y :code:`print()` son unas de las funciones más utilizadas, sobre todo para cuando tengamos que hacer depuración y revisar por qué en nuestro código hay cosas que no funcionan si estamos tratando con tipos de datos.

Tipos de datos en Python (Literals)

* Cadenas o strings
* Constantes
* Númericos
* Especiales

Cadenas o *strings*
####

Se forman encerrando un texto utilizando (" ") ó (' '). 

Por ejemplo:

.. code-block:: python

  helloWorld = "Hello world"
  helloWorld = 'Hello world'


Se puede definir cadenas con múltiples líneas:

.. code-block:: python
  :linenos:

  helloWorldMessage = '''
  Este es un mensaje para toda la civilización.
  Todos(as) aquellos(as) que no se interesen por la historia,
  estarán condenados(as) a repetir los mismos errores que se
  cometieron en el pasado. '''


Obtener la primera letra de un :code:`str`:

.. code-block:: python

  >>> mensaje = "Hola mundo"
  >>> print(mensaje[0])
  h


Obtener letras de un :code:`str` a partir de un rango:

.. code-block:: python

  >>> mensaje = "Hola mundo"
  >>> print(mensaje[0:4])
  hola


Conseguir la posición de un :code:`str` en un :code:`str`:

.. code-block:: python

  >>> mensaje = "Hola mundo, me llamo sincorchetes y estamos en echemosunbitstazo.es"
  >>> mensaje.find("me")
  12

Si nos ponemos a contar (*desde 0 siempre*) caracter por caracter (*incluyendo los espacios y ,*), obtendremos el número 12.

Reemplazar un :code:´str´ dentro de un :code:´str´:

.. code-block:: python

  >>> mensaje = "Hola mundo, me llamo sincorchetes y estamos en echemosunbitstazo.es"
  >>> mensaje.replace("sincorchetes","anonymous")
  'Hola mundo, me llamo anonymous y estamos en echemosunbitstazo.es'


Separar un :code:`str` cuando encuentre un caracter específico y devolver el resultado como una lista :code:`list`:

.. code-block:: python

  >>> mensaje = "Hola mundo, me llamo sincorchetes y estamos en echemosunbitstazo.es"
  >>> mensaje.split(" ")
  ['Hola',
   'mundo,',
   'me',
   'llamo',
   'sincorchetes',
   'y',
   'estamos',
   'en',
   'echemosunbitstazo.es']


Busca en el :code:`str` un :code:`str` y devuelve el nº de coincidencias:

.. code-block:: python

  >>> hi = "Hello"
  >>> hi.count("l")
  2

Convertir todos los caracteres de un :code:`str` a mayúsculas:

.. code-block:: python

  >>> hi = "Hello"
  >>> hi.upper()
  'HELLO'

Convertir todos los caracteres de un :code:`str` a minúsculas:

.. code-block:: python

  >>> hi = "HELLO"
  >>> hi.lower()
 'hello'

Convertir el primer caracter de un :code:`str` en mayúscula:

.. code-block:: python

  >>> hi = "hello"
  >>> hi.capitalize()
  'Hello'

Obtener el valor máximo de un :code:`str`:

.. code-block:: python

  >>> valor = "!#aBcDeFghI"
  >>> max(valor)
  'h'

Obtener el valor mínimo de un :code:`str`:

.. code-block:: python

  >>> valor = "!#aBcDeFghI"
  >>> min(valor)
  '!'

Constantes
####

Las constantes como su nombre indica son valores que no se modificarán a lo largo de la vida del programa. Sin embargo en Python no se declaran a lo mejor como en otro lenguaje tipo PHP. Para hacerlo en Python, tenemos que respetar una forma de trabajo y sintaxis específicas.

1. Crea un archivo llamado :code:`constantes.py`
2. Define en el variables, todas en mayúsculas y seguidas de "_ _ _".
3. Importa tu archivo en tu proyecto.
4. Llama a la constante.

Veamos un ejemplo:

1. Creamos el archivo :code:`constantes.py`
2. Añadimos las siguientes variables:

.. code-block:: python
IP_SERVIDOR = '127.0.0.1'
PUERTO_SERVIDOR = 3306
NOMBRE_USUARIO = 'sincorchetes'
PASS_USUARIO = 'Foo1234'
NOMBRE_DB = 'Foo'

3. Creamos un archivo :code:`main.py`
4. Importamos el archivo y mencionamos a la constante.
.. code-block:: python
import constantes
print(constantes.IP_SERVIDOR)

Veremos que tendremos una salida:
.. code-block:: python
127.0.0.1


Así definiríamos una constante en Python.

Por otro lado, Python tiene unas constantes integradas que no estaría más echarles un vistazo, no son muchas, pero viene bien <a href="https://docs.python.org/3/library/constants.html" target="blank">saberlas</a>.

Números
####

Tenemos varios tipos de dato en Python como puede ser:

* :code:`int`
* :code:`long` (_no se usa más en Python 3_)
* :code:`float`
* :code:`complex`

int o números enteros
^^^^

* Este tipo de dato solo almacena números enteros (*positivos y negativos, nada de comas, ni decimales, ni fracciones*).
* Este tipo de dato no contiene ninguna restricción por parte del número de bits en Python y puede expandirse el límite de la memoria disponible.
* No se necesita ningún tipo de declaración especial para almacenar números muy largos.

.. code-block:: python

  >>> a = 1
  >>> b = -2
  >>> print(a - b)
  3


float o número de coma flotante
^^^^

Si necesitas utilizar decimales, este es el tipo de dato que buscar.

.. code-block:: python
  >>> x = 20.30
  >>> y = -33.99
  >>> z = 100.12
  >>> print(x - y - z)
  -45.83

complex o números complejos
^^^^

Se utilizan para diferentes tipos de cálculos aplicados a la geometría, física... La definición en Python es :code:`a+bj`, dónde :code:`a` es el número que se encuentra representado en los números reales; :code:`bj` es el número imaginario.

.. code-block:: python

  >>> a = 2+3j
  >>> print(a)
  2+3j


Tipos de datos especiales
####

Tenemos el valor :code:`None` que viene a ser el valor :code:`null` en otros lenguajes como SQL, se suele utilizar para declarar un campo con este valor *¡ojo, esto no quiere decir que esté vacío!*
