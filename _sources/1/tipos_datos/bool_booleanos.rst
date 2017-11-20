Booleanos (bool)
----------------

Python también soporta el tipo de dato booleano:

.. activecode:: py_11
    :nocodelens:

    boolean = True
    print(boolean)
    print(not boolean)
    print(type(boolean))
    print(True or False and True)


También se puede crear un boolean a partir de comparar dos números:

.. activecode:: py_12
    :nocodelens:

    boolean = 5 != 5
    print(boolean)


Incluso, se puede saber fácilmente si un número está dentro de un rango
o no.

.. activecode:: py_13
    :nocodelens:

    numero = 7
    if 5 < numero < 9:
        print('El número 7 se encuentra en el rango entre 5 y 9')
    
    if 5 < numero < 6:
        print('El número 7 se encuentra en el rango entre 5 y 6')

Muchas formas de imprimir el número 25

.. activecode:: py_14
    :nocodelens:

    print("--{0}--".format(25))
    print("--{0:4}--".format(25))    # Ocupando 4 espacios
    print("--{0:04}--".format(25))   # Ocupando 4 espacios y rellenando con 0
    print("--{0:b}--".format(25))    # En binario
    print("--{0:x}--".format(25))    # En hexadecimal
    print("--{0:04x}--".format(25))  # En binario y ocupando 4 espacios y rellenando con 0

