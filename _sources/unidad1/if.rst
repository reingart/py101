Así como en Pascal se delimitan los bloques de código con las palabras
reservadas *begin* y *end*, en Python se usan la indentación (espacios)
para determinar qué se encuentra dentro de una estructura de control y
qué no.

if
--

.. activecode:: py_25
    :nocodelens:

    numero1 = 1
    numero2 = 2
    
    if numero1 == numero2:
        print('Los números son iguales')
    
    print('Este string se imprime siempre')
    
    print('Ahora cambio el valor de numero2')
    numero2 = 1
    
    if numero1 == numero2:
        print('Los números son iguales')
    
    print('Este string se imprime siempre')



if-else
-------

.. activecode:: py_26
    :nocodelens:

    numero1 = 1
    numero2 = 1
    
    if numero1 == numero2:
        print('Los números son iguales')
    else:
        print('Los números son distintos')


if-elif-else
------------

Ahora si queremos imprimir si un número es igual, menor o mayor a otro
tendríamos que usar if anidados en Pascal o C; y no queda del todo
claro:

.. activecode:: py_27
    :nocodelens:

    numero1 = 1
    numero2 = 2

    # Como lo tendríamos que hacer en Pascal o C.
    if numero1 == numero2:
        print('Los dos números son iguales')
    else:
        if numero1 > numero2:
            print('numero1 es mayor a numero2')
        else:
            print('numero1 es menor a numero2')


En cambio, en Python lo podemos un poco más compacto y claro:

.. activecode:: py_28
    :nocodelens:

    numero1 = 1
    numero2 = 2

    # Más corto y elegante en Python.
    if numero1 == numero2:
        print('Los dos números son iguales')
    elif numero1 > numero2:
        print('numero1 es mayor a numero2')
    else:
        print('numero1 es menor a numero2')


Cualquier tipo de dato se lo puede evaluar como booleano. Se toma como falso a:

* None
* False para los bool
* cero para todo tipo de dato numérico: 0, 0L, 0.0, 0j
* vacío para cualquier secuencia o diccionario: '', (), [], {}

Por lo tanto, se puede saber si una lista esta vacía o no con
simplemente:

.. activecode:: py_29
    :nocodelens:

    if []:
        print('La lista no esta vacía')

.. activecode:: py_30
    :nocodelens:

    if False or None or [] or () or {} or 0 or '':
        print('Alguna de las anteriores no era falsa')
    else:
        print('Todos los valores anteriores son consideradas como Falso')
    
    
    x = 'Este mensaje se va a mostrar porque será evaulado como verdadero'
    if x:
        print(x)
    else:
        print('Esta vacio')


