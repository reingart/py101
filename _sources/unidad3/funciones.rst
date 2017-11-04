Funciones
=========

Una de las premisas de Python era que *"La legibilidad cuenta"*, y el
uso de funciones ayudan mucho en que un código sea legible.

Las funciones permiten crear fragmentos de código que pueden llamarse en
diferentes situaciones, variando los parámetros de entrada y devolviendo
un resultado.

Para ello, se utilizan las siguientes instrucciones:

.. toctree::
      :maxdepth: 1

      def.rst
      return.rst


lambda (funciones anónimas)
---------------------------

Las funciones más simples en Python se pueden construir con expresiones
``lambda``.

Por ejemplo, para definir una función que calcule el promedio (recibe una
lista de valores y devuelve el resultado de la suma dividido la cantidad):


.. activecode:: py_01

   promedio = lambda valores: sum(valores) / len(valores)

   print(promedio([4, 10]))
   print(promedio([5, 5, 7, 7]))


La `funcion lineal <https://es.wikipedia.org/wiki/Funci%C3%B3n_lineal>`_

.. math:: f(x) = mx + b

también podría ser definida de forma simple:

.. activecode:: py_00

    # defino una funcion lineal:
    m = 3
    b = 2
    f = lambda x:  m * x + b

    print("x", "y")
    for x in range(10):
        # llamar a la funcion lineal
        y = f(x)
        print(x, y)


