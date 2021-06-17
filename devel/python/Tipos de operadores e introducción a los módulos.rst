Tipos de operadores
----

En Python tenemos varios tipos de oepradores para hacer comparaciones, cálculos, valorar expresiones lógicas...

* Aritmético
* Asignación
* Comparación
* Lógico
* Bit a bit (*bitwise*)
* Identidad
* Membresía

Aritméticos
####

Se utiliza para realizar operaciones matemáticas y se utilizando dos operandos para llevarlas a cabo.

|----------|-------------|
| Operador | Descripción |
|==========|=============|
|+| Se utiliza para realizar operaciones de adicción (suma) |
|----------|-------------|
|-| Operaciones de sustracción (resta) |
|----------|-------------|
|*| Multiplicación |
|----------|-------------|
|/| División (cociente) |
|----------|-------------|
|%| Módulo (_resto de una división_) |
|----------|-------------|

Adicción
^^^^

.. code-block:: python

  >>> 2 + 3
  5

Sustracción
^^^^

.. code-block:: python

  >>> 1 - 2
  -1


Multiplicación
^^^^

.. code-block:: python

  >>> 2 * 1
  2

División (cociente)
^^^^

.. code-block:: python

  >>> 4 / 2
  0

Módulo, (*resto de una división*)
^^^^

.. code-block:: python

  >>> 4 % 2
  2.0


Operadores de asignación
####

Estos operadores permiten asignar valores, por norma general a variables, pero no olvidemos que podemos involucrar otros tipos de identificadores como pueden ser listas, tuplas...

|----------|-------------|
| Operador | Descripción |
|==========|=============|
| = | Asigna un valor |
|----------|-------------|
| += | Suma un valor al valor actual y guardar el nuevo valor |
|----------|-------------|
| -= | Resta un valor al valor actual y guardar el nuevo valor |
|----------|-------------|
| *= |  Multiplica un valor al valor actual y guardar el nuevo valor |
|----------|-------------|

Igual (=)
^^^^

.. code-block:: python

  >>> variable = 10
  >>> print(variable)
  10


Más e igual (+=)
^^^^

.. code-block:: python

  >>> variable = 1
  >>> variable += 2
  >>> print(variable)
  3

Menos e igual (-=)
^^^^

.. code-block:: python

  >>> variable = 1
  >>> variable -= 2
  >>> print(variable)
  -1

Multiplicar e igual (*=)
^^^^

.. code-block:: python

  >>> variable = 2
  >>> variable *= 2
  >>> print(variable)
  4


Operadores de comparación
####

Estos operadores te permiten realizar una comparación entre dos valores, son muy utilizados en los condicionales o en validaciones como pueden ser bucles...etc. Además, los valores comparados devuelven un :code:`True` o un :code:`False` (*booleano*) si la comparación se cumple o no.

|----------|-------------|
| Operador | Descripción |
|==========|=============|
| <        | Menor que         |
|----------|-------------|
| >        | Mayor que         |
|----------|-------------|
| <=       | Menor o igual que |
|----------|-------------|
| >=       | Mayor o igual que |
|----------|-------------|
| !=       | Distinto de       |
|----------|-------------|

Menor que:
^^^^

.. code-block:: python

  >>> 1 < 2
  True

Mayor que:
^^^^

.. code-block:: python

  >>> 1 > 2
  False

Menor igual que:
^^^^

.. code-block:: python

  >>> 1 <= 2
  True

Mayor igual que:
^^^^

.. code-block:: python

  >>> 1 >= 2
  False

Distinto de:
^^^^

.. code-block:: python

  >>> 1 != 2
  True


Operadores lógicos
####

Estos permiten realizar operaciones lógicas y devuelven :code:`True` o :code:`False` según el resultado.

|----------|-------------|
| Operador | Descripción |
|==========|=============|
| `and` | Deben cumplirse las condiciones sí o sí |
|----------|-------------|
| `or` | Debe cumplir al menos una de las condiciones evaluadas |
|----------|-------------|
| `not` | Devuelve `False` si el resultado es verdadero |
|----------|-------------|

and
^^^^

.. code-block:: python

  >>> 1<2 and 2<3
  True
  >>> x = 100 < 20 and 2>3
  >>>print(x)
  False


or
^^^^

.. code-block:: python

  >>> 1<2 and 100>100
  True


not
^^^^

.. code-block:: python

  >>> not(2 != 100 and 90<200)
  False


Operadores *bitwise*
####

|----------|-------------|
| Operador | Descripción |
|==========|=============|
| &| Convierte el primer y segundo nº decimal en nº binarios, compara ambos nº. Cuando se encuentra 1 bit en el primer nº, y en el segundo también, se establece 1. 
Cuando se encuentra 1 bit en el primer nº y un 0 en el segundo también se establece un 0. |
|----------|-------------|
| \| | Convierte el primer y segundo nº decimal en nº binarios, compara ambos nº. Cuando se encuentra 1 bit en el primer nº, y en el segundo también, se establece 1. Cuando se encuentra 1 bit en el primer nº y un 0 en el segundo también se establece un 1. |
|----------|-------------|
| >> | Convierte el primer y segundo nº decimal en nº binarios, compara ambos nº. Cuando se encuentra 1 bit en el segundo nº, y se desplaza el bit en el segundo también, se establece 1. Cuando se encuentra 1 bit en el primer nº y un 0 en el segundo también se establece un 1. |
|----------|-------------|
| << | Lo anterior pero desde la izquierda|
|----------|-------------|
| ~ | Devuelve el complemento del nº menos el nº que obtenemos cambiado cada 1 por un 0 y un 0 por un 1. Es lo mismo que -nº-1 |
|----------|-------------|

Ampersan (&)
^^^^

.. code-block:: python

  >>> 7 & 2
  2

¿Por qué nos devuelve 2? Si nosotros pasamos a binario ambos números:

.. code-block:: python

  7 = 0 0 0 0 0 1 1 1
  2 = 0 0 0 0 0 0 1 0


Cuando coincida el 1 del primer valor, con el 1 del segundo quedará como 1. Si el primer valor hay un 0 y en el segundo hay 1, se quedará el 0 por encima del 1 quedando tal que así:

.. code-block::

  0 0 0 0 0 1 1 1
  0 0 0 0 0 0 1 0
  ---------------------
  0 0 0 0 0 0 1 0

Si conviertes este número binario a decimal te dará 2.

Tubería o *pipe*
^^^^


.. code-block:: python

  >>> 190 | 9
  191

¿Por qué nos devuelve 191? Si nosotros pasamos a binario ambos números:

.. code-block::

  190 = 1 0 1 1 1 1 1 0
  9 = 0 0 0 0 1 0 0 1

Cuando coincida el 1 del primer valor, con el 1 del segundo quedará como 1. Si el primer valor hay un 0 y en el segundo hay 1, se quedará el 1 por encima del 0 quedando tal que así:

.. code-block::
  1 0 1 1 1 1 1 0
  0 0 0 1 0 0 0 1
  ---------------------
  1 0 1 1 1 1 1 1

Si conviertes este número binario a decimal te dará 191.

Desplazamiento hacia la derecha o (*shift-to-right*)
^^^^

.. code-block:: python
  >>> 10 >> 2
  2

¿Por qué nos devuelve 2? Si pasas el nº 10 a binario:

.. code-block::
  
  10 = 0 0 0 0 1 0 1 0

Desplazas 2 posiciones añadiendo dos ceros hacia la derecha, y te quedaría:

.. code-block::

  0 0 0 0 0 0 1 0

Si conviertes este número binario a decimal te dará 2.

Desplazamiento hacia la izquierda o (*shift-to-left*)
^^^^

Este procedimiento es el mismo que el anterior, pero hacia el otro lado.

.. code-block:: python

  >>> 10 << 2
  40

¿Por qué devuelve 2? Si pasas a binario el nº 10:

.. code-block::
  
  10 = 0 0 0 0 1 0 1 0

Desplazas 2 posiciones añadiendo dos ceros hacia la izquierda, y te quedaría:

.. code-block::

  0 0 1 0 1 0 0 0

Si conviertes este número binario a decimal te dará 40.

Inversión *bitwise*
^^^^

.. code-block:: python
  >>> ~100
  -101

¿Por qué devuelve -101? Devuelve el complemento del nº menos el nº que obtenemos cambiado cada 1 por un 0 y un 0 por un 1. Es lo mismo que -nº-1

Operador de identidad
####

Prueba si dos operandos comparten una identidad. Aquí hay dos tipos de operadores :code:`is` e :code:`is not`.

is
^^^^

Por ejemplo, comparamos si un valor almacenado en x es igual a su valor:

.. code-block:: python

  >>> x = 10
  >>> x is 10
  True

is not
^^^^

Aquí utilizamos el ejemplo anterior pero a la inversa.

.. code-block:: python

  >>> x = 10
  >>> x is not 10
  False


Operadores de membresía
####

Estos operadores permiten verificar si hay un :code:`str` en otro :code:`str`, :code:`list`, :code:`dict`, :code:`tuple`... 
Se utiliza :code:`in` para buscar y devolver :code:`True` si encuentra dicho :code:`str`, o, `not in` para verificar que no está.

in
^^^^


.. code-block:: python

  >>> "echemos" in "echemos un bitstazo"
  True

not in
^^^^


.. code-block:: python

  >>> ".es" not in "echemos un bitstazo"
  True

Módulos
----

¿Qué son los módulos? Los módulos son fragmentos de código que contienen librerías... que elaboran otros usuarios o que ya vienen integradas con Python. Hay muchos módulos que vienen ya pre-instalados en el sistema como pueden ser :code:`os` que permite interactuar con el sistema operativo; :code:`subprocess` que permite ejecutar comandos de shell; :code:`json` con el que podremos trabajar con archivos o salidas JSON...

¿Cómo cargar este código?
#####

El código de los módulos puede cargarse utilizando la palabra :code:`import`, como en el siguiente ejemplo:

.. code-block:: python

  >>> import json

También podemos cargar parte del código de los módulos como por ejemplo :code:`random` es un módulo que contiene métodos y propiedades. Podemos cargar solo uno de los métodos que tienes como es :code:`.random()` y asignarle un alias para trabajar con él como en le siguiente ejemplo:

.. code-block:: python

  >>> from random import random as GenerarAleatorio
  >>> GenerarAleatorio()
  0.9037083824066462


¿Qué pasa si no me sé las propiedades o métodos de un módulo?
####

No pasa nada, puedes revisar siempre la documentación de Python pulsando `aquí <https://docs.python.org/3/>`_

