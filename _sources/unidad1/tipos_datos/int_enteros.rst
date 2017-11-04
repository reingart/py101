Enteros (int y long)
--------------------

Python 2 distingue dos tipos de enteros:

* int
* long

En Python 3 directamente existe un único tipo de entero, los int.

.. activecode:: py_01
    :nocodelens:

    # Asigno el número 5 a la variable numero_entero
    numero_entero = 5
    # Imprimo el valor que tiene la variable numero_entero
    print(numero_entero)
    # Imprimo el tipo de la variable numero_entero
    print(type(numero_entero))


Ahora, ¿qué pasa cuando ese número entero crece mucho?, por ejemplo, si
le asignamos 9223372036854775807

.. activecode:: py_02
    :nocodelens:

    # defino dos variables (no imprime)
    numero_entero = 5
    numero_muy_grande = -9223372036854775809

.. activecode:: py_03
    :nocodelens:
    :include: py_02

    print(numero_muy_grande)
    print(type(numero_muy_grande))
    print(2**16/2)


¿Y si ahora le sumamos 1?

.. activecode:: py_04
    :nocodelens:
    :include: py_02

    numero_muy_grande += 1
    print(numero_muy_grande)
    print(type(numero_muy_grande))


