Condicionales
-------------

Condicional if
##############

Esta estructura de control te permite evaluar una condición y ejecutar un trozo de código si la cumple.

.. code-block:: python

  >>> if (condición):
  >>>  Bloque de código


Condicional if-else
###################

El :code:`if-else` es una estructura de control que permite hacer 1 cosa si se cumple la condicioń, si esta no se cumple, únicamente se ejecutará un bloque de código sin contemplar otras posibilidades.

.. code-block:: python

  if (condición 1):
    Bloque de código
  else:
    Bloque de código

Veamos un ejemplo, Si tenemos un coche de marca Opel, emitirás un mensaje que diga "Tienes un Opel", si no es así, mostraremos un mensaje que diga que "No tienes un coche Opel".

.. code-block:: python

  >>> marca = "Citröen"
  >>> if (marca == "Opel"):
  >>>   print("Tienes un Opel")
  >>> else:
  >>>  print("No tienes un coche Opel")
  'No tienes un coche Opel'


Condicional if-elif-else
########################

¿Pero qué pasa cuando queremos comprobar múltiples condiciones? No podemos estar anidando :code:`if-else` como si no hubiese un mañana uno dentro del otro. Para eso tenemos la estructura :code:`if-elif-else`. Esta estructura nos permite hacer 1 cosa u otra en base a una condición, la cuál estará compuesto por uno o múltiples operadores como aritméticos, lógicos...

.. code-block:: python

  if (condición 1):
    Bloque de código
  elif (condición3):
    Bloque de código
  elif (condición2):
    Bloque de código
  else:
    Bloque de código

Veamos un ejemplo, Si tenemos un coche de marca Opel, emitirás un mensaje que diga "Tienes un Opel", si no es así, mostraremos un mensaje que diga que "No tienes un coche Opel".

.. code-block:: python

  >>> marca = "Citröen"
  >>> if (marca == "Opel")
  >>>   print("Tienes un Opel")
  >>> elif (marca == "Citröen")
  >>>   print("Tienes un coche Opel")
  >>> elif (marca == "Audi"):
  >>>   print("Tienes un Audi")
  >>> else:p
  >>>   print("Tu marca de coche no está registrada")
  Tienes un coche Citröen

Todo esto se puede complicar aún más haciendo uso de otros operadores y de otros :code:`if-elif-else` anidados, por ejemplo, utilizaremos los operadores de comparación con lógicos tal que así:

.. code-block:: python

  >>> marca_coche = "Toyota"
  >>> modelo_coche = "AE87"
  >>> motor_coche = 1600
  >>> if (marca_coche == "Toyota" and modelo_coche == "AE92"):
  >>>   if (motor_coche == 1600):
  >>>     print("Perfecto")
  >>>   elif (motor_coche == 1400):
  >>>     print("Bien")
  >>>   elif (motor_coche == 1200):
  >>>     print("Cuidado con las cuestas")
  >>>   else:
  >>>     print("Esto huele a chasis")
  >>> elif (marca_coche == "Citröen" and modelo_coche == "Saxo"):
  >>>   print("Enhorabuena, tienes un coche que pesa poco y corre mucho.")
  >>> else:
  >>>   print("Error 404, Tu coche no encontrado.")
  Error 404, Tu coche no encontrado.

Este mensaje se produce porque en el primer condicional estamos esperando recibir el modelo AE92, y sin embargo, recibimos el AE87; como en la segunda condición (:code:`elif`) requiere del modelo "Citröen" también queda descartado imprimiendo el mensaje "Error 404, Tu coche no encontrado.". No obstante, si cambiamos :code:`modelo_coche` por AE92 y volvemos a ejecutar las sentencias, veremos que recibiremos el mensaje de: "Perfecto".

Bucles
######

Bucle for
*********

¿Qué ocurre si queremos recorrer una lista o generar múltiples ejecuciones de código? Pues evidetenmente con un :code:`if` no nos vale, ya que solo nos permite validar una condicioń, y cuando la valide, esta dejará de ejecutarse.

.. code-block:: python

  for variable_interactiva in secuencia:
    Bloque código

¿Cómo funciona?
^^^^^^^^^^^^^^^

En :code:`secuencia` va una condición, podemos poner que recorra todos los valores de una lista y nos lo imprima por :code:`variable_interactiva`.

.. code-block:: python

  >>> frutas = [ "Peras", "Manzanas", "Arándanos", "Pomelo"]
  >>> for fruta in frutas:
  >>>   print(fruta)
  Peras
  Manzanas
  Arándanos
  Pomelo

También se puede hacer ejecuciones por el tamaño de la lista:

.. code-block:: python

  >>> frutas = [ "Peras", "Manzanas", "Arándanos", "Pomelo"]
  >>> for fruta in range(0 ,len(frutas)):
  >>>   print("Esta es la posición", fruta,"de la fruta: ",frutas[fruta])
  Esta es la posición 0 de la fruta:  Peras
  Esta es la posición 1 de la fruta:  Manzanas
  Esta es la posición 2 de la fruta:  Arándanos
  Esta es la posición 3 de la fruta:  Pomelo

¿Cómo podemos hacer, que se hagan :code:`n` ejecuciones para hacer tal cosa? 
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Con la función :code:`range()`.

.. code-block:: python

  >>> for x in range(0,100):
  >>>   print(x)
  0
  1
  2
  3
  4
  [... Corto aquí porque llega hasta 99 ...]

¿Por qué hasta 99 y no 100? 
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Porque recordemos que el valor 0 es una posición que se cuenta, realmente es :code:`n - 1`.

¿Cómo puedo romper una ejecución?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Tenemos el comando :code:`break` que rompe la ejecución del código, por lo que me han enseñado, es mejor finalizar las cosas como tocan en vez de usar este tipo de "cañones". Pero que sepamos que lo podemos usar. Normalmente se usan cuando hay condicionales añadidos, esto no quiere decir que se siga ejecutándo el resto del programa que tengamos, solo se frena el bucle :code:`for` que hemos invocado en nuestro fragmento de código.

.. code-block:: python

  >>> for x in range(0,100):
  >>>   print(x)
  >>>   if (x == 4):
  >>>     break
  0
  1
  2
  3
  4
  [... Se para la ejecución ...]

Bucle while
***********

Este bucle se repetirá hasta que la condición se cumpla. 

.. code-block:: python

  >>> while ( condicion ):
  >>>   # Bloque de código

Un ejemplo sencillo puede ser:

.. code-block:: python

  >>> a = 1
  >>> while a < 10:
  >>>   print(a)
  >>>   a += 2
  0
  2
  4
  6
  8

break, continue, pass
*********************

Estas tres sentencias permiten modificar la interacción de los bucles.
:code:`break`: Rompe toda la ejecución de un bucle.

.. code-block:: python

  for x in range(0,10):
    if x == 5:
      break
    print(x)

Veremos que la ejecución cuando llega a 5 el bucle se para a pesar de que le hemos dicho que el bucle vaya de 0 a 10 e imprimirá como último valor 4.

:code:`continue`: Se salta la ejecución en ese momento de la condición del bucle, pero sigue iterando el resto de elementos del bucle hasta finalizar.

.. code-block:: python

  for x in range(0,10):
    if x == 5:
      continue
    print(x)

En este caso, observamos que cuando detecte que :code:`x = 5`, el valor 5 no se imprimirá, pero continuará realizando el resto de condición.

:code:`pass`: No ejecuta nada y deja que continue el flujo del bucle.

.. code-block:: python

  for x in range(0,10):
    if x == 5:
      pass
    print(x)

Se ejecutará como si no existiera la palabra reservada :code:`pass`.

Juego, Dragón VS Personaje
**************************

Un dragón nos estará golpeando hasta que nosotros matemos al dragón o el dragón nos mate a nosotros:

.. note::
  Vamos a llamar al módulo :code:`random` y lo llamaremos como :code:`TirarDados` que más tarde utilizaremos el método :code:`.random()` para generar números aleatorios que están comprendidos entre 0.n y 1.n y que, haciendo uso del método :code:`.round()` aproximaremos el número a favor del 1 o del 0.

.. code-block:: python
  :linenos:

  #!/usr/bin/env python3
  #
  # Juego elaborado por Álvaro Castillo
  # GPLv2
  #
  from random import random as TirarDados
  dragon_hp = 100
  personaje_hp = 100
  hit_dragon = 5
  hit_personaje = 5
  
  while True: 
    if personaje_hp == 0:
      print("Hemos ganado :)")
      break
    elif dragon_hp == 0:
      print("Ganó el Dragón :(")
      break
    else:
      pass
    dados=round(TirarDados())
    if ( dados == 0 ):
      dragon_hp -= hit_dragon
      print("¡Hemos golpeado al dragón!, le queda: ", dragon_hp, "de vida.")
    elif ( dados == 1):
     personaje_hp -= hit_personaje
     print("¡El dragón nos ha golpeado!, tenemos de vida:", personaje_hp,".")
    else:
     print("Hubo un fallo")

Este es el análisis resumido de este juego:

#. La vida de ambos duelistas están asignadas en una variable
#. El daño que quita cada uno de ellos también
#. La condición siempre es :code:`True` por lo que siempre se ejecutará originando un bucle infinito :code:`infinityLoop`
#. Si la vida de alguno de los duelistas llega a :code:`0`, se interrumpe el bucle usando :code:`break`
#. La variable :code:`dados` obtiene un número aproximado a :code:`1|0` dependiendo lo que salga.
#. Hay un condicional que dice si :code:`datos=1` ataca el dragón, si :code:`dados=0` atacamos nosotros.
#. Haciendo uso de los operadores de asignación, restamos el valor de afección a la vida del duelista afectado y se imprime un mensaje indicando quién ha golpeado a quién y cuánta vida le queda al duelista contrario.
#. Se repite el proceso hasta llegar al punto 4

Dando como resultado algo parecido a esto:

.. code-block:: 

  ¡El dragón nos ha golpeado!, tenemos de vida: 95 .
  ¡Hemos golpeado al dragón!, le queda:  95 de vida.
  ¡Hemos golpeado al dragón!, le queda:  90 de vida.
  ¡Hemos golpeado al dragón!, le queda:  85 de vida.
  ¡El dragón nos ha golpeado!, tenemos de vida: 90 .
  ¡Hemos golpeado al dragón!, le queda:  80 de vida.
  ¡Hemos golpeado al dragón!, le queda:  75 de vida.
  [...]

