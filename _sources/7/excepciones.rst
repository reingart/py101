Excepciones
===========

Una excepción es la forma que tiene el intérprete de que indicarle al
programador y/o usuario que ha ocurrido un error. Si la excepción no es
controlada por el desarrollador ésta llega hasta el usuario y termina
abruptamente la ejecución del sistema. Por ejemplo:

.. activecode:: py_01
    :nocodelens:

    print(1/0)


Pero no hay que tenerle miedo a las excepciones, sólo hay que tenerlas
en cuenta y controlarlas en el caso de que ocurran:

.. activecode:: py_02
    :nocodelens:

    dividendo = 1
    divisor = 0
    print('Intentare hacer la división de %d/%d' % (dividendo, divisor))
    try:
        resultado = dividendo / divisor
        print(resultado)
    except ZeroDivisionError:
        print('No se puede hacer la división ya que el divisor es 0.')


Pero supongamos que implementamos la regla de tres de la siguiente
forma:

.. activecode:: py_03
    :nocodelens:

    def dividir(x, y):
        return x/y
    
    def regla_de_tres(x, y, z):
        return dividir(z*y, x)
    
    
    # Si de 28 alumnos, aprobaron 15, el porcentaje de aprobados es de...
    porcentaje_de_aprobados = regla_de_tres(28, 15, 100)
    print('Porcentaje de aprobados: %0.2f %%' % porcentaje_de_aprobados)



En cambio, si le pasamos 0 en el lugar de x:

.. activecode:: py_04
    :nocodelens:
    :include: py_03

    resultado = regla_de_tres(0, 13, 100)
    print('Porcentaje de aprobados: %0.2f %%' % resultado)


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

.. activecode:: py_05
    :nocodelens:

    def dividir(x, y):
        return x/y
    
    def regla_de_tres(x, y, z):
        resultado = 0
        try:
            resultado = dividir(z*y, x)
        except ZeroDivisionError:
            print('No se puede calcular la regla de tres '
                  'porque el divisor es 0')
            
        return resultado
            
    print(regla_de_tres(0, 1, 2))



Pero en este caso igual muestra 0, por lo que si queremos, podemos poner
los try/except incluso más arriba en el stacktrace:

.. activecode:: py_06
    :nocodelens:

    def dividir(x, y):
        return x/y
    
    def regla_de_tres(x, y, z):
        return dividir(z*y, x)
            
    try:
        print(regla_de_tres(0, 1, 2))
    except ZeroDivisionError:
        print('No se puede calcular la regla de tres '
              'porque el divisor es 0')



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

.. activecode:: py_07
    :nocodelens:

    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print('El resultado es: %s' % resultado)
        except ZeroDivisionError:
            print('ERROR: Ha ocurrido un error por mezclar tipos de datos')
    
    dividir_numeros(1, 0)
    dividir_numeros(10, 2)
    dividir_numeros("10", 2)



En esos casos podemos capturar más de una excepción de la siguiente
forma:

.. activecode:: py_08
    :nocodelens:

    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print('El resultado es: %s' % resultado)
        except TypeError:
            print('ERROR: Ha ocurrido un error por mezclar tipos de datos')
        except ZeroDivisionError:
            print('ERROR: Ha ocurrido un error de división por cero')
        except Exception:
            print('ERROR: Ha ocurrido un error inesperado')
    
    dividir_numeros(1, 0)
    dividir_numeros(10, 2)
    dividir_numeros("10", 2)



Incluso, si queremos que los dos errores muestren el mismo mensaje
podemos capturar ambas excepciones juntas:

.. activecode:: py_09
    :nocodelens:

    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print('El resultado es: %s' % resultado)
        except (ZeroDivisionError, TypeError):
            print('ERROR: No se puede calcular la división')
    
    dividir_numeros(1, 0)
    dividir_numeros(10, 2)
    dividir_numeros("10", 2)



Jerarquía de excepciones
~~~~~~~~~~~~~~~~~~~~~~~~

Existe una jerarquía de excepciones, de forma que si se sabe que puede
venir un tipo de error, pero no se sabe exactamente qué excepción puede
ocurrir siempre se puede poner una excepción de mayor jerarquía:

Por lo que el error de división por cero se puede evitar como:

.. activecode:: py_10
    :nocodelens:

    try:
        print(1/0)
    except ZeroDivisionError:
        print('Ha ocurrido un error de división por cero')


Y también como:

.. activecode:: py_11
    :nocodelens:

    try:
        print(1/0)
    except Exception:
        print('Ha ocurrido un error inesperado')


Si bien siempre se puede poner Exception en lugar del tipo de excepción
que se espera, no es una buena práctica de programación ya que se pueden
esconder errores indeseados. Por ejemplo, un error de sintaxis. Además,
cuando se lanza una excepción en el bloque ``try``, el intérprete
comienza a buscar entre todas cláusulas ``except`` una que coincida con
el error que se produjo, o que sea de mayor jerarquía. Por lo tanto, es
recomendable poner siempre las excepciones más específicas al principio
y las más generales al final:

.. activecode:: py_12
    :nocodelens:


    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print('El resultado es: %s' % resultado)
        except TypeError:
            print('ERROR: Ha ocurrido un error por mezclar tipos de datos')
        except ZeroDivisionError:
            print('ERROR: Ha ocurrido un error de división por cero')
        except Exception:
            print('ERROR: Ha ocurrido un error inesperado')

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

.. activecode:: py_13
    :nocodelens:


    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print('El resultado es {}'.format(resultado))
        except ZeroDivisionError:
            print('Error: División por cero')
        else:
            print('Este mensaje se mostrará sólo si no ocurre ningún error')
        finally: 
            print('Este bloque de código se muestra siempre')
    
    dividir_numeros(1, 0)
    print('-------------')
    dividir_numeros(10, 2)


Pero entonces, ¿por qué no poner ese código dentro del ``try-except``?.
Porque tal vez no queremos capturar con las cláusulas ``except`` lo que
se ejecute en ese bloque de código:

.. activecode:: py_14
    :nocodelens:


    def dividir_numeros(x, y):
        try:
            resultado = x/y
            print('El resultado es {}'.format(resultado))
        except ZeroDivisionError:
            print('Error: División por cero')
        else:
            print('Ahora hago que ocurra una excepción')
            print(1/0)
        finally: 
            print('Este bloque de código se muestra siempre')
    
    dividir_numeros(1, 0)
    print('-------------')
    dividir_numeros(10, 2)


Lanzar excepciones
~~~~~~~~~~~~~~~~~~

Hasta ahora vimos cómo capturar un error y trabajar con él sin que el
programa termine abruptamente, pero en algunos casos somos nosotros
mismos quienes van a querer lanzar una excepción. Y para eso, usaremos
la palabra reservada ``raise``:

.. activecode:: py_15
    :nocodelens:


    def dividir_numeros(x, y):
        if y == 0:
            raise Exception('Error de división por cero')
        
        resultado = x/y
        print('El resultado es {0}'.format(resultado))
    
    try:
        dividir_numeros(1, 0)
    except ZeroDivisionError as e:
        print('ERROR: División por cero')
    except Exception as e:
        print('ERROR: ha ocurrido un error del tipo Exception')
    
    print('----------')
    dividir_numeros(1, 0)



Crear excepciones
~~~~~~~~~~~~~~~~~

Pero así como podemos usar las excepciones estándares, también podemos
crear nuestras propias excepciones:

.. activecode:: py_16
    :nocodelens:

    class MiPropiaExcepcion(Exception):
        
        def __str__(self):
            return 'Mensaje del error'

Por ejemplo:

.. activecode:: py_17
    :nocodelens:


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
        print('No se puede dividir por 2')
    
    dividir_numeros(1, 2)


Para más información, ingresar a
https://docs.python.org/3/tutorial/errors.html



