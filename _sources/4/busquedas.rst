
Búsquedas en listas
===================

Para saber si un elemento se encuentra en una lista, alcanza con usar el
operador **in**:

.. activecode:: py_04
    :nocodelens:

    lista = [11, 4, 6, 1, 3, 5, 7]
    
    if 3 in lista:
        print('3 esta en la lista')
    else:
        print('3 no esta en la lista')
    
    if 15 in lista:
        print('15 esta en la lista')
    else:
        print('15 no esta en la lista')



También es muy fácil saber si un elemento **no** esta en la lista:

.. activecode:: py_05
    :nocodelens:

    lista = [11, 4, 6, 1, 3, 5, 7]
    
    if 3 not in lista:
        print('3 NO esta en la lista')
    else:
        print('3 SI esta en la lista')



En cambio, si lo que queremos es saber es dónde se encuentra el número 3
en la lista es:

.. activecode:: py_06
    :nocodelens:

    lista = [11, 4, 6, 1, 3, 5, 7]
    
    pos = lista.index(3)
    print('El 3 se encuentra en la posición', pos)
    
    pos = lista.index(15)
    print('El 15 se encuentra en la posición', pos)





