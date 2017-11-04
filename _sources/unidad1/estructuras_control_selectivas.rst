Estructuras de control selectivas
=================================

.. toctree::
      :maxdepth: 1

      if.rst


if corto
--------

Otra forma de escribir el if en una sola línea es poner:

.. code:: python

    variable = valor1 if condicion else valor2

Por ejemplo:

.. activecode:: py_32
    :nocodelens:

    num = 5
    es_par = True if (num % 2 == 0) else False
    print('5 es par?:', es_par)
    
    num = 6
    es_par = True if (num % 2 == 0) else False
    
    print('6 es par?:', es_par)


.. activecode:: py_33
    :nocodelens:

    nulo = None
    print(nulo)
    print(type(nulo))



