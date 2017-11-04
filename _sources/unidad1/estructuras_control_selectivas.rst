Estructuras de control selectivas
=================================

Para ejecución condicional, se utilizan las siguientes sentencias en Python:

.. toctree::
      :maxdepth: 1

      if.rst

Operadores condicionales
^^^^^^^^^^^^^^^^^^^^^^^^

Para trabajar con valores verderos o falso, se pueden utilizar los siguientes
operadores booleanos:

* ``not x`` devuelve ``True`` si x es falso, de lo contrario devuelve ``False``
* ``x and y`` en general equivale a ``True`` si ambas (x e y) son verdaderas
* ``x or y`` en general equivale a ``True`` si cualquiera (x o y) es verdadera

Expresiones condicionales (if corto)
------------------------------------

Una forma de escribir el ``if`` y ``else`` en una sola línea es poner:

.. code:: python

    variable = valor1 if condicion else valor2

La variable contendrá el valor1 si la condición evalua a verdadero, de lo
contrario contendrá el valor2.


Por ejemplo, dado que ``%`` permite calcular el resto de una división:

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



