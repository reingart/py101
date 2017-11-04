while
-----

El ciclo while también ejecuta un bloque de código mientras la condición
sea verdadera:

.. activecode:: py_24
    :nocodelens:

    numero = 5
    while numero < 10:
        print(numero)
        numero += 1


Las listas tienen una función llamada pop que lo que hace es tomar el
último elemento de ella y lo elimina:

.. activecode:: py_25
    :nocodelens:

    lista = list(range(5))
    print('La lista antes de entrar al while tiene:', lista)
    while lista:  # Si la lista no esta vacía, sigo sacando elementos
        print(lista.pop())
    
    print('La lista después de salir del while tiene:', lista)


Aunque también podría obtener el primero:

.. activecode:: py_26
    :nocodelens:

    lista = list(range(5))
    print('La lista antes de entrar al while tiene:', lista)
    while lista:  # Si la lista no esta vacía, sigo sacando elementos
        print(lista.pop(0))
    
    print('La lista después de salir del while tiene:', lista)
    

