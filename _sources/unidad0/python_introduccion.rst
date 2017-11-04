Python Intro
============

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


+-------------+-------------------------------+--------------------------------+
|             | **Compilado**                 | **Interpretado**               |
|             |                               |                                |
+=============+===============================+================================+
| Velocidad   | Lento, hay que compilar cada  | Rápido, se modifica el         |
| de          | vez y es una tarea que puede  | código y se vuelve a probar.   |
| desarrollo  | tardar varios minutos         | A veces, ni siquiera           |
|             |                               | requiere reiniciar el programa |
+-------------+-------------------------------+--------------------------------+
| Velocidad   | Rápido, se compila una única  | Lento, es necesario leer,      |
| de          | vez todo el programa y el     | interpretar y traducir el      |
| ejecución   | ejecutable generado ya lo     | código mientras el programa    |
|             | entiende la máquina           | está corriendo                 |
+-------------+-------------------------------+--------------------------------+
| Dependencia | Si, siempre que se genera un  | No, con instalar el intérprete |
| de la       | ejecutable es para una        | en la computadora que se       |
| plataforma  | arquitectura en particular.   | quiere correr el programa es   |
|             | Por ejemplo, para Windows de  | suficiente                     |
|             | 32 bits, linux 64 bits, etc.  |                                |
+-------------+-------------------------------+--------------------------------+
| Dependencia | No, una vez que se compilo no | Si, siempre que se quiera      |
| del         | es necesarioinstalar el       | correr el programa es          |
| lenguaje    | compilador para ejecutar el   | necesario instalar el          |
|             | programa                      | intérprete                     |
+-------------+-------------------------------+--------------------------------+

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
tenían dos alternativas, pero ninguna cerraba a la perfección:

* *Bash:* lenguaje de scripting (es el que usa la consola de linux como
  intérprete) y en este contexto se quedaba corto y complicaba la solución
* *C:* lenguaje estructurado con características de bajo, mediano y
  alto nivel; pero que en estas circunstancias era demasiado. Era como
  matar un mosquito con cañón.

Ante esta situación, e influido por el lenguaje ABC del cual había
participado, es que decidió crear Python como un lenguaje intermedio
entre bash y C que tiene las siguientes características:

* Extensible (se le pueden agregar módulos en C y Python)
* Multiplataforma (Amoeba OS, Unix, Windows y Mac)
* Sintaxis simple, clara y sencilla
* Fuertemente tipado
* Tipado dinámico
* Gran librería estándar
* Introspección

Filosofia de Python
~~~~~~~~~~~~~~~~~~~

Dentro de lo que es el *Zen de Python* están escritas varias reglas que
debería seguir todo código escrito en Python. Algunas de ellas son:

* Bello es mejor que feo
* **Explícito es mejor que implícito**
* Simple es mejor que complejo
* Complejo es mejor que complicado
* **La legibilidad cuenta**
* Los casos especiales no son tan especiales como para quebrantar las reglas
* Aunque lo práctico le gana a la pureza
* **Si la implementación es difícil de explicar, es una mala idea**

