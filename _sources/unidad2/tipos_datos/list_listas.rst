Listas (list)
-------------

En Python podemos guardar varios elementos usando
`listas <https://docs.python.org/3/tutorial/introduction.html#lists>`__

.. activecode:: py_01
    :nocodelens:

    lista_de_numeros = [1, 6, 3, 9, 5, 2]
    print(lista_de_numeros)
    print(type(lista_de_numeros))


Si se quiere saber si un número se encuentra en una lista o no, es muy
simple, sólo hay que usar el operador **in**:

.. activecode:: py_02
    :nocodelens:
    :include: py_01

    print('El %s esta en %s?: %s' % (5, lista_de_numeros, 5 in lista_de_numeros))
    print('El %s esta en %s?: %s' % (7, lista_de_numeros, 7 in lista_de_numeros))


El operador **in** también funciona para strings (es *case sensitive*):

.. activecode:: py_03
    :nocodelens:

    print('mundo in "Hola mundo": ', 'mundo' in "Hola mundo")
    print('MUNDO in "Hola mundo": ', 'MUNDO' in "Hola mundo")


A diferencia de los strings, en las listas si podemos cambiar un
elemento cualquiera:

.. activecode:: py_04
    :nocodelens:

    lista_de_numeros = [1, 6, 3, 9, 5, 2]
    print(lista_de_numeros)
    lista_de_numeros[3] = 152
    print(lista_de_numeros)


En ningún momento dijimos que la lista era de enteros, por lo que
tranquilamente podemos guardar elementos de distintos tipos de datos

.. activecode:: py_05
    :nocodelens:

    lista_de_cosas = [2, 5.5, 'letras', [1, 2, 3], ('tupla', 'de', 'strings')]
    print(lista_de_cosas)


Para eliminar un elemento sólo tenemos que usar la función **del** e
indicar la posición.

.. activecode:: py_06
    :nocodelens:

    lista_de_cosas = [2, 5.5, 'letras', [1, 2, 3], ('tupla', 'de', 'strings')]
    print('Lista de cosas:', lista_de_cosas)
    
    del lista_de_cosas[3]
    print('Después de eliminar la posición 3:', lista_de_cosas)


.. activecode:: py_07
    :nocodelens:

    lista_de_numeros = []
    
    if lista_de_numeros:
        print('la lista tiene elementos')
    else:
        print('la lista no tiene elementos')


Y con las listas también se pueden hacer *slices*:

.. activecode:: py_08
    :nocodelens:
    :include: py_05

    print('primer elemento:', lista_de_cosas[0])
    ultimo = lista_de_cosas[-1]
    print('último:', ultimo)
    print('del_segundo_al_ultimo_sin_incluirlo:', lista_de_cosas[1:4])
    print('del_segundo_al_ultimo_sin_incluirlo:', lista_de_cosas[1:-1])
    print('del_segundo_al_ultimo_incluyendolo:', lista_de_cosas[1:])


Existe una función llamada *range* que crea permite crear listas de
números:

.. activecode:: py_09
    :nocodelens:

    print('Ejemplos:')
    print('  range(15):', range(15))
    print('  range(15)[2:9]:', range(15)[2:9])
    print('  range(15)[2:9:3]:', range(15)[2:9:3])
    print('  range(2,9):', range(2,9))
    print('  range(2,9,3):', range(2,9,3))



