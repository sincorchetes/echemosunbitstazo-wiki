Aprendiendo scripting
---------------------

¿Cómo aprender?
###############

Realmente cuando hablamos de desarrollo se traduce literalmente en *por mucho que sepas, siempre aprenderás*. Porque se te olvida un :code:`done` en bucle, :code:`fi` en un condicional, una variable mal declarada...etc, esto es así y hay que sumarle que debemos estar constantemente mirando otros :code:`scripts` elaborados por terceras personas, practicar siempre que podamos porque esto nos ayudará a fianzar más los conocimientos que hemos aprendido aquí. Esto no es como memorizar un texto, haces examen y ¡ciao! ¡Implican muchas cosas! Como comprender conceptos abstractos, saber qué implica la ejecución de determinados comandos, conocer el sistema...etc

Pero no tenemos de que preocuparnos, todo es posible. Ahora le daremos paso a las variables y :code:`arrays`

Variables
#########

Las variables como hemos visto en su día en matemáticas, es un conjunto de caracteres alfanuméricos (peras, melones, X:sub:1, abc:sub:12) cuyo valor asignado varía o está sujeto a algún cambio.

En Bash las variables las podemos declarar directamente o mediante el uso del comando :code:`declare(1)` que lo hablaremos más adelante ya que permite generar diferentes tipos de 

Restricciones y usos
********************

Por norma general, las variables en mayúsculas se reservan para temas de administración y gestión del sistema.

Si utilizamos el comando :code:`env(1)`, veremos toda la ristra de variables de entorno que tenemos:

.. code-block:: bash

  LANG=en_US.utf8
  GDM_LANG=en_US.utf8
  HISTCONTROL=ignoredups
  DISPLAY=:0.0
  GUESTFISH_RESTORE=\e[0m
  HOSTNAME=set0.lan
  GTK_OVERLAY_SCROLLING=0
  COLORTERM=truecolor
  GUESTFISH_INIT=\e[1;34m
  IMSETTINGS_INTEGRATE_DESKTOP=yes
  KDEDIRS=/usr
  XDG_VTNR=1
  SSH_AUTH_SOCK=/home/sincorchetes/.cache/keyring-RYPSKZ/ssh
  XDG_SESSION_ID=2
  XDG_GREETER_DATA_DIR=/var/lib/lightdm-data/sincorchetes
  USER=sincorchetes
  GUESTFISH_PS1=\[\e[1;32m\]><fs>\[\e[0;31m\] 
  DESKTOP_SESSION=mate
  PT7HOME=/opt/pt
  [SALIDA ACORTADA]

No pueden empezar con números, signos @#~½!, deberán comenzar con al menos una letra y luego si es posible usar números:

Ejemplo de errores:

.. code-block:: bash

  @hola=23
  h!ola=23
  #o#=23
  3hola=23

Correcto:

.. code-block:: bash

  hola=23
  h014=23
  hola="Esto es un valor"

Declarando variables con texto
******************************

Si queremos añadir valores con cadenas a las variables, es muy importante comprender estas dos diferencias.
Podemos declarar ambas con doble comillado "", ó, comillado simple ''. El problema erradica, en que no son lo mismo, el ("") permite mostrar el contenido de una variable dentro de un texto, mientras que ('') interpreta el texto tal cual.

.. code-block:: bash

  $hw = "Hello World"
  echo "$hw for everyone"

  Hello World for everyone

.. code-block:: bash

  $hw = "Hello World"
  echo '$hw for everyone'
  $hw for everyone

Visualizando las variables de entorno/sistema
*********************************************

Tenemos a nuestra disposición el comando :code:`env(1)` que nos enseña todas las variables de entorno y de sistema que debemos respetar, vamos a comentar algunas de ellas.

+-----------------+----------------------------------------------------------------------------------------------------------------------+
| Nombre variable | Descripción                                                                                                          |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`HOME`    | Ruta de trabajo del usuario actual                                                                                   |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`PATH`    | Lista de directorios dónde el shell buscará ejecutables (binarios, scripts...)                                       |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`PS1`     | Prompt String 1, muestra el caracter, texto previo a la introducción de los comandos. :code:`[sincorchetes@set0 ~]$` |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`IFS`     | Internal Field Separator, separadores como tabulación, espacio, salto de línea, si está en blanco, se usan espacios  |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`MAIL`    | Ruta y archivo de los mensajes del (la) usuari@ que tienen que ver con el e-mail                                     |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`SHELL`   | Ruta del shell del usuario                                                                                           |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`LANG`    | Idioma y codificación                                                                                                |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`USER`    | Variable que identifica al/la usuari@ actual                                                                         |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`LOGNAME` | Nombre del login utilizado en inicio de sesión, por lo general suele ser el mismo que :code:`$USER`                  |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`HISTFILE`| Ruta de archivo del historial de comandos ejecutados en la shell                                                     |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`HISTSIZE`| Tamaño del archivo historial de comandos ejecutados en shell                                                         |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`OLDPWD`  | Directorio accedido anteriormente                                                                                    |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`PWD`     | Ruta actual                                                                                                          |
+-----------------+----------------------------------------------------------------------------------------------------------------------+
| :code:`RANDOM`  | Genera un número aleatorio comprendido entre 0 y 31767                                                               |
+-----------------+----------------------------------------------------------------------------------------------------------------------+


Eliminando una variable
***********************

Para eliminar una variable y su contenido, bastará con ejecutar el comando:

.. code-block:: bash

  unset variable

Variable con acceso solo lectura
********************************

Se puede establecer una variable cuyo contenido no cambia como si fuese una constante haciendo uso del comando :code:`readonly(1)`

.. code-block:: bash

  readonly ejemplo=2

Visualizando el contenido de una variable
*****************************************

Para visualizar una variable, bastará con utilizar el comando :code:`echo(1)`.

.. code-block:: bash

  ejemplo="Hola que tal"

  echo $ejemplo

Convertir una variable en global
********************************

En desarrollo, se puede entender variable global como aquella que es accesible en todo momento por el programa a pesar de encontrarse en una función de manera cerrada, y una variable local aquella que solo se produce una vez y posteriormente, una vez efectuada la ejecución del bloque de código acaba por auto-suprimirse como un mensaje del inspector Gadget.

Para poder hacerla accesible deberemos hacer uso del comando :code:`source(1)`. Si tenemos un archivo con variables y queremos cargarlas, bastará con ejecutar:

.. code-block:: bash

  source ruta_script

Y podremos acceder desde dónde queramos desde la shell dónde hayamos ejecutado dicho comando.

Utilizando variable para ayudarnos con los comandos
***************************************************

Por supuestísimo que podemos hacer uso de las variables para obtener una automatización.

.. code-block:: bash

  ejemplo=:code:`pwd`
  ls $ejemplo

.. note::

  No obstante, si tratamos de copiar archivos, directorios cuyas rutas se encuentran en variables, puede dar error, y es porque interpreta uno de los dos el nombre tal cual dando error. Para ello tendremos que utilizar el {}.

.. code-block:: bash

  ruta_archivo_origen = /etc/group
  ruta_archivo_destino = /home/$USER/Documentos

  cp ${ruta_archivo_origen} ${ruta_archivo_destino}

Sustituir cadenas en variables
******************************

Podemos sustituir los valores que se encuentran en las variables sin tener que reasignarlas, solo utilizando llaves.

Si la variable está vacía o no existe, el texto se autoasignará. Probaremos con una variable cualquiera que al hacerle un :code:`echo(1)` no mostrará valor alguno. Si está definida, mostrará el valor de la variable.

.. code-block:: bash

  echo $ejemplo

Posteriormente efectuamos:

.. code-block:: bash

  echo ${ejemplo:-Está aprobado}Está aprobado

Pero el valor y la variable desaparecen. Si está definida, mostrará el valor de la variable. Si queremos que perduren, haremos los siguiente:

.. code-block:: bash

  echo ${ejemplo:=Está aprobado}Está aprobadoecho $ejemploEstá aprobado

Por otro lado, si nos encontramos con una variable previamente declarada, pero no vacía, se puede sustituir utilizando el ":+", no es un cambio permanente.

.. code-block:: bash

  echo ${PS1:+[${USER}@:code:`pwd`]}

Y por último, si tenemos una variable que está vacía o que no exista, se interrumpe el script y mostrará el mensaje de error que le asignemos, si existe, devolverá el contenido de la variable:

.. code-block:: bash

  echo ${dsfsd:?[${USER}@:code:`pwd`]}bash: dsfsd: [sincorchetes@/home/sincorchetes]

Obtener el valor de una cadena
******************************

Si queremos obtener el número de caracteres que constituyen el valor de una variable podemos hacerlo:

.. code-block:: bash

  ejemplo="Hola que tal"echo ${#ejemplo}12

Operaciones aritméticas con variables
*************************************

Se pueden hacer operaciones aritméticas con variables si primeramente declaramos el tipo de dato a través del comando :code:`typeset(1)`.

+--------------------+---------------------------------------------------------+
| Operador           | Función                                                 |
+--------------------+---------------------------------------------------------+
| :code:`+ - * /`    | Sumar, restar, multiplicar, dividir                     |
+--------------------+---------------------------------------------------------+
| :code:`%`          | Nos da el módulo de la operación                        |
+--------------------+---------------------------------------------------------+
| :code:`< > <= =>`  | Establece comparaciones, :code:`1=True;` :code:`0=False`| 
+--------------------+---------------------------------------------------------+
| :code:`==`         | Igual que                                               |
+--------------------+---------------------------------------------------------+
| :code:`!=`         | Diferente de                                            |
+--------------------+---------------------------------------------------------+

Mostrar el resultado de la siguiente suma
*****************************************

.. code-block:: bash

  typeset -i aa=1200+2200echo $a3200

¿Son iguales estos resultados?

.. code-block:: bash

  typeset -i resultadoa=1200b=1200resultado=${a}==${b}echo $resultado1

Podemos encontrar muchos más operadores :code:`help let`.

Variables especiales
********************

No se pueden utilizar, suelen ser de solo lectura y notifican de algo ocurrido por lo general.

Saber si un comando se ejecutó con éxito o nop
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: bash

  echo $?

Nos devolverá un código al haber ejecutado un comando. Por lo general, 0 es que se ejecutó con éxito, 1 falló la ejecución del comando, 127 no encontró el ejecutable. Según el comando, ejecutable, binario... devuelve un código de error distinto.

Obtener el PID del shell actual
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

El PID proviene de Process ID, es el número que identifica un proceso, (*más adelante explicaremos qué son los procesos*) de la shell actual

.. code-block:: bash

  echo $$25382

PID del último proceso iniciado en segundo plano
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Si hemos ejecutado un binario y/o ejecutable en segundo plano, nos chivará el número de identificación de proceso.

.. code-block:: bash

  echo $!25982

Opciones del shell
^^^^^^^^^^^^^^^^^^

Son las características que tiene habilitadas la shell por defecto, en Fedora muestran las siguientes:

.. code-block:: bash
  
  echo $-himBHs

El significado lo podemos encontrar :code:`bash(1)`, sección *SHELL BUILTIN COMMANDS*:

* h: Recuerda la ubicación de los comandos a medida de que se buscan para ejecutarse.  Activado por defecto.
* i: Interactiva
* m: Modo monitor. El control de trabajos está activado.
* B: El intérprete de comandos permite una expansión del uso de las llaves y las varibles. Por ejemplo, :code:`echo a{d,c,d,b}e` devolverá :code:`ade ace abe`. Viene habilitado por defecto.
* H: Permite sustituir el estilo del histórico de comandos, se habilita por defecto pero debe tener la característica de interactivo (i).

Arrays (vectores)
#################

Los vectores, o también conocidos como *arrays* permiten almacenar un conjunto de datos en un solo espacio de la memoria. En otros lenguajes como PHP pueden anidarse y confinar múltiples conjuntos de datos dentro de un solo espacio de memoria creando *arrays* multidimensionales. 

Sin embargo, en Bash, esto no es posible, ya que solo podremos crear vectores de una sola dimensión y sin un índice personalizado mediante su creación. a menos que declaremos la posición como el resultado de una variable (* :code:`pagina1=1` = :code:`array[pagina1]="Valor"` *). El índice en este caso, se identifica mediante un número comprendido entre 0-(n) dónde "n" es el número de datos que hemos añadido cuando declaramos un *array*.

.. code-block:: bash

  $array = (a b c d )   Datos almacenados en cada una de las posiciones   ^    \_|_|_|_/      /*----------------------*\    |     |||      /   ==> a = 1234       \   Nombre     Datos    /  ==> b = "Hello world"   \   del    de  -------*   ==> c = :code:`pwd`         *    Array    Declarados   \  ==> d = $resultado     /                \*-----------------------*/

En este caso, para acceder al valor de cada letra correspondiente, tendremos que hacer uso de: :code:`$nombre_array` + [:code:`n`]. Dónde n es la posición del dato que queremos obtener.

Ejemplo:

.. code-block:: bash

  echo $array[0]||----> Obtendremos: 1234echo $array[1]||----> Obtendremos: Hello worldecho $array[2]||----> Obtendremos: /home/sincorchetes (en mi caso)

¿Cómo obtener la longitud de un *array*?
****************************************

Básicamente, de la siguiente forma:

.. code-block:: bash

  echo ${#array[*]}

Nos tendrá que dar como resultado "4", que son los valores declarados. (a= 1234, b = "Hello world"...)

¿Cómo obtener todos los valores de un *array*?
**********************************************

Sustituiremos el número de la posición por una @.

.. code-block:: bash

  echo ${array[@]}

¿Cómo añadir un nuevo valor a un índice específico de un array declarado?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Bastará con mencionar el número de posición que queremos asignar el nuevo dato:

.. code-block:: bash

  $array[10]="Hola que tal"

Visualizar el número de posiciones ocupadas dentro de un *array*
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Simplemente si queremos ver que posiciones están ocupadas para utilizar las que estén libres:

.. code-block:: bash

  echo ${!array[*]}

Ver cuánto tamaño contiene de largo una posición
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Para comprobar el tamaño, simplemente hacemos:

.. code-block:: bash

  echo ${#array[1]}

¿Cómo añadir un nuevo valor sin declarar posición en un *array*?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Simplemente si queremos añadir un dato nuevo sin especificar un índice en cuestión.

.. code-block:: bash

  array+=(nuevo_valor)

Eliminar una posición del array
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Utilizaremos el comando :code:`unset(1)` como se ha utilizado para eliminar variables declaradas.

.. code-block:: bash

  unset array[n]

Resultado de un comando que se separe como valores y que estos ocupen una posición dentro del *array*
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Esto quiere decir, que si asignamos un solo valor, cuyo valor sea el resultado de un comando, este generará una salida y todos los datos expuestos en la salida del comando se convertirán en un valor dentro de una posición. Por ejemplo, si hacemos un :code:`cat /etc/group`, obtendremos una salida similar a esta:

.. code-block:: bash

  root:x:0:bin:x:1:daemon:x:2:sys:x:3:adm:x:4:tty:x:5:disk:x:6:[SALIDA ACORTADA]

Bien, si le decimos al *array* que nos almacene esta lista para luego visualizarla, podemos hacerlo.

.. code-block:: bash

  array=(`cat /etc/group`)

Si hacemos un :code:`echo ${array[0]}` veremos que nos saldrá la primera línea del documento:

.. code-block:: bash

  root:x:0:

Si queremos obtener toda la lista:

.. code-block:: bash

  echo ${array[@]}

Condicionales
#############

Imaginémonos que vamos a comprar el pan y resulta de que o bien no hay, o bien sale más caro de lo que imaginamos, o bien no es el tipo que buscamos...etc, entonces tenemos que pensar ¿Qué hacer? y aquí entra en juego el uso de los condicionales.

Los condicionales son evaulaciones que aplicamos en determinados valores que obtenemos como resultado de una operación anterior, bloques de código que han sido ejecutados y que han devuelto alguna salida. Es decir, con el if **regularemos el flujo de trabajo de nuestro sript**, añadiendo diferentes situaciones para resultados diferentes.

Condicional If
**************

If permite añadir una situación diferente que en caso de que no se cumpla la condición, continuará ejecutando el resto del código. Este se puede elaborar en dentro de un script (*como haremos a partir de ahora*), o bien se puede ejecutar en una sola línea de ejecución en Bash.

Creamos un script dónde añadiremos el siguiente bloque de código.

.. code-block:: bash

  estado="Cerrado"
  parque=$estado

  if [ $parque == "Cerrado"]
  then
    echo "Está cerrado"
  fi

Si ejecutamos el código de arriba, nos devolverá un mensaje de que se encuentra cerrado. Sin embargo, si cambiamos "Cerrado" => "Abierto". La cosa cambia, ya que no producirá una salida.

.. code-block:: bash

  estado="Cerrado"
  parque=$estado

  if [ $parque == "Cerrado"]
  then
    echo "Está cerrado"
  fi

¿Por qué sucede esto? Porque como la condición no se cumple, ya que caracter-caracter se va comprobando que sean correctos dentro de la condición, en cuanto sea alguno de ellos distinto, se prosigue con el resto del código sin hacer nada al respecto. Si queremos decirle que ejecute otra instrucción de código utilizaremos la sentencia else.

.. code-block:: bash

  estado="Cerrado"
  parque=$estado

  if [ $parque == "Cerrado"]
  then
    echo "Está cerrado"
  else
    echo "Está abierto"
  fi

Pero... ¿Y si queremos añadir más condiciones? Un parque puede estar abierto, cerrado, en obras entre otras cosas. Para eso tenemos la sentencia if-elif.

Condicional If-elif
*******************

.. code-block:: bash

  estado="Abierto"
  parque=$estado

  if [ $parque == "Cerrado"]
  then
    echo "Está cerrado"
  elif [ $parque == "Abierto" ]
  then
    echo "Está abierto"
  fi

Más estados...

.. code-block:: bash

  estado="Obras"
  parque=$estado

  if [ $parque == "Cerrado"]
  then
    echo "Está cerrado"
  elif [ $parque == "Abierto" ]
  then
    echo "Está abierto"
  elif [ $parque == "Obras" ]
  then
    echo "Está en obras"

  else
    echo "Consulte al ayuntamiento de su ciudad"
  fi

Condicional en una simple linea
*******************************

Se pueden escribir condicionales en una sola línea, acortando todo el bloque de código en una sola instrucción reduciendo el consumo de memoria y de procesamiento, pero aumentando la complejidad de lectura para el desarrollador.

.. code-block:: bash
  
  if [ $parque == "Cerrado" ]; then  echo "Está cerrado" ; elif [ $parque == "Abierto" ]; then  echo "Está abierto" ; elif [ $parque == "Obras" ]; then echo "Está en obras" ; fi

¿Cómo evalúa if todo esto?
**************************

Los corchetes que incluimos como sintaxis del if, realmente esconden el comando :code:`test(1)`. Este comando básicamente compara valores, por ejemplo:

.. code-block:: bash

  [ 2 -eq 0 ]

Si hacemos un :code:`echo $?` para ver el resultado de la ejecución del comando, nos saldrá un 1 como señal de ARCHIVOALSE.

.. code-block:: bash

  [ 0 -eq 0 ]

Al hacer un :code:`echo $?` nos mostrará el 0, de verdadero.

Lo mismo da utilizar los corchetes como llamar directamente al comando.

.. code-block:: bash

  test 0 -eq 0

Veremos el resultado de la ejecución del comando, recordemos 0 es éxito !=0 puede ser un error.

.. code-block:: bash

  echo $?

Tabla de expresiones utilizadas
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Las siguientes expresiones devuelven todas verdadero en su defecto en caso de que cumplan la condición. Para ver el resultado, hay que verificar la salida de la ejecución del comando con :code:`echo $?`

+----------------------------------------------------+--------------------------------------------------------------------------------+
| Expresión en terminal                              | Descripción                                                                    |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -a ARCHIVO ]`                             | ARCHIVO existe                                                                 |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -b ARCHIVO ]`                             | ARCHIVO existe y es un fichero especial de bloques                             |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -c ARCHIVO ]`                             | ARCHIVO existe y es archivo especial de caracteres                             |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -d ARCHIVO ]`                             | ARCHIVO existe y es un directorio                                              |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -e ARCHIVO ]`                             | ARCHIVO existe                                                                 |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -f ARCHIVO ]`                             | ARCHIVO existe y es un archivo regular                                         |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -g ARCHIVO ]`                             | ARCHIVO existe y tiene el SGID asignado                                        |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -h ARCHIVO ]`                             | ARCHIVO existe y es un enlace simbólico                                        |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -k ARCHIVO ]`                             | ARCHIVO existe y tiene asignado sticky bit                                     |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -p ARCHIVO ]`                             | ARCHIVO existe y está nombrado como tubería (ARCHIVOIARCHIVOO)                 |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -r ARCHIVO ]`                             | ARCHIVO existe y tiene permisos de lectura                                     |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -s ARCHIVO ]`                             | ARCHIVO existe y tiene un tamaño mayor que 0                                   |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -t ARCHIVO ]`                             | La descripción del fichero de ARCHIVO está abierta y se refiere a una terminal |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -u ARCHIVO ]`                             | ARCHIVO existe y tiene SUID asignado                                           |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -w ARCHIVO ]`                             | ARCHIVO existe y puede escribirse en él                                        |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -x ARCHIVO ]`                             | ARCHIVO existe y es un ejecutable                                              |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -O ARCHIVO ]`                             | ARCHIVO existe y está gestionado por su usario                                 |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -G ARCHIVO ]`                             | ARCHIVO existe y está gestionado por su grupo                                  |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -L ARCHIVO ]`                             | ARCHIVO existe y es enlace simbólico                                           |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -N ARCHIVO ]`                             | ARCHIVO existe y se modificó desde la última vez que se leyó                   |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -S ARCHIVO ]`                             | ARCHIVO existe y es un socket                                                  |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ ARCHIVO1 -nt ARCHIVO2 ]`                  | ARCHIVO1 se modificó antes que ARCHIVO2, o si ARCHIVO1 existe y ARCHIVO2 no    |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ ARCHIVO1 -ot ARCHIVO2 ]`                  | ARCHIVO1 es más viejo que ARCHIVO2, o ARCHIVO2 existe y ARCHIVO1 no            |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ ARCHIVO1 -ef ARCHIVO2 ]`                  | ARCHIVO1 y ARCHIVO2 se refieren al mismo dispositivo y número de inodo         |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -o OPNAME ]`                              | Si la shell tiene la opción "OPTIONNAME" activdada :code:`bash -o`             |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -z STRING ]`                              | La longitud del STR es 0                                                       |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ -n STRING ]`                              | Si la longitud de STRING no es 0                                               |
+----------------------------------------------------+                                                                                +
| :code:`[ STRING ]`                                 |                                                                                |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ STR1 == STR2 ]`                           | Si las cadenas son iguales                                                     |
+----------------------------------------------------+                                                                                +
| :code:`[ STR1 = STR2 ]`                            |                                                                                |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ STR1 != STR2 ]`                           | Si las cadenas no son iguales                                                  |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ STR1 < STR2 ]`                            | STR1 se ordena antes que STR2 según como esté la localización configurada      |
+----------------------------------------------------+--------------------------------------------------------------------------------+
| :code:`[ STR1 > STR2 ]`                            | STR1 ordena después de STR2 en base al idioma del sistema                      |
+----------------------------------------------------+--------------------------------------------------------------------------------+


Expresiones para números
^^^^^^^^^^^^^^^^^^^^^^^^

Las siguientes condiciones solo son aplicables para números enteros, y devolverán verdadero en caso de cumplir la condición.

+-----------------------+----------------------------+
| Expresión en terminal | Descripción                |
+-----------------------+----------------------------+
| :code:`[ N1 -eq N2 ]` | N1 es igual que N2         |
+-----------------------+----------------------------+
| :code:`[ N1 -ne N2 ]` | N1 no es igual a N2        |
+-----------------------+----------------------------+
| :code:`[ N1 -lt N2 ]` | N1 es menor que N2         |
+-----------------------+----------------------------+
| :code:`[ N1 -le N2 ]` | N1 es menor o igual que N2 |
+-----------------------+----------------------------+
| :code:`[ N1 -gt N2 ]` | N1 es mayor que N2         |
+-----------------------+----------------------------+
| :code:`[ N1 -ge N2 ]` | N1 es mayor o igual que N2 |
+-----------------------+----------------------------+

Comparando múltiples valores
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Se pueden anidar condiciones para un determinado valor o conjunto de valores como podemos ver a continuación gracias a los operadores lógicos.

:code:`cmd1 && cmd2` => Si devuelve 0 (éxito), se ejecutará :code:`cmd2`
:code:`cmd1 || cmd2` => Si devuelve un número distinto a 0, se ejecutará :code:`cmd2`

+----------------------------------------------+-------------------------------------------------------------------------------------+
| Expresión en terminal                        | Descripción                                                                         |
+----------------------------------------------+-------------------------------------------------------------------------------------+
| :code:`[[ VAL1 -eq VAL2 && VAL3 -lt VAL1 ]]` | Si el VAL1 es igual a VAL2 y a su vez, VAL3 es menor que VAL1, devolverá verdadero  |
+----------------------------------------------+-------------------------------------------------------------------------------------+
| :code:`[[ VAL1 == VAL2 ]]`                   | Comprueba que VAL1 es igual a VAL2                                                  |
+----------------------------------------------+-------------------------------------------------------------------------------------+


Referencias
###########

* Ediciones ENI ~ LPIC-1
* StackOverflow - `Why echo outputs himBH on man bash shell <https://stackoverflow.com/questions/35432562/why-echo-outputs-himbh-on-man-bash-shell>`_
* Gulvi ~ `Curso programación Bash <https://gulvi.com/serie/curso-programacion-bash/capitulo/arrays-bash>`_
* StackExchange ~ `How can I remove an element from an array <https://unix.stackexchange.com/questions/68322/how-can-i-remove-an-element-from-an-array-completely>`_
* LinuxQuestions ~ `Bash array Add function example using indirect <https://www.linuxquestions.org/questions/programming-9/bash-array-add-function-example-using-indirect-array-reference-as-function-argument-815329>`_
* GNU.org ~ `Brace Expansion <https://www.gnu.org/software/bash/manual/html_node/Brace-Expansion.html?target=_blank>`_
