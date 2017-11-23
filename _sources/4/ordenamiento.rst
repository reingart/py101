
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

.. activecode:: py_01
    :nocodelens:

    lista_de_numeros = [1, 6, 3, 9, 5, 2]
    lista_ordenada = sorted(lista_de_numeros)
    print(lista_ordenada)


Pero, ¿y cómo hacemos para ordenarla de mayor a menor?. Simple,
interrogamos un poco a la función:

.. code:: python

    >>> print(sorted.__doc__)
    sorted(iterable, cmp=None, key=None, reverse=False) --> new sorted list

Entonces, con sólo pasarle el parámetro de *reverse* en ``True`` debería
alcanzar:

.. activecode:: py_02
    :nocodelens:

    lista_de_numeros = [1, 6, 3, 9, 5, 2]
    print(sorted(lista_de_numeros, reverse=True))


¿Y si lo que quiero ordenar es una lista de registros?. Podemos pasarle
una función que sepa cómo comparar esos registros o una que sepa
devolver la información que necesita comparar.

.. activecode:: py_03
    :nocodelens:

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
            print('    {pos:2}. {padron} - {nombre}: {nota}'.format(
                pos=idx, **x))
    
    
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
    print('La lista tiene los alumnos:')
    imprimir_curso(curso)
    
    lista_ordenada = sorted(curso, key=obtener_padron)
    print('Y la lista ordenada por padrón:')
    imprimir_curso(lista_ordenada)
    
    otra_lista_ordenada = sorted(curso, cmp=ordenar_por_padron)
    print('Y la lista ordenada por padrón:')
    imprimir_curso(otra_lista_ordenada)



