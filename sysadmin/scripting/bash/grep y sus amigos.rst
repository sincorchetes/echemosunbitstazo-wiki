grep y sus amigos
-----------------

Comando grep(1)
###############

Este es uno de los comandos más esencial de Bash, nos permite mostrar coincidencias en archivos en base a la cadena de caracteres que nosotr@s le pasemos, en otras palabras, si queremos buscar una palabra en un archivo de texto, :source:`grep(1)` es nuestro comando.

Sintaxis y ejemplos
*******************

Acorde con las indicaciones que nos proporciona la todopoderosa biblia de los comandos, :source:`man(1)` estos son 3 ejemplos que nos da :source:`man 1 grep`. 

.. code-block:: bash

  grep [OPCIONES] PATRÓN [FICHERO...]
  grep [OPCIONES] -e PATRÓN ... [FICHERO...]
  grep [OPCIONES] -f FICHERO ... [FICHERO...]

Tanto las opciones, como los patrones y los ficheros se pueden repetir dentro de la línea de ejecución de nuestro comando.

Vamos con los ejemplos:

.. code-block:: bash

  grep -o "Linux" /proc/version

Imprimirá la cadena "Linux" si la encuentra en el archivo, y la imprime tantas veces como la encuentre.

.. code-block:: bash

  grep -q "Linux" /proc/version

No imprime nada, es una opción en la que se omite la salida, si encuentra una coincidencia con dicha palabra, devolverá en el estado de la shell un 0.
:source:`echo $?` = 0 si se encontró y = 1 en el caso contrario.

.. code-block:: bash

  grep -H "sda" /proc/* 2>/dev/null

Muestra en cada línea en la que encuentre coincidencias, también el nombre del archivo y omite errores.

.. code-block:: bash

  grep -A 2 "_this_module" /proc/kallsyms

Muestra las 2 líneas siguientes de haber encontrado la coincidencia en la o las líneas.

.. code-block:: bash

  grep -B 2 "_this_module" /proc/kallsyms

La inversa de la anterior, en vez de mostrar las 2 líneas siguientes, muestra las dos líneas anteriores a la coincidencia.

.. code-block:: bash

  grep -C 2 "_this_module" /proc/kallsyms

Si la A y la B hacía cada cosa por separado, con la C podemos mostrar tanto las líneas anteriores como las posteriores. En este caso muestra el resultado de las dos sentencias anteriores en una sola sentencia.

.. code-block:: bash

  grep -rA 2 "gcc" /proc/ 2>/dev/null

Buscará de forma recursiva en todos los ficheros y directorios que se encuentren dentro del directorio especificado y cuándo obtenga una coincidencia, imprimirá las 2 líneas anteriores a la coincidencia incluyendo el nombre del archivo en el que se encuentre.

.. note::

  El uso del parámetro -r ya incluye el parámetro -H por defecto

.. code-block:: bash

  grep -U "note" /bin/cp

Pretendemos encontrar una coincidencia dentro de un binario, y que en caso de encontrarla, ésta nos lo diga mediante un mensaje de salida.

.. code-block:: bash

  grep -ob "root" /etc/passwd

Nos mostrará las líneas en dónde la coincidencia se haya repetido n veces dentro de un fichero especificado.

.. code-block:: bash

  grep -obrA 2 "root" /etc 2>/dev/null

Permite efectuar lo mismo, pero se visualizarán las 2 líneas en cada coincidencia encontrada, número de línea, nombre de archivo dentro de un directorio y se omitirán los mensajes de error.

.. code-block:: bash

  grep -FrB 2 '/usr' /proc 2>/dev/null

Permite utilizar caracteres especiales para la búsqueda de coincidencias. Este comando buscará de forma recursiva la cadena que contiene un carácter "prohibido" y mostrará las 2 líneas anteriores cada vez que encuentre una coincidencia. También omitirán los mensajes de error.

.. code-block:: bash

  grep -ErC 2 '??linux' /proc 2>/dev/null

Al contrario que el anterior, aquí utilizaremos expresiones regulares como es el caso de ?? que sustituye a un caracter por signo de interrogación que no recordemos o no estemos seguro de cuál puede ser. Esta sentencia imprimirá las dos líneas siguientes a las coincidencias así mismo como las 2 anteriores, los mensajes de error se omitirán y se visualizará el nombre de los archivos que contengan dichas coincidencias

Los amigos de grep, fgrep(1) y egrep(1)
#######################################

Pues ya los hemos dado en los dos ejemplos anteriores, aunque no lo creamos, :source:`fgrep(1)` como :source:`egrep(1)` son dos comandos que actúan como alias.

* :source:`fgrep(1)` equivale a :source:`grep -F`
* :source:`egrep(1)` es igual a :source:`grep -E`

Fuentes
#######

* man pages ~ :source:`grep(1)`