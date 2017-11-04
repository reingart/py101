Reales (float)
--------------

.. activecode:: py_05
    :nocodelens:

    numero_real = 7.5
    print(numero_real)
    print(type(numero_real))


¿Y qué pasa si a un entero le sumamos un real?

.. activecode:: py_06
    :nocodelens:

    numero_entero = 5
    numero_real = 7.5
    print(numero_entero + numero_real)
    print(type(numero_entero + numero_real))


Operaciones entre reales y enteros
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

¿Y si dividimos dos números enteros?, ¿dará un número real?

.. activecode:: py_07
    :nocodelens:

    dividendo = 5
    divisor = 3
    resultado = dividendo / divisor
    print(resultado)
    print(type(resultado))

CUIDADO: En Python 3 sí devuelve un número real (con decimales), 
pero en Python 2 devuelve un número entero! 

En cambio, si alguno de los números es real:

.. activecode:: py_08
    :nocodelens:

    dividendo = 5
    divisor = 3.0
    resultado = dividendo / divisor
    print(resultado)
    print(type(resultado))


Tanto en Python 2 como en Python 3 devuelve un número real (con decimales).
 
¿Y si queremos hacer la división entera por más que uno de los números
sea real?

.. activecode:: py_09
    :nocodelens:

    dividendo = 5
    divisor = 3.0
    cociente = dividendo // divisor
    print("cociente: ", cociente)
    print(type(cociente))
    
    resto = dividendo % divisor
    print("resto: ", resto)
    print(type(resto))


Esto cambia en Python 3, donde la / hace la división real (por más que
le pases dos números enteros) y la // hace la división entera.


