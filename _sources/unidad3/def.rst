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



