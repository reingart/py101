
.. raw:: html

   <!--
   15/10
   Características del Python. Lenguajes compilados vs interpretados. Tipado estático vs dinámico. Fuertemente tipado vs débilmente tipado.
   Variables. Operaciones Elementales. Tipos de Datos atómicos. Estructuras de Control Selectivas
   -->

Python
======

Python es un lenguaje de alto nivel creado por Guido van Rossum a
finales del año 1989 y que tuvo si primer versión pública (0.9.0) en
Febrero de 1991.

Mientras Guido participaba del desarrollo de un sistema
operativo llamado Amoeba OS, se enfrentaba a ciertos problemas que eran
muy complejos para ser desarrollado en Bash, pero desarrollarlos en C le
parecía un exceso, por lo tanto, creó Python como lenguaje intermedio
entre Bash y C.

.. raw:: html

   <!-- http://pythoniza.me/books/ -->

Compilado vs Interpretado
-------------------------

Existen infinitas clasificaciones para los lenguajes de programación,
entre ellas una que los distingue en función de cuándo requieren de una
aplicación para que la computadora entienda el código escrito por el
desarrollador:

**Compilador:** programa que lee todo el
código una única vez y lo traduce al lenguaje binario que es el que
entiende la computadora. Sería el equivalente a traducir un libro. Cada
frase se traduce una única vez y después tal vez nunca se la lee, o tal
vez se la lee mil veces, pero la frase ya esta traducida. \*

**Intérprete:** programa que lee el código a medida que lo necesita y
va traduciendo al binario, la computadora ejecuta la instrucción que el
intérprete le pide, y descarta esa traducción; por lo que cuando vuelva
a pasar por esa misma porción de código, deberá volver a traducirla. Es
el equivalente a un intérprete en una conferencia, si el orador repite
la misma frase más de una vez, éste tiene que volver a traducirla.

+----------+-------------+---------------+
| **Compil | **Interpret |
| ado**    | ado**       |
+==========+=============+===============+
| Velocida | Lento, hay  | Rápido, se    |
| d        | que         | modifica el   |
| de       | compilar    | código y se   |
| desarrol | cada vez y  | vuelve a      |
| lo       | es una      | probar. A     |
|          | tarea que   | veces, ni     |
|          | puede       | siquiera      |
|          | tardar      | requiere      |
|          | varios      | reiniciar el  |
|          | minutos     | programa      |
+----------+-------------+---------------+
| Velocida | Rápido, se  | Lento, es     |
| d        | compila una | necesario     |
| de       | única vez   | leer,         |
| ejecució | todo el     | interpretar y |
| n        | programa y  | traducir el   |
|          | el          | código        |
|          | ejecutable  | mientras el   |
|          | generado ya | programa está |
|          | lo entiende | corriendo     |
|          | la máquina  |               |
+----------+-------------+---------------+
| Dependen | Si, siempre | No, con       |
| cia      | que se      | instalar el   |
| de la    | genera un   | intérprete en |
| platafor | ejecutable  | la            |
| ma       | es para una | computadora   |
|          | arquitectur | que se quiere |
|          | a           | correr el     |
|          | en          | programa es   |
|          | particular. | suficiente    |
|          | Por         |               |
|          | ejemplo,    |               |
|          | para        |               |
|          | Windows de  |               |
|          | 32 bits,    |               |
|          | linux de 64 |               |
|          | bits, etc.  |               |
+----------+-------------+---------------+
| Dependen | No, una vez | Si, siempre   |
| cia      | que se      | que se quiera |
| del      | compilo no  | correr el     |
| lenguaje | es          | programa es   |
|          | necesario   | necesario     |
|          | instalar el | instalar el   |
|          | compilador  | intérprete    |
|          | para        |               |
|          | ejecutar el |               |
|          | programa    |               |
+----------+-------------+---------------+

Si bien Python es un lenguaje interpretado, en realidad se podría
compilar el código y algo de eso hace sólo el intérprete cuando genera
los archivos \*.pyc.

Tipado estático vs tipado dinámico
----------------------------------

Otra posible clasificación radica en si una variable puede cambiar el
tipo de dato que se puede almacenar en ella entre una sentencia y la
siguiente (tipado dinámico). O si en la etapa de definición se le asigna
un tipo de dato a una variable y, por más que se puede cambiar el
contenido de la misma, no cambie el tipo de dato de lo que se almacena
en ella (tipado estático).

Fuertemente tipado vs débilmente tipado
---------------------------------------

Y por último, también podríamos clasificar los lenguajes en función de
la posibilidad que nos brindan para mezclar distintos tipos de datos. Se
dice que un lenguaje es *fuertemente tipado* cuando **no** se pueden
mezclar dos variables de distinto tipo lanzando un error o una
excepción. Por el contrario, cuando se pueden mezclar dos variables de
distinto tipo, realizar una operación entre ellas y obtener un resultado
se dice que es un lenguaje *débilmente tipado*. Por ejemplo, en
javascript (lenguaje débilmente tipado), si queremos sumar el string '1'
con el número 2 dá como resultado el string '12', cuando en Python lanza
una excepción al momento de ejecutar el código y, en Pascal, lanza un
error al momento de querer compilar el código.

Declaración y definición de variables
-------------------------------------

En lenguajes como Pascal, la declaración y la definición de variables se
encuentran en dos momentos distintos. La **declaración** se dá dentro
del bloque *var* y es donde el desarrollador le indica al compilador que
va a necesitar una porción de memoria para almacenar algo de un tipo de
dato en particular y va a referirse a esa porción de memoria con un
cierto nombre. Por ejemplo:

.. code:: pascal

    var
       n : integer;

Se declara que existirá una variable llamada *n* y en ella se podrán
guardar números enteros entre -32.768 y 32.767. La **definición** de esa
variable se dá en el momento en el que se le asigna un valor a esa
variable. Por ejemplo:

.. code:: pascal

    n := 5;

En Python, la declaración y definición de una variable se hacen el mismo
momento:

.. code:: python

    n = 5
    n = 'Hola mundo'

En la primer línea se declara que se usará una variable llamada *n*, que
almacenará un número entero y se la define asignándole el número 5. En
la segunda línea, a esa variable de tipo entero se la "pisa" cambiándole
el tipo a string y se le asigna la cadena de caracteres
``'Hola mundo'``.

Objetivos y características
---------------------------

En 1989 Guido van Rossum era parte del equipo que desarrollaba Amoeba OS
y se dió cuenta que muchos programadores al momento de tener que elegir
un lenguaje para solucionar ciertos problemas se encontraban con que
tenían dos alternativas, pero ninguna cerraba a la perfección: \*
*Bash:* lenguaje de scripting (es el que usa la consola de linux como
intérprete) y en este contexto se quedaba corto y complicaba la solución
\* *C:* lenguaje estructurado con características de bajo, mediano y
alto nivel; pero que en estas circunstancias era demasiado. Era como
matar un mosquito con cañón.

Ante esta situación, e influido por el lenguaje ABC del cual había
participado, es que decidió crear Python como un lenguaje intermedio
entre bash y C que tiene las siguientes características: \* Extensible
(se le pueden agregar módulos en C y Python) \* Multiplataforma (Amoeba
OS, Unix, Windows y Mac) \* Sintaxis simple, clara y sencilla \*
Fuertemente tipado \* Tipado dinámico \* Gran librería estándar \*
Introspección

Filosofia de Python
~~~~~~~~~~~~~~~~~~~

Dentro de lo que es el *Zen de Python* están escritas varias reglas que
debería seguir todo código escrito en Python. Algunas de ellas son: \*
Bello es mejor que feo \* **Explícito es mejor que implícito** \* Simple
es mejor que complejo \* Complejo es mejor que complicado \* **La
legibilidad cuenta** \* Los casos especiales no son tan especiales como
para quebrantar las reglas \* Aunque lo práctico le gana a la pureza \*
**Si la implementación es difícil de explicar, es una mala idea**

Estructura de un programa en Python
-----------------------------------

La estructura de un programa en Python no es tan estricta como puede
serlo en Pascal o en C/C++, ya que no debe comenzar con ninguna palabra
reservada, ni con un procedimiento o función en particular. Simplemente
con escribir un par de líneas de código ya podríamos decir que tenemos
un programa en Python.

Lo que es importante destacar es la forma de identificar los distintos
bloques de código. En Pascal se definía un bloque de código usando las
palabras reservadas ``Begin`` y ``End``; en C/C++ se define mediante el
uso de las llaves (``{`` y ``}``). Sin embargo, en Python, se utiliza la
indentación; es decir, la cantidad de espacios (o tabulaciones) que hay
entre el comienzo de la línea y el primer carácter distinto a ellos.

--------------

Tipos de datos
--------------

En Python a las variables se les puede preguntar de qué tipo son usando
la función type:

.. activecode:: py_00
    :nocodelens:

    variable = 'Hola mundo'
    tipo_de_la_variable = type(variable)
    print(tipo_de_la_variable)

Enteros
~~~~~~~

Python 2 distingue dos tipos de enteros: \* int \* long

En Python 3 directamente existe un único tipo de entero, los int.

.. activecode:: py_01
    :nocodelens:

    # Asigno el número 5 a la variable numero_entero
    numero_entero = 5
    # Imprimo el valor que tiene la variable numero_entero
    print(numero_entero)
    # Imprimo el tipo de la variable numero_entero
    print(type(numero_entero))


Ahora, ¿qué pasa cuando ese número entero crece mucho?, por ejemplo, si
le asignamos 9223372036854775807

.. activecode:: py_02
    :nocodelens:

    # defino dos variables (no imprime)
    numero_entero = 5
    numero_muy_grande = -9223372036854775809

.. activecode:: py_03
    :nocodelens:
    :include: py_02

    print(numero_muy_grande)
    print(type(numero_muy_grande))
    print(2**16/2)


¿Y si ahora le sumamos 1?

.. activecode:: py_04
    :nocodelens:
    :include: py_02

    numero_muy_grande += 1
    print(numero_muy_grande)
    print(type(numero_muy_grande))


Reales
~~~~~~

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
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

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

Complejos
~~~~~~~~~

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

Booleanos
~~~~~~~~~

Python también soporta el tipo de dato booleano:

.. activecode:: py_11
    :nocodelens:

    boolean = True
    print(boolean)
    print(not boolean)
    print(type(boolean))
    print(True or False and True)


También se puede crear un boolean a partir de comparar dos números:

.. activecode:: py_12
    :nocodelens:

    boolean = 5 != 5
    print(boolean)


Incluso, se puede saber fácilmente si un número está dentro de un rango
o no.

.. activecode:: py_13
    :nocodelens:

    numero = 7
    if 5 < numero < 9:
        print('El número 7 se encuentra en el rango entre 5 y 9')
    
    if 5 < numero < 6:
        print('El número 7 se encuentra en el rango entre 5 y 6')

Muchas formas de imprimir el número 25

.. activecode:: py_14
    :nocodelens:

    print("--{0}--".format(25))
    print("--{0:4}--".format(25))    # Ocupando 4 espacios
    print("--{0:04}--".format(25))   # Ocupando 4 espacios y rellenando con 0
    print("--{0:b}--".format(25))    # En binario
    print("--{0:x}--".format(25))    # En hexadecimal
    print("--{0:04x}--".format(25))  # En binario y ocupando 4 espacios y rellenando con 0


Strings
~~~~~~~

En python los strings se pueden armar tanto con comillas simples (')
como dobles ("), lo que no se puede hacer es abrir con unas y cerrar con
otras.

.. activecode:: py_15
    :nocodelens:

    cadena_caracteres = 'Holamundo'
    print(cadena_caracteres)
    print(type(cadena_caracteres))
    
    cadena_caracteres = "Y con doble comilla?, de qué tipo es?"
    print(cadena_caracteres)
    print(type(cadena_caracteres))


Además, se pueden armar strings multilínea poniendo tres comillas
simples o dobles seguidas:

.. activecode:: py_16
    :nocodelens:

    cadena_caracteres = """y si quiero
    usar un string
    que se escriba en varias
    líneas?."""
    print(cadena_caracteres)
    print(type(cadena_caracteres))


Índices y *Slice* en string
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Si queremos obtener un caracter del string podemos acceder a él
simplemente con poner entre corchetes su posición (comenzando con la 0):

.. activecode:: py_18
    :nocodelens:

    cadena_caracteres = 'Hola mundo'
    print(cadena_caracteres)
    print('El septimo caracter de la cadena "{0}" es "{1}"'.format(cadena_caracteres, cadena_caracteres[6]))


+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+
| H   | o   | l   | a   |     | m   | u   | n   | d   | o   |
+=====+=====+=====+=====+=====+=====+=====+=====+=====+=====+
| 0   | 1   | 2   | 3   | 4   | 5   | 6   | 7   | 8   | 9   |
+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+

Aunque también nos podemos referir a ese caracter comenzando por su
posición, pero comenzando a contar desde la última posición (comenzando
en 1):

.. activecode:: py_19
    :nocodelens:

    cadena_caracteres = 'Hola mundo'
    print('El septimo caracter de la cadena "{0}" es "{1}"'.format(cadena_caracteres, cadena_caracteres[-4]))


+-------+------+------+------+------+------+------+------+------+------+
| H     | o    | l    | a    |      | m    | u    | n    | d    | o    |
+=======+======+======+======+======+======+======+======+======+======+
| 0     | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    |
+-------+------+------+------+------+------+------+------+------+------+
| -10   | -9   | -8   | -7   | -6   | -5   | -4   | -3   | -2   | -1   |
+-------+------+------+------+------+------+------+------+------+------+

Lo que no se puede hacer es cambiar sólo una letra de un string:

.. activecode:: py_20
    :nocodelens:

    cadena_caracteres = 'Hola mundo'
    cadena_caracteres[6] = 'x'


Aunque a veces lo que queremos es una parte del string, no todo:

.. activecode:: py_21
    :nocodelens:

    cadena_caracteres = 'Hola mundo'
    print(cadena_caracteres)
    print(cadena_caracteres[3])
    print(cadena_caracteres[2:8])     # Con los dos índices positivos
    print(cadena_caracteres[2:-2])    # Con un índice negativo y otro positivo
    print(cadena_caracteres[-8:8])    # Con un índice negativo y otro positivo
    print(cadena_caracteres[-8:-2])   # Con ambos índices negativos
    print(cadena_caracteres[2:-2:3])  # Y salteándose de a dos


Aunque lo más común es quitar el último carácter, por ejemplo, cuando es
un Enter:

.. activecode:: py_22
    :nocodelens:

    cadena_caracteres = 'Hola mundo\n'
    print(cadena_caracteres)
    print(cadena_caracteres[:-1])
    print(cadena_caracteres[:-5])


Ingreso de datos desde teclado
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. activecode:: py_23
    :nocodelens:

    numero = input('Ingrese un número: ')
    print(numero)
    print(type(numero))


Y para convertirlo como entero:

.. activecode:: py_24
    :nocodelens:

    numero = int(input('Ingrese un número: '))
    print(numero)
    print(type(numero))


None
~~~~

None es el tipo de dato nulo que sólo puede tomar un valor: None. Aunque
parezca que es muy inútil, en realidad se usa mucho.

.. raw:: html

   <!--
   ## Mutables vs Inmutables

   En algunas ocasiones 

   -->

Estructuras de control selectivas
=================================

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


Cualquier tipo de dato se lo puede evaluar como booleano. Se toma como
falso a: \* None \* False para los bool \* cero para todo tipo de dato
numérico: 0, 0L, 0.0, 0j \* vacío para cualquier secuencia o
diccionario: '', (), [], {}

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


short-if
--------

Otra forma de escribir el if en una sola línea es poner:

.. code:: python

    variable = valor1 if condicion else valor2

Por ejemplo:

.. activecode:: py_32
    :nocodelens:

    num = 5
    es_par = True if (num % 2 == 0) else False
    print('5 es par?:', es_par)
    
    num = 6
    es_par = True if (num % 2 == 0) else False
    
    print('6 es par?:', es_par)


.. activecode:: py_33
    :nocodelens:

    nulo = None
    print(nulo)
    print(type(nulo))



Ejercicios
==========

1.  Teniendo en dos variables la base y la altura de un rectángulo,
    calcular el perímetro y la superficie.
2.  Dados dos números, imprimir:
 a. La suma de ambos
 b. La diferencia (el mayor menos el menor)
 c. La multiplicación
 d. La división
3.  Escribir un algoritmo que determine si un número N es divisible por
    M, siendo N y M dos variables del programa.
4.  Pasar un período expresado en segundos a un período expresado en
    días, horas, minutos y segundos.
5.  Dada la distancia entre dos puntos y las horas de partida y de
    llegada de un movil, expresadas en horas, minutos y segundos,
    calcular su velocidad promedio.
6.  La relación entre temperaturas Celsius y Fahrenheit está dada por:

    .. math:: C = 5/9 * (F-32)

    Escribir un algoritmo que le pida al usuario:
 a. la temperatura
 b. la unidad en la que se encuentra
 c. y luego mostrar la temperatura convertida en la otra unidad.
