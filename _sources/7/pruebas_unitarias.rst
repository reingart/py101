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

.. activecode:: py_08
    :nocodelens:


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
