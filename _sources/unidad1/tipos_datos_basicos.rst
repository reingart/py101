Tipos de datos básicos
======================

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

.. activecode:: py_23
    :nocodelens:

    numero = input('Ingrese un número: ')
    print(numero)
    print(type(numero))


Y para convertirlo como entero:

.. activecode:: py_24
    :nocodelens:

    numero = int(input('Ingrese un número: '))
    print(numero)
    print(type(numero))

