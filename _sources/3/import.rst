Uso de módulos externos
=======================

Así como en Pascal usando la cláusula ``Uses`` podíamos usar código que
no pertenecía al archivo que estábamos codificando, en Python podemos
hacer lo mismo usando la cláusula
`*import* <https://docs.python.org/3/tutorial/modules.html>`__ y
poniendo a continuación el nombre del módulo. Por ejemplo, si queremos
importar el módulo datetime para trabajar con fechas y horas, tendríamos
que hacer:

.. code-block:: Python

    import datetime

Para usarlo simplemente tenemos que poner el nombre del módulo, un punto
y la función que queramos usar. En este caso, dentro del módulo
``datetime`` vamos a usar la función que se encuentra en ``date`` y se
llama ``today()``.

.. activecode:: py_29
    :nocodelens:

    import datetime
    
    print(datetime.date.today())


Pero a diferencia de Pascal y C, acá podemos elegir importar una función
o algo en particular de ese módulo, en lugar de traerlo todo. Para eso
tendríamos que poner en primer lugar la cláusula ``from``, luego el
nombre del módulo y a continuación la cláusula ``import`` todo lo que
queremos importar separada por comas. Por ejemplo, del módulo
``datetime`` podríamos traer los submódulos ``date`` y ``time``.
Después, para usarlos simplemente lo hacemos llamando lo que importamos
sin el nombre del módulo.

.. activecode:: py_30
    :nocodelens:

    from datetime import date, time
    
    print(date.today())
    print(time(1, 23, 32))



Si tenemos un archivo llamado *ejemplo.py* que tiene el siguiente
código:

.. code-block:: Python

    def imprimir(param):
        print(param)

    def sumar(n1, n2):
        return n1+n2

y queremos importarlo a otro archivo y usarlo, podemos hacer:

.. code-block:: Python

    import ejemplo

    ejemplo.imprimir("123")
    print(ejemplo.sumar(2,3))

Y, como dijimos, también podemos importar solo una función de ese módulo
y usarla como si estuviera definida dentro de nuestro contexto.

.. code-block:: Python

    from ejemplo import sumar

    print(sumar(4, 5))

