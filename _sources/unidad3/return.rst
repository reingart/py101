return
------

En Python no existen los procedimientos: son todas funciones.
Incluso, aunque nosotros no devolvamos ningún valor, Python lo hará por
nosotros, retornando ``None``.

El ejemplo anterior, la función simplemente imprimia el resultado, no lo
devolvía, por lo que dicho valor se "pierde" y no puede ser utilizado
posteriormente.

La forma de devolver valores es, usando la palabra reservada **return**
y el valor a retornar. Y de igual forma, una vez que se ejecuta esa
sentencia, no se ejecuta ninguna sentencia más de esa función;
sin importar si está dentro de un ciclo o todavía no hayamos hecho nada.

Por ejemplo:

.. activecode:: py_01

    def sumar(x, y):  # Defino la función sumar
        suma = x + y
        return suma

    sumar(1, 2)

.. activecode:: py_01b
    :nocodelens:
    :include: py_01

    x = 4
    z = 5
    
    # Invoco a la función sumar con los parámetros x y z
    print(sumar(x, z))
    # Invoco a la función sumar con los parámetros 1 y 2
    print(sumar(1, 2))


Al devolver el valor, podemos utilizarlo nuevamente:

.. activecode:: py_01c
    :nocodelens:
    :include: py_01

    a = sumar(4, 5)
    b = sumar(2, 2)
    c = sumar(a, b)
    print("El resultado final es:", c)


Aunque en ningún momento indicamos que lo que tiene que sumar son
números, por lo que también puede sumar strings:

.. activecode:: py_02
    :nocodelens:
    :include: py_01

    print(sumar('hola ', 'mundo'))


Además, a esta función le podría agregar comentarios (docstrings) para
que al hacer help de la función se entienda qué es lo que hace:

.. code-block:: Python

    def sumar(x, y):
        """Suma dos elementos y retorna el resultado.
        """
        return x + y
    
    help(sumar)


.. parsed-literal::

    Suma dos elementos y retorna el resultado.

El resultado de la función no es necesario que lo guarde en una
variable, tranquilamente la puedo invocar y perder ese valor.

.. activecode:: py_04

    def factorial(n):
        """Calcula el factorial de un número de forma iterativa.
        """
        for i in range(1,n):
            n = n * i
            
        return n
    
    # calculo el factorial de 5 y lo guardo en fact_5
    fact_5 = factorial(5)
    # calculo el factorial de 10 y no lo guardo en ninguna variable
    factorial(10)

    # imprimo el factorial de 5 calculado anteriormente:
    print(fact_5)


¿Y qué sucede si no pongo el return en una función?

.. activecode:: py_05
    :nocodelens:

    def imprimir(msg):
        print(msg)

.. activecode:: py_05b
    :nocodelens:
    :include: py_05
        
    imprimir('Hola mundo')



¿Y si le asigno el resultado de este procedimiento a una variable?

.. activecode:: py_06
    :nocodelens:
    :include: py_05

    resultado = imprimir('Hola mundo')
    print(resultado)



Por lo que no existen los procedimientos, los "procedimientos" en
realidad son funciones que devuelven None. Y una prueba más de esto es
el resultado de llamar a la función type y pasarle como parámetro la
función sumar y el "procedimiento" imprimir:

.. activecode:: py_07
    :nocodelens:
    :include: py_05, py_01

    print(type(imprimir))
    print(type(sumar))
    print(sumar)



Ahora, si la función es un tipo de dato, significa que se lo puedo
asignar a una variable...

.. activecode:: py_08
    :nocodelens:
    :include: py_01

    mi_suma = sumar

¿Y qué pasa si ahora llamo a mi\_suma con los parámetros 1 y 2 como hice
antes con sumar?

.. activecode:: py_09
    :nocodelens:
    :include: py_01, py_08

    print(mi_suma(1, 2))
    print(id(mi_suma))
    print(id(sumar))



Retornar múltiples valores
--------------------------

¿Y cómo podemos hacer si queremos devolver dos variables en lugar de
una?. Una opción simple sería retornar una lista o una tupla con todos
las variables, de esa forma nos podría quedar:

.. activecode:: py_10
    :nocodelens:

    def suma_y_resta(x, y):
        """Función que suma y resta dos números."""
        resultado = []
        resultado.append(x+y)
        resultado.append(x-y)
        
        return resultado

Despues cuando querramos usarla sólo tendríamos que hacer:

.. activecode:: py_11
    :nocodelens:
    :include: py_10

    resultado = suma_y_resta(23, 5)
    suma = resultado[0]
    resta = resultado[1]

Pero así como podemos construir la lista y agregarle los valores,
tranquilamente podríamos consutruirla directamente con los valores que
queremos que tenga:

.. activecode:: py_12
    :nocodelens:

    def suma_y_resta(x, y):
        """Función que suma y resta dos números."""
        resultado = [x+y, x-y]
        
        return resultado

Y si decíamos que la única diferencia entre una lista y una tupla era
que la primera se podía modificar y la segunda no, entonces,
tranquilamente podríamos reemplazar la lista por una tupla y hasta
obviar la variable resultado y directamente:

.. activecode:: py_13
    :nocodelens:

    def suma_y_resta(x, y):
        """Función que suma y resta dos números."""
        return (x+y, x-y)

Incluso, los paréntesis son opcionales para crear una tupla:

.. activecode:: py_14
    :nocodelens:

    tupla = 1,
    print(tupla)
    print(type(tupla))


Entonces, nos podría quedar:

.. activecode:: py_15
    :nocodelens:

    def suma_y_resta(x, y):
        """Función que suma y resta dos números."""
        return x+y, x-y

Y si vamos un poco más allá, el
`*unpacking* <https://docs.python.org/2/tutorial/controlflow.html#unpacking-argument-lists>`__
de una lista o tupla se puede hacer en una sóla instrucción

.. activecode:: py_16
    :nocodelens:

    x, y, z = [1, [2, 3, 4, 5], 3]
    print(x)
    print(y)
    print(z)


Por lo que también podemos cambiar la forma en que se *desempacan* esos
valores que retorna la función y nos podría quedar:

.. activecode:: py_17
    :nocodelens:

    def suma_y_resta(x, y):
        """Función que suma y resta dos números."""
        return x+y, x-y
    
    suma, resta = suma_y_resta(23, 5)
    
    print('La suma es: ', suma)
    print('La resta es: ', resta)


