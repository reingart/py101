Complejos
---------

Python, a diferencia de la mayoría de los lenguajes, también soporta los
números complejos. Tal vez éste es uno de los motivos por los que Python
se usa tanto en el campo científico.

.. activecode:: py_10
    :nocodelens:

    complejo = 5 + 3j
    print(complejo)
    print(type(complejo))
    complejo_cuadrado = complejo ** 2
    print('(5+3j)*(5+3j) = 5*5 + 5*3j + 3j*5 + 3j*3j = (25-9) + 30j')
    print(complejo_cuadrado)


Si bien Python soporta aritmética de complejos, la verdad es que no es
uno de los tipos de datos más usados. Sin embargo, es bueno saber que
existe.

