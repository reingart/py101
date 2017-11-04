Tuplas (tuple)
--------------

Las
`tuplas <https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences>`__
son listas inmutables, es decir, que no se pueden modificar. Si no se
pueden modificar, ¿para qué existen?. Porque crearlas es mucho más
eficiente que crear listas y en muchas ocasiones, como con las
constantes, queremos crear variables que no se modifiquen.

.. activecode:: py_10
    :nocodelens:

    tupla = (1, 2, 3, 4)  # Se usa paréntesis en lugar de corchetes
    print(tupla)
    
    tupla = tupla[2:4]
    print(tupla)
    print(type(tupla))



