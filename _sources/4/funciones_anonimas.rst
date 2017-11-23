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
    


.. activecode:: py_07
    :nocodelens:

    mi_funcion = lambda x, y: x+y
    
    resultado = mi_funcion(1,2)
    print(resultado)




Si bien no son funciones que se usen todos los días, se suelen usar
cuando una función recibe otra función como parámetro (las funciones son
un tipo de dato, por lo que se las pueden asignar a variables, y por lo
tanto, también pueden ser parámetros). Por ejemplo, para ordenar los
alumnos por padrón podríamos usar:

.. activecode:: py_08
    :nocodelens:
    :include: py_03

    sorted(curso, key=lambda x: x['padron'])

Ahora, si quiero ordenar la lista anterior por nota decreciente y, en
caso de igualdad, por padrón podríamos usar:

.. activecode:: py_09
    :nocodelens:
    :include: py_03

    curso = crear_alumnos(15)
    print('Curso original')
    imprimir_curso(curso)
    
    lista_ordenada = sorted(curso, key=lambda x: (-x['nota'], x['padron']))
    print('Curso ordenado')
    imprimir_curso(lista_ordenada)




Otro ejemplo podría ser implementar una búsqueda binaria que permita
buscar tanto en listas crecientes como decrecientes:

.. activecode:: py_10
    :nocodelens:

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
        centro = (min + max) // 2
        while (lista[centro] != clave) and (min < max):
            if cmp(lista[centro], clave):
                max = centro - 1
            else:
                min = centro + 1
            centro = (min + max) // 2
        if lista[centro] == clave:
            return centro
        else:
            return -1
    
    print(binaria(es_mayor, [1, 2, 3, 4, 5, 6, 7, 8, 9], 8))
    print(binaria(es_menor, [1, 2, 3, 4, 5, 6, 7, 8, 9], 8))
    print(binaria(es_mayor, [1, 2, 3, 4, 5, 6, 7, 8, 9], 123))
    
    print(binaria(es_menor, [9, 8, 7, 6, 5, 4, 3, 2, 1], 6))





