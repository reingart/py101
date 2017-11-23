
.. raw:: html

   <!--
   27/10
   Ordenamientos y búsquedas.
   Excepciones. Funciones anónimas.(Pablo o Andres)
   -->

Ordenamiento de listas
======================

Las listas se pueden ordenar fácilmente usando la función
`*sorted* <https://docs.python.org/2/library/functions.html?highlight=raw_input#sorted>`__:

.. code:: python

    lista_de_numeros = [1, 6, 3, 9, 5, 2]
    lista_ordenada = sorted(lista_de_numeros)
    print lista_ordenada


.. parsed-literal::

    [1, 2, 3, 5, 6, 9]


Pero, ¿y cómo hacemos para ordenarla de mayor a menor?. Simple,
interrogamos un poco a la función:

.. code:: python

    >>> print sorted.__doc__
    sorted(iterable, cmp=None, key=None, reverse=False) --> new sorted list

Entonces, con sólo pasarle el parámetro de *reverse* en ``True`` debería
alcanzar:

.. code:: python

    lista_de_numeros = [1, 6, 3, 9, 5, 2]
    print sorted(lista_de_numeros, reverse=True)


.. parsed-literal::

    [9, 6, 5, 3, 2, 1]


¿Y si lo que quiero ordenar es una lista de registros?. Podemos pasarle
una función que sepa cómo comparar esos registros o una que sepa
devolver la información que necesita comparar.

.. code:: python

    import random
    
    def crear_alumnos(cantidad_de_alumnos=5):
        nombres = ['Javier', 'Pablo', 'Ramiro', 'Lucas', 'Carlos']
        apellidos = ['Saviola', 'Aimar', 'Funes Mori', 'Alario', 
                     'Sanchez']
    
        alumnos = []
        for i in range(cantidad_de_alumnos):
            a = {
                'nombre': '{}, {}'.format(
                    random.choice(apellidos), random.choice(nombres)),
                'padron': random.randint(90000, 100000),
                'nota': random.randint(4, 10)
            }
            alumnos.append(a)
        
        return alumnos
    
    
    def imprimir_curso(lista):
        for idx, x in enumerate(lista, 1):
            print '    {pos:2}. {padron} - {nombre}: {nota}'.format(
                pos=idx, **x)
    
    
    def obtener_padron(alumno):
        return alumno['padron']
    
    
    def ordenar_por_padron(alumno1, alumno2):
        if alumno1['padron'] < alumno2['padron']:
            return -1
        elif alumno2['padron'] < alumno1['padron']:
            return 1
        else:
            return 0
    
    curso = crear_alumnos()
    print 'La lista tiene los alumnos:'
    imprimir_curso(curso)
    
    lista_ordenada = sorted(curso, key=obtener_padron)
    print 'Y la lista ordenada por padrón:'
    imprimir_curso(lista_ordenada)
    
    otra_lista_ordenada = sorted(curso, cmp=ordenar_por_padron)
    print 'Y la lista ordenada por padrón:'
    imprimir_curso(otra_lista_ordenada)


.. parsed-literal::

    La lista tiene los alumnos:
         1. 96617 - Funes Mori, Lucas: 5
         2. 94069 - Saviola, Lucas: 10
         3. 99533 - Alario, Javier: 5
         4. 96185 - Aimar, Pablo: 5
         5. 98034 - Saviola, Carlos: 5
    Y la lista ordenada por padrón:
         1. 94069 - Saviola, Lucas: 10
         2. 96185 - Aimar, Pablo: 5
         3. 96617 - Funes Mori, Lucas: 5
         4. 98034 - Saviola, Carlos: 5
         5. 99533 - Alario, Javier: 5
    Y la lista ordenada por padrón:
         1. 94069 - Saviola, Lucas: 10
         2. 96185 - Aimar, Pablo: 5
         3. 96617 - Funes Mori, Lucas: 5
         4. 98034 - Saviola, Carlos: 5
         5. 99533 - Alario, Javier: 5


Búsquedas en listas
===================

Para saber si un elemento se encuentra en una lista, alcanza con usar el
operador **in**:

.. code:: python

    lista = [11, 4, 6, 1, 3, 5, 7]
    
    if 3 in lista:
        print '3 esta en la lista'
    else:
        print '3 no esta en la lista'
    
    if 15 in lista:
        print '15 esta en la lista'
    else:
        print '15 no esta en la lista'


.. parsed-literal::

    3 esta en la lista
    15 no esta en la lista


También es muy fácil saber si un elemento **no** esta en la lista:

.. code:: python

    lista = [11, 4, 6, 1, 3, 5, 7]
    
    if 3 not in lista:
        print '3 NO esta en la lista'
    else:
        print '3 SI esta en la lista'


.. parsed-literal::

    3 SI esta en la lista


En cambio, si lo que queremos es saber es dónde se encuentra el número 3
en la lista es:

.. code:: python

    lista = [11, 4, 6, 1, 3, 5, 7]
    
    pos = lista.index(3)
    print 'El 3 se encuentra en la posición', pos
    
    pos = lista.index(15)
    print 'El 15 se encuentra en la posición', pos


.. parsed-literal::

    El 3 se encuentra en la posición 4


::


    ---------------------------------------------------------------------------

    ValueError                                Traceback (most recent call last)

    <ipython-input-6-d0e7e1660268> in <module>()
          4 print 'El 3 se encuentra en la posición', pos
          5 
    ----> 6 pos = lista.index(15)
          7 print 'El 15 se encuentra en la posición', pos


    ValueError: 15 is not in list


Funciones anónimas
------------------

Hasta ahora, a todas las funciones que creamos les poníamos un nombre al
momento de crearlas, pero cuando tenemos que crear funciones que sólo
tienen una línea y no se usan en una gran cantidad de lugares se pueden
usar las funciones
`*lambda* <https://docs.python.org/2/tutorial/controlflow.html#lambda-expressions>`__:

.. code:: python

    help("lambda")


.. parsed-literal::

    Lambdas
    *******
    
       lambda_expr     ::= "lambda" [parameter_list]: expression
       old_lambda_expr ::= "lambda" [parameter_list]: old_expression
    
    Lambda expressions (sometimes called lambda forms) have the same
    syntactic position as expressions.  They are a shorthand to create
    anonymous functions; the expression "lambda arguments: expression"
    yields a function object.  The unnamed object behaves like a function
    object defined with
    
       def name(arguments):
           return expression
    
    See section *Function definitions* for the syntax of parameter lists.
    Note that functions created with lambda expressions cannot contain
    statements.
    
    Related help topics: FUNCTIONS
    


.. code:: python

    mi_funcion = lambda x, y: x+y
    
    resultado = mi_funcion(1,2)
    print resultado


.. parsed-literal::

    3


Si bien no son funciones que se usen todos los días, se suelen usar
cuando una función recibe otra función como parámetro (las funciones son
un tipo de dato, por lo que se las pueden asignar a variables, y por lo
tanto, también pueden ser parámetros). Por ejemplo, para ordenar los
alumnos por padrón podríamos usar:

.. code:: python

    sorted(curso, key=lambda x: x['padron'])

Ahora, si quiero ordenar la lista anterior por nota decreciente y, en
caso de igualdad, por padrón podríamos usar:

.. code:: python

    curso = crear_alumnos(15)
    print 'Curso original'
    imprimir_curso(curso)
    
    lista_ordenada = sorted(curso, key=lambda x: (-x['nota'], x['padron']))
    print 'Curso ordenado'
    imprimir_curso(lista_ordenada)


.. parsed-literal::

    Curso original
         1. 96341 - Alario, Lucas: 5
         2. 99826 - Aimar, Javier: 10
         3. 90226 - Saviola, Carlos: 6
         4. 99389 - Aimar, Ramiro: 9
         5. 97936 - Saviola, Lucas: 4
         6. 94269 - Funes Mori, Ramiro: 9
         7. 94319 - Sanchez, Carlos: 4
         8. 94865 - Funes Mori, Ramiro: 4
         9. 96940 - Funes Mori, Carlos: 5
        10. 94417 - Aimar, Lucas: 5
        11. 99753 - Alario, Ramiro: 5
        12. 98255 - Alario, Carlos: 5
        13. 94344 - Saviola, Lucas: 8
        14. 99279 - Funes Mori, Carlos: 6
        15. 99785 - Sanchez, Ramiro: 6
    Curso ordenado
         1. 99826 - Aimar, Javier: 10
         2. 94269 - Funes Mori, Ramiro: 9
         3. 99389 - Aimar, Ramiro: 9
         4. 94344 - Saviola, Lucas: 8
         5. 90226 - Saviola, Carlos: 6
         6. 99279 - Funes Mori, Carlos: 6
         7. 99785 - Sanchez, Ramiro: 6
         8. 94417 - Aimar, Lucas: 5
         9. 96341 - Alario, Lucas: 5
        10. 96940 - Funes Mori, Carlos: 5
        11. 98255 - Alario, Carlos: 5
        12. 99753 - Alario, Ramiro: 5
        13. 94319 - Sanchez, Carlos: 4
        14. 94865 - Funes Mori, Ramiro: 4
        15. 97936 - Saviola, Lucas: 4


Otro ejemplo podría ser implementar una búsqueda binaria que permita
buscar tanto en listas crecientes como decrecientes:

.. code:: python

    es_mayor = lambda n1, n2: n1 > n2
    es_menor = lambda n1, n2: n1 < n2
    
    
    def binaria(cmp, lista, clave):
        """Binaria es una función que busca en una lista la clave pasada.
        Es un requisito de la búsqueda binaria que la lista se encuentre 
        ordenada, pero no si el orden es ascendente o descendente. Por 
        este motivo es que también recibe una función que le indique en
        que sentido ir.
        Si la lista está ordenada en forma ascendente la función que se 
        le pasa tiene que ser verdadera cuando el primer valor es mayor 
        que la segundo; y falso en caso contrario.
        Si la lista está ordenada en forma descendente la función que se 
        le pasa tiene que ser verdadera cuando el primer valor es menor 
        que la segundo; y falso en caso contrario.
        """
        min = 0
        max = len(lista) - 1
        centro = (min + max) / 2
        while (lista[centro] != clave) and (min < max):
            if cmp(lista[centro], clave):
                max = centro - 1
            else:
                min = centro + 1
            centro = (min + max) / 2
        if lista[centro] == clave:
            return centro
        else:
            return -1
    
    print binaria(es_mayor, [1, 2, 3, 4, 5, 6, 7, 8, 9], 8)
    print binaria(es_menor, [1, 2, 3, 4, 5, 6, 7, 8, 9], 8)
    print binaria(es_mayor, [1, 2, 3, 4, 5, 6, 7, 8, 9], 123)
    
    print binaria(es_menor, [9, 8, 7, 6, 5, 4, 3, 2, 1], 6)



.. parsed-literal::

    7
    -1
    -1
    3



