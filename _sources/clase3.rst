
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
uso de funciones ayudan mucho en que un código sea legible.

def
---

La definición de una función comienza usando la palabra reservada **def**, y
continúa dejando un espacio, poniendo el nombre de la función, los parámetros
entre paréntesis (los paréntesis son obligatorios por más que no se pasen
parámetros) y un dos puntos para terminar la línea. En las líneas que le siguen
va el código de la función, que, al igual que para las estructuras de control,
la forma en que se indica el bloque de código que se tiene que ejecutar es
haciendo uso de la indentación.

El nombre de la función tiene que cumplir las mismas reglas para las variables,
puede empezar con cualquier letra y el \_ y después le puede seguir cualquier
carácter alfanumérico más el \_.

Por ejemplo:

.. activecode:: py_00

    # Defino la función sumar
    def sumar(x, y):
        suma = x + y
        print(suma)

    sumar(1, 2)

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



Pasaje de parámetros
--------------------

A diferencia de otros lenguajes, en Python todos los parámetros que se
le pasan a una función son **siempre por referencia**, es decir,
cualquier modificación que sufran dentro de la función, también se verá
reflejada fuera de la misma. Sin embargo, cuando le pasamos un parámetro
inmutable, como puede ser un *int*, *bool* o una *tupla*, si el
parámetro formal se modifica, el parámetro actual no verá esa moficación
ya que en realidad se modificó otra posición de memoria:

.. activecode:: py_18
    :nocodelens:

    def multiplicar_y_agregar(num, lista):
        num *= 2
        lista.append(num)
        print('Dentro de la función num vale {num} y ' 
              'lista vale {lista}'.format(num=num, lista=lista))
        
    lista = []
    n = 2
    print('1. Al comenzar num vale {num} y lista '
          'vale {lista}'.format(num=n, lista=lista))
    multiplicar_y_agregar(n, lista)
    print('2. Fuera de la función num vale {num} y ' \
          'lista vale {lista}'.format(num=n, lista=lista))
    print()
    n *= 3
    print('Ahora multiplico por 3: n *= 3 --> n = {}'.format(n))
    multiplicar_y_agregar(n, lista)
    print('3. Fuera de la función num vale {num} y lista ' 
          'vale {lista}'.format(num=n, lista=lista))



Lista de parámetros
-------------------

¿Qué pasa cuando no sabemos `cuántos
parámetros <https://docs.python.org/2/tutorial/controlflow.html#arbitrary-argument-lists>`__
nos pueden pasar, pero si sabemos qué hacer con ellos?

.. activecode:: py_19
    :nocodelens:

    def sumar(*lista_de_numeros):
        suma = 0
        for e in lista_de_numeros:
            suma += e
            
        return suma
    
    print(sumar(1, 2))
    print(sumar(1, 2, 3, 4, 5))
    print(sumar(*[1, 2, 3, 4, 5, 6]))
    print(sumar)



Parámetros por defecto
----------------------

Algo más común que no saber la cantidad de parámetros que nos van a
pasar es asumir que ciertos parámetros pueden no pasarlos y para ellos
asumiremos un `valor por
defecto <https://docs.python.org/2/tutorial/controlflow.html#default-argument-values>`__.
Por ejemplo:

.. activecode:: py_20
    :nocodelens:

    def imprimir_parametros(param1, param2, param3=5, 
                            param4="es el cuarto parametro", 
                            param5=False):
        print(param1, param2, param3, param4, param5)


Para esta función nos pueden pasar 2, 3, 4 o 5 parámetros. Si nos pasan
los 5 parámetros, se imprimirán los valores que nos pasen:

.. activecode:: py_21
    :nocodelens:
    :include: py_20

    imprimir_parametros(1, 2, 3, 4, 5)


Ahora, si nos pasan 4 parámetros, el intérprete asumirá que el faltante
es param5, por lo que dicho parámetro tomará el valor False. Y lo mismo
pasa con el resto de los parámetros.

.. activecode:: py_22
    :nocodelens:
    :include: py_20

    imprimir_parametros(1, 2, 3, 4)
    imprimir_parametros(1, 2, 3)
    imprimir_parametros(1, 2)


¿Y si le pasamos un sólo parámetro?.

.. activecode:: py_23
    :nocodelens:
    :include: py_20

    imprimir_parametros(1)



¿Y qué pasa si quiero pasarle los parámetros 1, 2 y el 5?. No es
problema, para eso tenemos que usar parámetros nombrados:

.. activecode:: py_24
    :nocodelens:
    :include: py_20

    imprimir_parametros(1, 2, param5="Este el parametro5")
    imprimir_parametros(1, 2)



Lo mismo pasa si lo que quiero cambiar es el cuatro parámetro:

.. activecode:: py_25
    :nocodelens:
    :include: py_20

    imprimir_parametros(1, 2, param4=4)


Hasta se pueden nombrar todos los parámetros:

.. activecode:: py_26
    :nocodelens:
    :include: py_20

    imprimir_parametros(param5=1, param3=2, param1=3, param2=4, param4=5)



Si bien puede parecer innecesario el uso de `parámetros
nombrados <https://docs.python.org/2/tutorial/controlflow.html#keyword-arguments>`__,
en algunas oportunidades se suele usar para agregar claridad y
legibilidad al código, y en otros para pasarle un diccionario:

.. activecode:: py_27
    :nocodelens:
    :include: py_20

    parametros = {
        'param1': 1,
        'param2': 2,
        'param3': 3,
        'param4': 4,
        'param5': 5,
    }
    
    imprimir_parametros(**parametros)



Uso de módulos externos
=======================

Así como en Pascal usando la cláusula ``Uses`` podíamos usar código que
no pertenecía al archivo que estábamos codificando, en Python podemos
hacer lo mismo usando la cláusula
`*import* <https://docs.python.org/3/tutorial/modules.html>`__ y
poniendo a continuación el nombre del módulo. Por ejemplo, si queremos
importar el módulo datetime para trabajar con fechas y horas, tendríamos
que hacer:

.. code-block:: Python

    import datetime

Para usarlo simplemente tenemos que poner el nombre del módulo, un punto
y la función que queramos usar. En este caso, dentro del módulo
``datetime`` vamos a usar la función que se encuentra en ``date`` y se
llama ``today()``.

.. activecode:: py_29
    :nocodelens:

    import datetime
    
    print(datetime.date.today())


Pero a diferencia de Pascal y C, acá podemos elegir importar una función
o algo en particular de ese módulo, en lugar de traerlo todo. Para eso
tendríamos que poner en primer lugar la cláusula ``from``, luego el
nombre del módulo y a continuación la cláusula ``import`` todo lo que
queremos importar separada por comas. Por ejemplo, del módulo
``datetime`` podríamos traer los submódulos ``date`` y ``time``.
Después, para usarlos simplemente lo hacemos llamando lo que importamos
sin el nombre del módulo.

.. activecode:: py_30
    :nocodelens:

    from datetime import date, time
    
    print(date.today())
    print(time(1, 23, 32))



Si tenemos un archivo llamado *ejemplo.py* que tiene el siguiente
código:

.. code-block:: Python

    def imprimir(param):
        print(param)

    def sumar(n1, n2):
        return n1+n2

y queremos importarlo a otro archivo y usarlo, podemos hacer:

.. code-block:: Python

    import ejemplo

    ejemplo.imprimir("123")
    print(ejemplo.sumar(2,3))

Y, como dijimos, también podemos importar solo una función de ese módulo
y usarla como si estuviera definida dentro de nuestro contexto.

.. code-block:: Python

    from ejemplo import sumar

    print(sumar(4, 5))

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
