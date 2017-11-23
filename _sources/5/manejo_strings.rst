
.. raw:: html

   <!--
   29/10
   Archivos de texto. 
   Operaciones con cadenas de caracteres.
   String formaters.
   CLASE DE LABORATORIO 
   (Gonzalo)
   -->

Manejo de strings
=================

Con los strings podemos hacer `muchas
operaciones <https://docs.python.org/2/library/stdtypes.html#string-methods>`__:

.. activecode:: py_01
    :nocodelens:

    cadena_caracteres = "Hola mundo"
    print(dir(cadena_caracteres))

String formating
----------------

Existen varias formas crear, concatenar e imprimir strings:

¿Cómo imprimir un string?
~~~~~~~~~~~~~~~~~~~~~~~~~

Para imprimir un string sólo es necesario usar la palabra
`print <https://docs.python.org/2/library/functions.html#print>`__:

.. activecode:: py_02
    :nocodelens:

    print('Hola mundo')
    print('Pero el print también imprime un Enter al terminar la línea')



Pero si no queremos imprimir ese último Enter lo que tenemos que hacer
es poner una coma al final de la línea:

.. activecode:: py_03
    :nocodelens:

    print('Pero al usar end', end=" ")
    print('cambia el enter por un espacio')
    print('También puedo escribir lo mismo' ' en dos partes')
    print('Lo que puedo usar ' \
        'cuando un string es muy largo' \
        'si le agrego una contrabarra')



¿Y si lo que quiero es imprimir un número pegado al string?

.. activecode:: py_04
    :nocodelens:

    print('Entonces tengo que ponerlo después de la coma:', 5)
    print('Al que también le agrega la coma para separarlo')
    print('También puedo ponerlo en el medio:\nHoy es', 29, 'de Octubre')


`String formating <https://docs.python.org/2/library/string.html#new-string-formatting>`__
------------------------------------------------------------------------------------------

Pero en algunas ocasiones vamos a tener que crear springs más complejos
y agregarle una coma no va a ser suficiente, o tal vez queremos crearlos
pero no para imprimirlos, por lo que no podríamos usar la función print.
En esos casos, podemos usar la función
`format <https://docs.python.org/2/library/string.html#string.Formatter.format>`__

.. code:: python

    print(str.format.__doc__)


.. parsed-literal::

    S.format(*args, **kwargs) -> string
    
    Return a formatted version of S, using substitutions from args and kwargs.
    The substitutions are identified by braces ('{' and '}').


Format lo que hace es reemplazar las llaves con los parámetros que le
pasen:

.. activecode:: py_05
    :nocodelens:

    print('El nombre del jugador número {0} es {1}'.format(10, 'Lionel Messi'))


Aunque en realidad los números no son obligatorios:

.. activecode:: py_06
    :nocodelens:

    print('El nombre del jugador número {} es {}'.format(10, 'Lionel Messi'))


Pero la ventaja de usar los números es que podemos imprimir ese
parámetro varias veces, y no necesariamente en el órden que figura:

.. activecode:: py_07
    :nocodelens:

    print('{0}{1}{0}'.format('abra', 'cad'))


Incluso, se pueden usar parámetros nombrados:

.. activecode:: py_08
    :nocodelens:

    print('La nota del alumno {padron} - {nombre} es un {nota}.'
        .format(padron=123, nombre='Carlos Sanchez', nota=8))


Incluso, si en lugar de pasarle cada uno de los parámetros le pasamos un
diccionario usando el operador \*\*

.. activecode:: py_09
    :nocodelens:

    alumno = {
        'padron': 123,
        'nombre': 'Carlos Sanchez',
        'nota': 8
    }
    
    print('La nota del alumno {padron} - {nombre} es un {nota}.'
        .format(**alumno))



Incluso, si lo que le pasamos es una lista, podemos acceder a una
posición en particular:

.. activecode:: py_10
    :nocodelens:

    alumno = {
        'padron': 123,
        'nombre': 'Carlos Sanchez',
        'tps': [8, 9] 
    }
    
    print('La nota de los tps de {nombre} son {tps[0]} y {tps[1]}.'
        .format(**alumno))


Incluso puedo alinear el texto que pongo usando los dos puntos (:)

.. activecode:: py_11
    :nocodelens:

    print('Imprimo un texto alineado a la |{:<20}| de 20 posiciones'.format(
            'izquierda'))
    print('Imprimo un texto alineado a la |{:>20}| de 20 posiciones'.format(
            'derecha'))
    print('Imprimo un texto |{:^20}| de 20 posiciones'.format('centrado'))
    print('Relleno |{:#<20}| con #'.format('izquierda'))
    print('Relleno |{:#>20}| con #'.format('derecha'))
    print('Relleno |{:#^20}| con #'.format('centrado'))


Pueden ver más ejemplos en la `documentación oficial de
Python <https://docs.python.org/2/library/string.html#format-examples>`__\ 
También se puese usar el signo ``%`` para `construir un
string <https://docs.python.org/2/library/stdtypes.html#string-formatting-operations>`__,
aunque no suele quedar tan claro el código:

Funciones de los strings
------------------------

También existen varias
`funciones <https://docs.python.org/2/library/stdtypes.html#string-methods>`__
que podemos usar cuando trabajamos con strings:

.. activecode:: py_12
    :nocodelens:

    cadena_caracteres = 'Hola mundo'
    print('"{0}" cambia a "{1}" con title'.format(cadena_caracteres, cadena_caracteres.title()))
    print('"{0}" cambia a "{1}" con lower'.format(cadena_caracteres, cadena_caracteres.lower()))
    print('"{0}" cambia a "{1} con upper"'.format(cadena_caracteres, cadena_caracteres.upper()))
    print('"{0}" cambia a "{1}" con capitalize'.format(cadena_caracteres, cadena_caracteres.capitalize()))
    print('"{0}" cambia a "{1}" cuando reemplazamos las o por 0'.format(cadena_caracteres, cadena_caracteres.replace('o', '0')))
    
    x = 'mi string'
    y = x.replace('i', 'AA')
    print(x, y)
    print(id(x))
    x += 'Hola mundo'
    print(id(x))



Y también podemos separar y combinar strings:

.. activecode:: py_13
    :nocodelens:

    print("Hola mundo".split())
    print("Hola mundo".split('o'))
    print("Hola mundo".split('mu'))
    print(''.join(['Hola', 'mundo']))
    print(' '.join(['Hola', 'mundo']))
    var = '#separador#'.join(['Hola', 'mundo'])
    print(var)
    
    padron, nombre, nota = '12321,nom bekr,4'.split(',')




Unicodes
--------

Los strings ocupan 1 byte en memoria, por lo que sólo se pueden
representar 256 caractéres distintos; pero, si queremos representar los
caracteres de todos los idiomas, 255 caracteres no son suficientes.
Debido a esto, es que surgieron distintas codificaciones de los
archivos, como pueden latin-1 (iso-8859-1), utf-8, etc. Y si bien en un
principio esto fue una solución, la verdad es que con el tiempo trajo
mucho problemas por no saber cómo interpretar cada letra. Para
solucionar este problema es que Python introdujo en la versión 2.0 los
caracteres de tipo
`unicode <https://docs.python.org/2/library/functions.html#unicode>`__
que pasaron a ocupar 2 bytes, por lo que ahora se pueden representar
65.536 todos los caracteres necesarios. En Python 3 todos los strings
pasaron a ser del tipo Unicode.


