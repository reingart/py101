for
---

Si queremos imprimir los números del 0 al 14 podemos crear una lista con
range y usar el for para imprimir cada valor:

.. activecode:: py_18
    :nocodelens:

    for i in range(15):
        print(i)



Incluso, si queremos imprimir los valores de una lista que nosotros
armamos, también podemos hacerlo:

.. activecode:: py_19
    :nocodelens:

    for i in [1, 6, 3, 9, 5, 2]:
        print(i)



Y si queremos imprimir cada elemento de la lista junto con su posición
podemos usar la función enumerate:

.. activecode:: py_20
    :nocodelens:

    lista = range(15, 30, 3)
    print(lista)
    for idx, value in enumerate(lista):
        print('%s: %s' % (idx, value))



También se puede usar la función zip para ir tomando los primeros
elementos de una lista, después los segundos, y así sucesivamente

.. activecode:: py_21
    :nocodelens:

    for par in zip([1, 2, 3], [4, 5, 6]):
        print(par)


Y en realidad, se puede iterar sobre cualquier elemento *iterable*, como
por ejemplo los strings:

.. activecode:: py_22
    :nocodelens:

    for caracter in "Hola mundo":
        print(caracter)


También se pueden iterar listas que tengan distintos tipos de elementos,
pero hay que tener en cuenta qué se quiere hacer con ellos:

.. activecode:: py_23
    :nocodelens:

    lista = [1, 2, "12", "34", [5, 6]]
    print('La lista tiene los elementos:', lista)
    for elemento in lista:
        print('{0}*2: {1}:'.format(elemento, elemento*2))



