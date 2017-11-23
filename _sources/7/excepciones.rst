
.. raw:: html

   <!--
   5/11
   Cortes de control
   Pruebas Unitarias(Andres)
   CLASE DE LABORATORIO 
   -->

.. raw:: html

   <!--
   # Corte de control

   TODO: Hacer
   -->

Excepciones
===========

Una excepción es la forma que tiene el intérprete de que indicarle al
programador y/o usuario que ha ocurrido un error. Si la excepción no es
controlada por el desarrollador ésta llega hasta el usuario y termina
abruptamente la ejecución del sistema. Por ejemplo:

.. code:: python

    print 1/0


::


    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-11-e19d6e6ac7e1> in <module>()
    ----> 1 print 1/0
    

    ZeroDivisionError: integer division or modulo by zero


Pero no hay que tenerle miedo a las excepciones, sólo hay que tenerlas
en cuenta y controlarlas en el caso de que ocurran:

.. code:: python

    dividendo = 1
    divisor = 0
    print 'Intentare hacer la división de %d/%d' % (dividendo, divisor)
    try:
        resultado = dividendo / divisor
        print resultado
    except ZeroDivisionError:
        print 'No se puede hacer la división ya que el divisor es 0.'


.. parsed-literal::

    Intentare hacer la división de 1/0
    No se puede hacer la división ya que el divisor es 0.


Pero supongamos que implementamos la regla de tres de la siguiente
forma:

.. code:: python

    def dividir(x, y):
        return x/y
    
    def regla_de_tres(x, y, z):
        return dividir(z*y, x)
    
    
    # Si de 28 alumnos, aprobaron 15, el porcentaje de aprobados es de...
    porcentaje_de_aprobados = regla_de_tres(28, 15, 100)
    print 'Porcentaje de aprobados: %0.2f %%' % porcentaje_de_aprobados


.. parsed-literal::

    Porcentaje de aprobados: 53.00 %


En cambio, si le pasamos 0 en el lugar de x:

.. code:: python

    resultado = regla_de_tres(0, 13, 100)
    print 'Porcentaje de aprobados: %0.2f %%' % resultado


::


    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-14-9a6333da0823> in <module>()
    ----> 1 resultado = regla_de_tres(0, 13, 100)
          2 print 'Porcentaje de aprobados: %0.2f %%' % resultado


    <ipython-input-13-745c31bab81a> in regla_de_tres(x, y, z)
          3 
          4 def regla_de_tres(x, y, z):
    ----> 5     return dividir(z*y, x)
          6 
          7 


    <ipython-input-13-745c31bab81a> in dividir(x, y)
          1 def dividir(x, y):
    ----> 2     return x/y
          3 
          4 def regla_de_tres(x, y, z):
          5     return dividir(z*y, x)


    ZeroDivisionError: integer division or modulo by zero


Acá podemos ver todo el *traceback* o *stacktrace*, que son el cómo se
fueron llamando las distintas funciones entre sí hasta que llegamos al
error. Pero no es bueno que este tipo de excepciones las vea
directamente el usuario, por lo que podemos controlarlas en distintos
momentos. Se pueden controlar inmediatamente donde ocurre el error, como
mostramos antes, o en cualquier parte de este *stacktrace*. En el caso
de la ``regla_de_tres`` no nos conviene poner el ``try/except``
encerrando la línea ``x/y``, ya que en ese punto no tenemos toda la
información que necesitamos para informarle correctamente al usuario,
por lo que podemos ponerla en:

.. code:: python

    def dividir(x, y):
        return x/y
    
    def regla_de_tres(x, y, z):
        resultado = 0
        try:
            resultado = dividir(z*y, x)
        except ZeroDivisionError:
            print 'No se puede calcular la regla de tres ' \
                  'porque el divisor es 0'
            
        return resultado
            
    print regla_de_tres(0, 1, 2)


.. parsed-literal::

    No se puede calcular la regla de tres porque el divisor es 0
    0


Pero en este caso igual muestra 0, por lo que si queremos, podemos poner
los try/except incluso más arriba en el stacktrace:

.. code:: python

    def dividir(x, y):
        return x/y
    
    def regla_de_tres(x, y, z):
        return dividir(z*y, x)
            
    try:
        print regla_de_tres(0, 1, 2)
    except ZeroDivisionError:
        print 'No se puede calcular la regla de tres ' \
              'porque el divisor es 0'



.. parsed-literal::

    No se puede calcular la regla de tres porque el divisor es 0


Todos los casos son distintos y no hay UN lugar ideal dónde capturar la
excepción; es cuestión del desarrollador decidir dónde conviene ponerlo
para cada problema.

Capturar múltiples excepciones
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Una única línea puede lanzar distintas excepciones, por lo que capturar
un tipo de excepción en particular no me asegura que el programa no
pueda lanzar un error en esa línea que supuestamente es segura: En
algunos casos tenemos en cuenta que el código puede lanzar una excepción
como la de ``ZeroDivisionError``, pero eso puede no ser suficiente:

.. code:: python

    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print 'El resultado es: %s' % resultado
        except ZeroDivisionError:
            print 'ERROR: Ha ocurrido un error por mezclar tipos de datos'
    
    dividir_numeros(1, 0)
    dividir_numeros(10, 2)
    dividir_numeros("10", 2)


.. parsed-literal::

    ERROR: Ha ocurrido un error por mezclar tipos de datos
    El resultado es: 5


::


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-17-0976f95f1946> in <module>()
          8 dividir_numeros(1, 0)
          9 dividir_numeros(10, 2)
    ---> 10 dividir_numeros("10", 2)
    

    <ipython-input-17-0976f95f1946> in dividir_numeros(x, y)
          1 def dividir_numeros(x, y):
          2     try:
    ----> 3         resultado = x/y
          4         print 'El resultado es: %s' % resultado
          5     except ZeroDivisionError:


    TypeError: unsupported operand type(s) for /: 'str' and 'int'


En esos casos podemos capturar más de una excepción de la siguiente
forma:

.. code:: python

    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print 'El resultado es: %s' % resultado
        except TypeError:
            print 'ERROR: Ha ocurrido un error por mezclar tipos de datos'
        except ZeroDivisionError:
            print 'ERROR: Ha ocurrido un error de división por cero'
        except Exception:
            print 'ERROR: Ha ocurrido un error inesperado'
    
    dividir_numeros(1, 0)
    dividir_numeros(10, 2)
    dividir_numeros("10", 2)


.. parsed-literal::

    ERROR: Ha ocurrido un error de división por cero
    El resultado es: 5
    ERROR: Ha ocurrido un error por mezclar tipos de datos


Incluso, si queremos que los dos errores muestren el mismo mensaje
podemos capturar ambas excepciones juntas:

.. code:: python

    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print 'El resultado es: %s' % resultado
        except (ZeroDivisionError, TypeError):
            print 'ERROR: No se puede calcular la división'
    
    dividir_numeros(1, 0)
    dividir_numeros(10, 2)
    dividir_numeros("10", 2)


.. parsed-literal::

    ERROR: No se puede calcular la división
    El resultado es: 5
    ERROR: No se puede calcular la división


Jerarquía de excepciones
~~~~~~~~~~~~~~~~~~~~~~~~

Existe una jerarquía de excepciones, de forma que si se sabe que puede
venir un tipo de error, pero no se sabe exactamente qué excepción puede
ocurrir siempre se puede poner una excepción de mayor jerarquía:

Por lo que el error de división por cero se puede evitar como:

.. code:: python

    try:
        print 1/0
    except ZeroDivisionError:
        print 'Ha ocurrido un error de división por cero'


.. parsed-literal::

    Ha ocurrido un error de división por cero


Y también como:

.. code:: python

    try:
        print 1/0
    except Exception:
        print 'Ha ocurrido un error inesperado'


.. parsed-literal::

    Ha ocurrido un error inesperado


Si bien siempre se puede poner Exception en lugar del tipo de excepción
que se espera, no es una buena práctica de programación ya que se pueden
esconder errores indeseados. Por ejemplo, un error de sintaxis. Además,
cuando se lanza una excepción en el bloque ``try``, el intérprete
comienza a buscar entre todas cláusulas ``except`` una que coincida con
el error que se produjo, o que sea de mayor jerarquía. Por lo tanto, es
recomendable poner siempre las excepciones más específicas al principio
y las más generales al final:

.. code:: python

    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print 'El resultado es: %s' % resultado
        except TypeError:
            print 'ERROR: Ha ocurrido un error por mezclar tipos de datos'
        except ZeroDivisionError:
            print 'ERROR: Ha ocurrido un error de división por cero'
        except Exception:
            print 'ERROR: Ha ocurrido un error inesperado'

Si el error no es capturado por ninguna clausula se propaga de la misma
forma que si no se hubiera puesto nada.

Otras cláusulas para el manejo de excepciones
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Además de las cláusulas ``try`` y ``except`` existen otras relacionadas
con las excepciones que nos permiten manejar de mejor manera el flujo
del programa: \* **else**: se usa para definir un bloque de código que
se ejecutará **sólo si no ocurrió ningún error**. \* **finally**: se usa
para definir un bloque de código que se ejecutará **siempre**,
independientemente de si se lanzó una excepción o no.

.. code:: python

    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print 'El resultado es {}'.format(resultado)
        except ZeroDivisionError:
            print 'Error: División por cero'
        else:
            print 'Este mensaje se mostrará sólo si no ocurre ningún error'
        finally: 
            print 'Este bloque de código se muestra siempre'
    
    dividir_numeros(1, 0)
    print '-------------'
    dividir_numeros(10, 2)


.. parsed-literal::

    Error: División por cero
    Este bloque de código se muestra siempre
    -------------
    El resultado es 5
    Este mensaje se mostrará sólo si no ocurre ningún error
    Este bloque de código se muestra siempre


Pero entonces, ¿por qué no poner ese código dentro del ``try-except``?.
Porque tal vez no queremos capturar con las cláusulas ``except`` lo que
se ejecute en ese bloque de código:

.. code:: python

    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print 'El resultado es {}'.format(resultado)
        except ZeroDivisionError:
            print 'Error: División por cero'
        else:
            print 'Ahora hago que ocurra una excepción'
            print 1/0
        finally: 
            print 'Este bloque de código se muestra siempre'
    
    dividir_numeros(1, 0)
    print '-------------'
    dividir_numeros(10, 2)


.. parsed-literal::

    Error: División por cero
    Este bloque de código se muestra siempre
    -------------
    El resultado es 5
    Ahora hago que ocurra una excepción
    Este bloque de código se muestra siempre


::


    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-24-a9e50d1c2355> in <module>()
         13 dividir_numeros(1, 0)
         14 print '-------------'
    ---> 15 dividir_numeros(10, 2)
    

    <ipython-input-24-a9e50d1c2355> in dividir_numeros(x, y)
          7     else:
          8         print 'Ahora hago que ocurra una excepción'
    ----> 9         print 1/0
         10     finally:
         11         print 'Este bloque de código se muestra siempre'


    ZeroDivisionError: integer division or modulo by zero


Lanzar excepciones
~~~~~~~~~~~~~~~~~~

Hasta ahora vimos cómo capturar un error y trabajar con él sin que el
programa termine abruptamente, pero en algunos casos somos nosotros
mismos quienes van a querer lanzar una excepción. Y para eso, usaremos
la palabra reservada ``raise``:

.. code:: python

    def dividir_numeros(x, y):
        if y == 0:
            raise Exception('Error de división por cero')
        
        resultado = x/y
        print 'El resultado es {0}'.format(resultado)
    
    try:
        dividir_numeros(1, 0)
    except ZeroDivisionError as e:
        print 'ERROR: División por cero'
    except Exception as e:
        print 'ERROR: ha ocurrido un error del tipo Exception'
    
    print '----------'
    dividir_numeros(1, 0)



.. parsed-literal::

    ERROR: ha ocurrido un error del tipo Exception
    ----------


::


    ---------------------------------------------------------------------------

    Exception                                 Traceback (most recent call last)

    <ipython-input-25-e8d834f7341d> in <module>()
         14 
         15 print '----------'
    ---> 16 dividir_numeros(1, 0)
    

    <ipython-input-25-e8d834f7341d> in dividir_numeros(x, y)
          1 def dividir_numeros(x, y):
          2     if y == 0:
    ----> 3         raise Exception('Error de división por cero')
          4 
          5     resultado = x/y


    Exception: Error de división por cero


Crear excepciones
~~~~~~~~~~~~~~~~~

Pero así como podemos usar las excepciones estándares, también podemos
crear nuestras propias excepciones:

.. code:: python


    class MiPropiaExcepcion(Exception):
        
        def __str__(self):
            return 'Mensaje del error'

Por ejemplo:

.. code:: python

    class ExcepcionDeDivisionPor2(Exception):
        
        def __str__(self):
            return 'ERROR: No se puede dividir por dos'
        
    
    def dividir_numeros(x, y):
        if y == 2:
            raise ExcepcionDeDivisionPor2()
        
        resultado = x/y
    
    try:
        dividir_numeros(1, 2)
    except ExcepcionDeDivisionPor2:
        print 'No se puede dividir por 2'
    
    dividir_numeros(1, 2)


.. parsed-literal::

    No se puede dividir por 2


::


    ---------------------------------------------------------------------------

    ExcepcionDeDivisionPor2                   Traceback (most recent call last)

    <ipython-input-26-f793162bfdde> in <module>()
         16     print 'No se puede dividir por 2'
         17 
    ---> 18 dividir_numeros(1, 2)
    

    <ipython-input-26-f793162bfdde> in dividir_numeros(x, y)
          7 def dividir_numeros(x, y):
          8     if y == 2:
    ----> 9         raise ExcepcionDeDivisionPor2()
         10 
         11     resultado = x/y


    ExcepcionDeDivisionPor2: ERROR: No se puede dividir por dos


Para más información, ingresar a
https://docs.python.org/2/tutorial/errors.html



