
.. raw:: html

   <!--
   22/10
   Entrada y salida de datos
   Funciones (parámetros por default, nombrados), módulos (distintas formas de importarlos)
   CLASE DE LABORATORIO 
   Vencimiento TP1
   Enunciado del TP 2
   Eze
   -->

Funciones
=========

Una de las premisas de Python era que *"La legibilidad cuenta"*, y el
uso de funciones ayudan mucho en que un código sea legible. En Python no
existen los procedimientos: son todas funciones. Incluso, aunque
nosotros no devolvamos ningún valor, Python lo hará por nosotros,
retornando ``None``. La forma de devolver valores es, al igual que en C,
usando la palabra reservada **return** y el valor a retornar. Y de igual
forma, una vez que se ejecuta esa sentencia, no se ejecuta ninguna
sentencia más de esa función; sin importar si está dentro de un ciclo o
todavía no hayamos hecho nada. La definición de una función comienza
usando la palabra reservada **def**, y continúa dejando un espacio,
poniendo el nombre de la función, los parámetros entre paréntesis(los
paréntesis son obligatorios por más que no se pasen parámetros) y un dos
puntos para terminar la línea. En las líneas que le siguen va el código
de la función, que, al igual que para las estructuras de control, la
forma en que se indica el bloque de código que se tiene que ejecutar es
haciendo uso de la indentación. El nombre de la función tiene que
cumplir las mismas reglas para las variables, puede empezar con
cualquier letra y el \_ y después le puede seguir cualquier carácter
alfanumérico más el \_. Por ejemplo:

.. code:: python

    def sumar(x, y):  # Defino la función sumar
        suma = x + y
        return suma
    
    x = 4
    z = 5
    
    print sumar(x, z)  # Invoco a la función sumar con los
                       # parámetros x y z
    print sumar(1, 2)  # Invoco a la función sumar con los
                       # parámetros 1 y 2


.. parsed-literal::

    9
    3


Aunque en ningún momento indicamos que lo que tiene que sumar son
números, por lo que también puede sumar strings:

.. code:: python

    print sumar('hola ', 'mundo')


.. parsed-literal::

    hola mundo


Además, a esta función le podría agregar comentarios (docstrings) para
que al hacer help de la función se entienda qué es lo que hace:

.. code:: python

    def sumar(x, y):
        """Suma dos elementos y retorna el resultado.
        """
        return x + y
    
    help(sumar)


.. parsed-literal::

    Help on function sumar in module __main__:
    
    sumar(x, y)
        Suma dos elementos y retorna el resultado.
    


El resultado de la función no es necesario que lo guarde en una
variable, tranquilamente la puedo invocar y perder ese valor.

.. code:: python

    def factorial(n):
        """Calcula el factorial de un número de forma iterativa.
        """
        for i in range(1,n):
            n *= i
            
        return n
    
    fact_5 = factorial(5)  # calculo el factorial de 5 y lo guardo 
                           # en fact_5
    factorial(10)  # calculo el factorial de 10 y no lo guardo en 
                   # ninguna variable





.. parsed-literal::

    3628800



¿Y qué sucede si no pongo el return en una función?

.. code:: python

    def imprimir(msg):
        print msg
        
    imprimir('Hola mundo')


.. parsed-literal::

    Hola mundo


¿Y si le asigno el resultado de este procedimiento a una variable?

.. code:: python

    resultado = imprimir('Hola mundo')
    print resultado


.. parsed-literal::

    Hola mundo
    None


Por lo que no existen los procedimientos, los "procedimientos" en
realidad son funciones que devuelven None. Y una prueba más de esto es
el resultado de llamar a la función type y pasarle como parámetro la
función sumar y el "procedimiento" imprimir:

.. code:: python

    print type(imprimir)
    print type(sumar)
    print sumar


.. parsed-literal::

    <type 'function'>
    <type 'function'>
    <function sumar at 0x7fbb0a09f8c0>


Ahora, si la función es un tipo de dato, significa que se lo puedo
asignar a una variable...

.. code:: python

    mi_suma = sumar

¿Y qué pasa si ahora llamo a mi\_suma con los parámetros 1 y 2 como hice
antes con sumar?

.. code:: python

    print mi_suma(1, 2)
    print id(mi_suma)
    print id(sumar)


.. parsed-literal::

    3
    140441304037568
    140441304037568


Retornar múltiples valores
--------------------------

¿Y cómo podemos hacer si queremos devolver dos variables en lugar de
una?. Una opción simple sería retornar una lista o una tupla con todos
las variables, de esa forma nos podría quedar:

.. code:: python

    def suma_y_resta(x, y):
        """Función que suma y resta dos números."""
        resultado = []
        resultado.append(x+y)
        resultado.append(x-y)
        
        return resultado

Despues cuando querramos usarla sólo tendríamos que hacer:

.. code:: python

    resultado = suma_y_resta(23, 5)
    suma = resultado[0]
    resta = resultado[1]

Pero así como podemos construir la lista y agregarle los valores,
tranquilamente podríamos consutruirla directamente con los valores que
queremos que tenga:

.. code:: python

    def suma_y_resta(x, y):
        """Función que suma y resta dos números."""
        resultado = [x+y, x-y]
        
        return resultado

Y si decíamos que la única diferencia entre una lista y una tupla era
que la primera se podía modificar y la segunda no, entonces,
tranquilamente podríamos reemplazar la lista por una tupla y hasta
obviar la variable resultado y directamente:

.. code:: python

    def suma_y_resta(x, y):
        """Función que suma y resta dos números."""
        return (x+y, x-y)

Incluso, los paréntesis son opcionales para crear una tupla:

.. code:: python

    tupla = 1,
    print tupla
    print type(tupla)


.. parsed-literal::

    (1,)
    <type 'tuple'>


Entonces, nos podría quedar:

.. code:: python

    def suma_y_resta(x, y):
        """Función que suma y resta dos números."""
        return x+y, x-y

Y si vamos un poco más allá, el
`*unpacking* <https://docs.python.org/2/tutorial/controlflow.html#unpacking-argument-lists>`__
de una lista o tupla se puede hacer en una sóla instrucción

.. code:: python

    x, y, z = [1, [2, 3, 4, 5], 3]
    print x
    print y
    print z


.. parsed-literal::

    1
    [2, 3, 4, 5]
    3


Por lo que también podemos cambiar la forma en que se *desempacan* esos
valores que retorna la función y nos podría quedar:

.. code:: python

    def suma_y_resta(x, y):
        """Función que suma y resta dos números."""
        return x+y, x-y
    
    suma, resta = suma_y_resta(23, 5)
    
    print 'La suma es: ', suma
    print 'La resta es: ', resta


.. parsed-literal::

    La suma es:  28
    La resta es:  18


Pasaje de parámetros
--------------------

A diferencia de otros lenguajes, en Python todos los parámetros que se
le pasan a una función son **siempre por referencia**, es decir,
cualquier modificación que sufran dentro de la función, también se verá
reflejada fuera de la misma. Sin embargo, cuando le pasamos un parámetro
inmutable, como puede ser un *int*, *bool* o una *tupla*, si el
parámetro formal se modifica, el parámetro actual no verá esa moficación
ya que en realidad se modificó otra posición de memoria:

.. code:: python

    def multiplicar_y_agregar(num, lista):
        num *= 2
        lista.append(num)
        print 'Dentro de la función num vale {num} y ' \
              'lista vale {lista}'.format(num=num, lista=lista)
        
    lista = []
    n = 2
    print '1. Al comenzar num vale {num} y lista ' \
          'vale {lista}'.format(num=n, lista=lista)
    multiplicar_y_agregar(n, lista)
    print '2. Fuera de la función num vale {num} y ' \
          'lista vale {lista}'.format(num=n, lista=lista)
    print 
    n *= 3
    print 'Ahora multiplico por 3: n *= 3 --> n = {}'.format(n)
    multiplicar_y_agregar(n, lista)
    print '3. Fuera de la función num vale {num} y lista ' \
          'vale {lista}'.format(num=n, lista=lista)



.. parsed-literal::

    1. Al comenzar num vale 2 y lista vale []
    Dentro de la función num vale 4 y lista vale [4]
    2. Fuera de la función num vale 2 y lista vale [4]
    
    Ahora multiplico por 3: n *= 3 --> n = 6
    Dentro de la función num vale 12 y lista vale [4, 12]
    3. Fuera de la función num vale 6 y lista vale [4, 12]


Lista de parámetros
-------------------

¿Qué pasa cuando no sabemos `cuántos
parámetros <https://docs.python.org/2/tutorial/controlflow.html#arbitrary-argument-lists>`__
nos pueden pasar, pero si sabemos qué hacer con ellos?

.. code:: python

    def sumar(*lista_de_numeros):
        suma = 0
        for e in lista_de_numeros:
            suma += e
            
        return suma
    
    print sumar(1, 2)
    print sumar(1, 2, 3, 4, 5)
    print sumar(*[1, 2, 3, 4, 5, 6])
    print sumar


.. parsed-literal::

    3
    15
    21
    <function sumar at 0x7fbb0a09f7d0>


Parámetros por defecto
----------------------

Algo más común que no saber la cantidad de parámetros que nos van a
pasar es asumir que ciertos parámetros pueden no pasarlos y para ellos
asumiremos un `valor por
defecto <https://docs.python.org/2/tutorial/controlflow.html#default-argument-values>`__.
Por ejemplo:

.. code:: python

    def imprimir_parametros(param1, param2, param3=5, 
                            param4="es el cuarto parametro", 
                            param5=False):
        print param1, param2, param3, param4, param5


Para esta función nos pueden pasar 2, 3, 4 o 5 parámetros. Si nos pasan
los 5 parámetros, se imprimirán los valores que nos pasen:

.. code:: python

    imprimir_parametros(1, 2, 3, 4, 5)


.. parsed-literal::

    1 2 3 4 5


Ahora, si nos pasan 4 parámetros, el intérprete asumirá que el faltante
es param5, por lo que dicho parámetro tomará el valor False. Y lo mismo
pasa con el resto de los parámetros.

.. code:: python

    imprimir_parametros(1, 2, 3, 4)
    imprimir_parametros(1, 2, 3)
    imprimir_parametros(1, 2)


.. parsed-literal::

    1 2 3 4 False
    1 2 3 es el cuarto parametro False
    1 2 5 es el cuarto parametro False


¿Y si le pasamos un sólo parámetro?.

.. code:: python

    imprimir_parametros(1)


::


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-18-8b3152a74f3f> in <module>()
    ----> 1 imprimir_parametros(1)
    

    TypeError: imprimir_parametros() takes at least 2 arguments (1 given)


¿Y qué pasa si quiero pasarle los parámetros 1, 2 y el 5?. No es
problema, para eso tenemos que usar parámetros nombrados:

.. code:: python

    imprimir_parametros(1, 2, param5="Este el parametro5")
    imprimir_parametros(1, 2)


.. parsed-literal::

    1 2 5 es el cuarto parametro Este el parametro5
    1 2 5 es el cuarto parametro False


Lo mismo pasa si lo que quiero cambiar es el cuatro parámetro:

.. code:: python

    imprimir_parametros(1, 2, param4=4)


.. parsed-literal::

    1 2 5 4 False


Hasta se pueden nombrar todos los parámetros:

.. code:: python

    imprimir_parametros(param5=1, param3=2, param1=3, param2=4, param4=5)


.. parsed-literal::

    3 4 2 5 1


Si bien puede parecer innecesario el uso de `parámetros
nombrados <https://docs.python.org/2/tutorial/controlflow.html#keyword-arguments>`__,
en algunas oportunidades se suele usar para agregar claridad y
legibilidad al código, y en otros para pasarle un diccionario:

.. code:: python

    parametros = {
        'param1': 1,
        'param2': 2,
        'param3': 3,
        'param4': 4,
        'param5': 5,
    }
    
    imprimir_parametros(**parametros)


.. parsed-literal::

    1 2 3 4 5


Uso de módulos externos
=======================

Así como en Pascal usando la cláusula ``Uses`` podíamos usar código que
no pertenecía al archivo que estábamos codificando, en Python podemos
hacer lo mismo usando la cláusula
`*import* <https://docs.python.org/2/tutorial/modules.html>`__ y
poniendo a continuación el nombre del módulo. Por ejemplo, si queremos
importar el módulo datetime para trabajar con fechas y horas, tendríamos
que hacer:

.. code:: python

    import datetime

Para usarlo simplemente tenemos que poner el nombre del módulo, un punto
y la función que queramos usar. En este caso, dentro del módulo
``datetime`` vamos a usar la función que se encuentra en ``date`` y se
llama ``today()``.

.. code:: python

    import datetime
    
    print datetime.date.today()


.. parsed-literal::

    2017-05-25


Pero a diferencia de Pascal y C, acá podemos elegir importar una función
o algo en particular de ese módulo, en lugar de traerlo todo. Para eso
tendríamos que poner en primer lugar la cláusula ``from``, luego el
nombre del módulo y a continuación la cláusula ``import`` todo lo que
queremos importar separada por comas. Por ejemplo, del módulo
``datetime`` podríamos traer los submódulos ``date`` y ``time``.
Después, para usarlos simplemente lo hacemos llamando lo que importamos
sin el nombre del módulo.

.. code:: python

    from datetime import date, time
    
    print date.today()
    print time(1, 23, 32)



.. parsed-literal::

    2017-05-25
    01:23:32


Si tenemos un archivo llamado *ejemplo.py* que tiene el siguiente
código:

.. code:: python

    def imprimir(param):
        print param

    def sumar(n1, n2):
        return n1+n2

y queremos importarlo a otro archivo y usarlo, podemos hacer:

.. code:: python

    import ejemplo

    ejemplo.imprimir("123")
    print ejemplo.sumar(2,3)

Y, como dijimos, también podemos importar solo una función de ese módulo
y usarla como si estuviera definida dentro de nuestro contexto.

.. code:: python

    from ejemplo import sumar

    print sumar(4, 5)

Ejercicios
==========

1. Escribir un programa que le pregunte un número al usuario. Si el
   número es 5, que muestre "Suerte!"; si el número es mayor a 10, que
   muestre "Grande!"; para los otros casos que muestre "Sin suerte, :(".
2. Crear una función que calcule el factorial de un número, pedirle al
   usuario que ingrese un número y mostrarle el factorial de dicho
   número.
3. Crear una función que indique si un número es primo o no e imprimir
   todos los números primos entre 1 y un número que se le solicite al
   usuario.
4. Dada una lista de números enteros y un entero k, escribir una función
   que muestre todo el vector multiplicado por k.
5. Hacer un programa que genere un número entero al azar (módulo random)
   entre 0 y 1000, y le vaya pidiendo al usuario que ingrese números
   enteros para adivinarlo. Si el usuario ingresa un número menor que el
   objetivo, muestra "Es más alto!"; si el usuario ingresa uno mayor,
   muestra "Es más bajo!"; si el usuario acierta, muestra "Ganaste!!!",
   y termina. Si el usuario no acertó en 7 intentos, que muestre
   "Perdiste! :(" y termine.
6. Armar una función que reciba una tupla y devuelva si la tupla está
   ordenada (de menor a mayor) o no.
