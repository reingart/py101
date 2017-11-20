Tipos de datos básicos
======================

Los tipos de datos básicos (un único valor "atómico") a utilizar en este curso:

.. toctree::
      :maxdepth: 1

      tipos_datos/int_enteros.rst
      tipos_datos/float_reales.rst
      tipos_datos/complex_complejos.rst
      tipos_datos/string_cadenas_caracteres.rst
      tipos_datos/none_nulos.rst
      tipos_datos/bool_booleanos.rst

En Python a las variables se les puede preguntar de qué tipo son usando
la función type:

.. activecode:: py_00
    :nocodelens:

    variable = 'Hola mundo'
    tipo_de_la_variable = type(variable)
    print(tipo_de_la_variable)


Ingreso de datos desde teclado
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Python 3 permite solicitar al usuario que ingrese datos, utilizando la función
``input``:

.. activecode:: py_23
    :nocodelens:

    cadena = input('Ingrese una cadena de caracteres: ')
    print(cadena)
    print(type(cadena))


Y para convertirlo como entero, se puede usar el mismo tipo de datos `int`,
que actua como función de conversión:

.. activecode:: py_24
    :nocodelens:

    numero = int(input('Ingrese un número: '))
    print(numero)
    print(type(numero))

