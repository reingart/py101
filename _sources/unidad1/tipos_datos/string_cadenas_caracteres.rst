Cadenas de caracteres (str)
---------------------------

En python los strings se pueden armar tanto con comillas simples (')
como dobles ("), lo que no se puede hacer es abrir con unas y cerrar con
otras.

.. activecode:: py_15
    :nocodelens:

    cadena_caracteres = 'Holamundo'
    print(cadena_caracteres)
    print(type(cadena_caracteres))
    
    cadena_caracteres = "Y con doble comilla?, de qué tipo es?"
    print(cadena_caracteres)
    print(type(cadena_caracteres))


Además, se pueden armar strings multilínea poniendo tres comillas
simples o dobles seguidas:

.. activecode:: py_16
    :nocodelens:

    cadena_caracteres = """y si quiero
    usar un string
    que se escriba en varias
    líneas?."""
    print(cadena_caracteres)
    print(type(cadena_caracteres))


Índices y Rebanadas en string
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Si queremos obtener un caracter del string podemos acceder a él
simplemente con poner entre corchetes su posición (comenzando con la 0):

.. activecode:: py_18
    :nocodelens:

    cadena_caracteres = 'Hola mundo'
    print(cadena_caracteres)
    print('El septimo caracter de la cadena "{0}" es "{1}"'.format(cadena_caracteres, cadena_caracteres[6]))


+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+
| H   | o   | l   | a   |     | m   | u   | n   | d   | o   |
+=====+=====+=====+=====+=====+=====+=====+=====+=====+=====+
| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+

Aunque también nos podemos referir a ese caracter comenzando por su
posición, pero comenzando a contar desde la última posición (comenzando
en 1):

.. activecode:: py_19
    :nocodelens:

    cadena_caracteres = 'Hola mundo'
    print('El septimo caracter de la cadena "{0}" es "{1}"'.format(cadena_caracteres, cadena_caracteres[-4]))


+-------+------+------+------+------+------+------+------+------+------+
| H     | o    | l    | a    |      | m    | u    | n    | d    | o    |
+=======+======+======+======+======+======+======+======+======+======+
| 0     | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    |
+-------+------+------+------+------+------+------+------+------+------+
| -10   | -9   | -8   | -7   | -6   | -5   | -4   | -3   | -2   | -1   |
+-------+------+------+------+------+------+------+------+------+------+

Lo que no se puede hacer es cambiar sólo una letra de un string:

.. activecode:: py_20
    :nocodelens:

    cadena_caracteres = 'Hola mundo'
    cadena_caracteres[6] = 'x'


Aunque a veces lo que queremos es una parte del string, no todo:

.. activecode:: py_21
    :nocodelens:

    cadena_caracteres = 'Hola mundo'
    print(cadena_caracteres)
    print(cadena_caracteres[3])
    print(cadena_caracteres[2:8])     # Con los dos índices positivos
    print(cadena_caracteres[2:-2])    # Con un índice negativo y otro positivo
    print(cadena_caracteres[-8:8])    # Con un índice negativo y otro positivo
    print(cadena_caracteres[-8:-2])   # Con ambos índices negativos
    print(cadena_caracteres[2:-2:3])  # Y salteándose de a dos


Aunque lo más común es quitar el último carácter, por ejemplo, cuando es
un Enter:

.. activecode:: py_22
    :nocodelens:

    cadena_caracteres = 'Hola mundo\n'
    print(cadena_caracteres)
    print(cadena_caracteres[:-1])
    print(cadena_caracteres[:-5])


