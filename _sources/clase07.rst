
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


Testing
=======

Cuando estamos desarrollando un programa, si hicimos las cosas con
responsabilidad y ejecutamos el programa, hicimos algunas pruebas, etc,
podemos afirmar que lo que hicimos, con mayor o menor seguridad,
funciona. A partir de ese momento y hasta la próxima vez que se
modifique el código, o que alguien encuentre una falla en el sistema
(bug) podemos seguir manteniendo esa afirmación. Supongamos que después
de tiempo viene el usuario y nos pide un cambio en el funcionamiento del
programa... una vez que modificamos el código para incorporar ese
requerimiento del usuario tenemos que probar nuevamente todo el programa
para asegurarnos que con esa modificación no rompimos nada. En programas
chicos esto no tiene un gran impacto, pero si pensamos en un programa
que actualmente se está usando y se estuvo desarrollando por años, un
pequeño cambio podría requerir semanas de pruebas. Y es por eso que no
todo el código que escribimos en nuestra vida profesional está destinado
a ser ejecutado por el usuario final, gran parte, está destinado a
asegurar que nuestro código funciona como nosotros decimos que funciona.
Existen varias formas de probar automáticamente nuestro código: \*
Pruebas unitarias \* Pruebas de integración \* Pruebas funcionales \*
Pruebas de regresión

Pero por el momento nos centraremos en lo que son las pruebas unitarias.

Pruebas unitarias
-----------------

Las pruebas unitarias son catalogadas de caja blanca, ya que es
necesario conocer el código para poder escribirlas. Estas pruebas tienen
que ser:

-  *Automatizables:* tienen que poder correrse todas las pruebas
   automáticamente sin intervención del usuario
-  *Repetibles:* se tienen que poder correrse varias veces y dar los
   mismos resultados
-  *Independientes:* la ejecución de una prueba no debe afectar al resto
-  *Aisladas:* la ejecución de una prueba no debe fallar por una falla
   ajena al código que estamos probando
-  *Con un único objetivo:* cada prueba debe tener como objetivo probar
   una única cosa

Las ventajas de realizar pruebas unitarias son:

-  *Documentan el código:* al leer las pruebas puede entender qué es lo
   que intenta hacer el código
-  *Dan seguridad al momento hacer cambios:* al momento de incorporar
   nuevos requerimientos del usuario, o al realizar un *refactor*, se
   pueden correr las pruebas y asegurarse rápidamente si el código sigue
   funcionando como se esperaba o no.
-  *Los errores son más fáciles de encontrar:* al momento de correr las
   pruebas y encontrar que falla un test, sólo tenemos que ir a la
   función que prueba ese test y fijarnos si lo que está mal es el test
   o la función.
-  *Diseñan:* si las pruebas se escriben antes que el código que deben
   probar ayudan a comprender lo que tiene que hacer esa función y en
   cierto sentido ayudan a diseñar la solución a implementar

Etapas de una prueba
~~~~~~~~~~~~~~~~~~~~

Las etapas de una prueba unitaria son:

1. *Setup*: Preparar el contexto para poder ejecutar el código a testear
2. *Exercise*: Ejecución de la función a testear
3. *Verify*: Verificar que el resultado obtenido es igual al resultado
   esperado

Cómo realizar las pruebas
~~~~~~~~~~~~~~~~~~~~~~~~~

Al momento de desarrollarlas:

1. se elige una función a probar
2. se elige cuáles son sus parámetros de entrada
3. en función de los parámetros de entrada, se determina cuáles son los
   parámetros de salida de esa función
4. al definir los parámetros de entrada, podemos anticipar cual será el
   flujo de sentencias que se ejecutarán dentro de la función, por lo
   que podríamos iterar varias veces los puntos 2 y 3 hasta lograr pasar
   por todas las líneas de la función (nos ayuda a identificar código
   muerto), o, por lo menos, hasta alcanzar el nivel de cobertura
   deseado.

Es importante tener en cuenta no sólo los casos felices, sino también
los que tienen que mostrar algún mensaje de error para asegurarnos que
el código maneje esos errores como corresponde.

En python
~~~~~~~~~

En la versión 2.1 de python se incluyó el módulo
`unittest <https://docs.python.org/2/library/unittest.html>`__ que es
uno de los que usualmente se utiliza para implementar estas pruebas. La
estructura de un archivo que contenga las pruebas debe ser:

.. code:: python

    # encoding: utf-8
    import unittest  # Importar el módulo unittest


    # Crear una clase que herede de unittest.TestCase
    class TestStringMethods(unittest.TestCase):

        # Definir un método que comience con test
        def test_upper_of_foo_will_return_foo_in_uppercase(self):
            # Setup
            target = 'foo'
            expected_result = 'FOO'
            
            # Exercise
            result = target.upper()
        
            # Verify
            self.assertEqual(result, expected_result)

        # Definir un método que comience con test
        def test_isupper_of_upper_target_will_return_true(self):
            # Setup
            target = 'FOO'
            
            # Exercise
            result = target.isupper()
        
            # Verify
            self.assertTrue(result)

        # Definir un método que comience con test
        def test_isupper_of_capitalize_target_will_return_false(self):
            # Setup
            target = 'Foo'
            
            # Exercise
            result = target.isupper()
        
            # Verify
            self.assertFalse(result)


    # Esto es opcional, pero si se quiere ejecutar los tests
    # como python test_de_strings.py es necesario.
    if __name__ == '__main__':
        unittest.main()

Y si suponemos que el archivo se llama ``test_de_strings.py`` y lo
ejecutamos con el comando ``python test_de_strings.py`` nos mostrará en
la consola:

::

    ...
    ----------------------------------------------------------------------
    Ran 3 tests in 0.000s

    OK

Y si a la clase ``TestStringMethods`` le agregamos el siguiente método:

.. code:: python

        def test_isupper_of_lower_target_will_return_true(self):
            # Setup
            target = 'foo'
            
            # Exercise
            result = target.isupper()
        
            # Verify
            self.assertTrue(result)

Va a fallar este nuevo test, ya que ``result`` valdrá *False*.

::

    .F..
    ======================================================================
    FAIL: test_isupper_of_lower_target_will_return_true (__main__.TestStringMethods)
    ----------------------------------------------------------------------
    Traceback (most recent call last):
      File "test_de_strings.py", line 50, in test_isupper_of_lower_target_will_return_true
        self.assertTrue(result)
    AssertionError: False is not true

    ----------------------------------------------------------------------
    Ran 4 tests in 0.001s

    FAILED (failures=1)

Descubriendo los tests
^^^^^^^^^^^^^^^^^^^^^^

Otra forma de ejecutar estos tests es, parado en la misma carpeta donde
se encuentra el archivo, ejecutando el comando
``python -m unittest discover`` y en ese caso no es necesario poner al
final del archivo las líneas:

.. code:: python

    if __name__ == '__main__':
        unittest.main()

En realidad, no es necesario que se encuentren en la misma carpeta, lo
que tiene que pasar es que se encuentre dentro del mismo
`paquete <https://docs.python.org/2/tutorial/modules.html#packages>`__.
Y eso en python para eso se usan los archivos ``__init__.py``.

Ejemplo
-------

Supongamos que tenemos que hacer una función que parsea una línea de un
archivo de texto sabiendo que es un archivo CSV (por lo que cada campo
estará separado por una coma) y el formato es:

::

    numero_de_partido,goles_local,goles_visitante # comentario

Donde:

-  ``numero_de_partido``: es un número entero mayor a 1 (no tiene límite
   superior)
-  ``goles_local`` y ``goles_visitante``: son los goles convertidos por
   cada uno de los equipos
-  A continuación de los goles del equipo visitante pueden venir,
   opcionalmente, una cantidad no determinada de espacios e, incluso, un
   comentario anteponiendo el caracter #.

Dicha función tiene que retornar un diccionario con los campos provistos
por el archivo.

Si pudieramos asumir que el archivo siempre tendrá líneas válidas, una
posible solución podría ser:

.. code:: python

    def parsear_linea_prode(linea):
        '''Función que no parsea una línea de un archivo
        CSV con los resultados de un partido.
        return: Diccionario con las claves numero_de_partido,
        goles_local y goles_visitante.
        '''

        sin_comentario = linea.partition('#')[0]
        sin_espacios = sin_comentario.strip()
        id_partido, goles_loc, goles_vis = sin_espacios.split(',')
        resultado = {
           'numero_partido': int(id_partido),
           'goles_local': int(goles_loc),
           'goles_visitante': int(goles_vis)
        }

        return resultado

Para asegurarnos que nuestro código funciona correctamente podríamos
agregar los siguientes test:

.. code:: python

    #!/usr/bin/env python
    # -*- coding: utf-8 -*-
    import unittest
    from prode import parsear_linea_prode


    class TestParsearLineasFixture(unittest.TestCase):

        def test_parsear_linea_prode_parsea_bien_la_primer_linea(self):
            # Setup
            linea = '1,0,0'
            resultado_esperado = {
                'numero_partido': 1,
                'goles_local': 0,
                'goles_visitante': 0
            }

            # Exercise
            resultado = parsear_linea_prode(linea)

            # Verify
            self.assertEquals(resultado, resultado_esperado)
        
        def test_parsear_linea_prode_ignora_el_comentario_despues_del_numeral(self):
            # Setup
            linea = '1,0,0   # Chile vs Ecuador'
            resultado_esperado = {
                'numero_partido': 1,
                'goles_local': 0,
                'goles_visitante': 0
            }

            # Exercise
            resultado = parsear_linea_prode(linea)

            # Verify
            self.assertEquals(resultado, resultado_esperado)

        def test_parsear_linea_prode_ignora_el_enter_al_final_de_la_linea(self):
            # Setup
            linea = '1,0,0   # Chile vs Ecuador\n'
            resultado_esperado = {
                'numero_partido': 1,
                'goles_local': 0,
                'goles_visitante': 0
            }

            # Exercise
            resultado = parsear_linea_prode(linea)

            # Verify
            self.assertEquals(resultado, resultado_esperado)

        def test_parsear_linea_para_valores_mayores_a_10_tambien_funciona(self):
            # Setup
            linea = '999,123,432   # Chile vs Ecuador\n'
            resultado_esperado = {
                'numero_partido': 999,
                'goles_local': 123,
                'goles_visitante': 432
            }

            # Exercise
            resultado = parsear_linea_prode(linea)

            # Verify
            self.assertEquals(resultado, resultado_esperado)


    if __name__ == '__main__':
        unittest.main()

Pero qué pasa si después nos agregan un requerimiento en el que dicen
que, en

.. code:: python

        def test_parsear_linea_prode_retorna_un_diccionario_vacio_cuando_le_pasan_una_linea_vacia(self):
            # Setup
            linea = ''
            resultado_esperado = {}

            # Exercise
            resultado = parsear_linea_prode(linea)

            # Verify
            self.assertEquals(resultado, resultado_esperado)

        def test_parsear_linea_prode_retorna_un_diccionario_vacio_cuando_le_pasan_4_valores(self):
            # Setup
            linea = '1,2,3,4'
            resultado_esperado = {}

            # Exercise
            resultado = parsear_linea_prode(linea)

            # Verify
            self.assertEquals(resultado, resultado_esperado)

        def test_parsear_linea_prode_retorna_un_diccionario_vacio_cuando_le_pasan_2_valores(self):
            # Setup
            linea = '1,2'
            resultado_esperado = {}

            # Exercise
            resultado = parsear_linea_prode(linea)

            # Verify
            self.assertEquals(resultado, resultado_esperado)

        def test_parsear_linea_prode_retorna_un_diccionario_vacio_cuando_le_pasan_comentario_sin_numeral(self):
            # Setup
            linea = '1,2,3 comentario'
            resultado_esperado = {}

            # Exercise
            resultado = parsear_linea_prode(linea)

            # Verify
            self.assertEquals(resultado, resultado_esperado)

        def test_parsear_linea_prode_retorna_un_diccionario_vacio_cuando_le_pasan_una_letra(self):
            # Setup
            linea = '1,a,3'
            resultado_esperado = {}

            # Exercise
            resultado = parsear_linea_prode(linea)

            # Verify
            self.assertEquals(resultado, resultado_esperado)

.. raw:: html

   <!--
   ## TDD (Test Driven Development)

   TDD es una metodología de desarrollo que se basa fuertemente en las pruebas unitarias. De hecho, sus dos principales reglas son:

   1. Primero se escriben los test, y luego, el código que cumple con esos test
   2. No se escribe código más allá del que es necesario para cumplir con la batería de test que se tengan por el momento
   -->

Otros frameworks
----------------

`Nosetest <https://nose.readthedocs.org/en/latest/>`__ y
`py.test <http://pytest.org/latest/>`__. Para más información se puede
ver: http://docs.python-guide.org/en/latest/writing/tests/
