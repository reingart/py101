
.. raw:: html

   <!--
   17/11
   Introducción a la de programación orientada a objetos. Uso de objetos dados.
   -->

Programación Orientada a Objetos (POO)
======================================

¿Qué es un objeto?
------------------

Comencemos por definir ¿qué es un objeto?. Según la RAE, un objeto es
una *cosa*. Y si vamos a la definición de cosa de la RAE, veremos que
dice > *Lo que tiene entidad, ya sea corporal o espiritual, natural o
artificial, concreta, abstracta o virtual*.

O sea, a todo lo que nos rodea que tiene entidad, se lo puede considerar
un objeto. Y cada uno de esos objetos tienen distintas características,
como pueden ser el color, tamaño, peso, etc. Y a su vez, la forma que
tendremos para interactuar con esos objetos, o lo que nos permite hacer
cada uno de ellos, será distinto.

POO
---

La programacion orientada a objetos es un paradigma de programación que
se basa en el concepto de objetos para representar la realidad. Es
imporante destacar que es ***una*** forma de representar la realidad
para poder trabajar con esas abstracciones y hacer un algoritmo que
tenga un objetivo en particular. La POO junta en una misma estructura
las variables que sirven para describir las carácterísticas (variables)
de aquello que se esta modelando, junto con aquellas que determinan el
estado en que se encuentra (también variables) y las funciones que le
dan un comportamiento a dicha estructura. Por ejemplo, si queremos
modelar un curso de una materia, podemos crear distintos objetos, como
pueden ser los alumnos, los profesores y el curso que los contiene a
todos ellos. Los alumnos tendrán ciertas variables que los distingan
entre sí, como pueden ser el *padrón*, *nombre* y *apellido*. Y otras
que definan el estado en que se encuentra; como las notas de
*parciales*, *trabajos prácticos* y *coloquios*, que determinan si el
alumno: *Recurso*, *Esta en condiciones de rendir coloquio* o *Aprobó*.
Y las funciones que definen su comportamiento pueden ser *rendir exámen*
o *entregar trabajo práctico*\  A todas esas variables que componen el
objeto se las llaman **atributos** y las funciones que determinan su
comportamiento se las llama **métodos**.

Clases y objetos
----------------

Así como en la programación estructurada tenemos el concepto de tipo de
dato y valores, en objetos tenemos los conceptos de **clases**, que es
algo abstracto que define las características y comportamientos de un
objeto (como eran los tipos de datos), y **objetos**, que son una
instancia de esa clase. Por ejemplo, todos sabemos a qué nos referimos
cuando hablamos de una mesa, y si vamos a la definición de la RAE
encontraremos:

    *Mueble compuesto de un tablero horizontal liso y sostenido a la
    altura conveniente, generalmente por una o varias patas, para
    diferentes usos, como escribir, comer, etc.*

Eso, vendría a ser una clase, es sólo la idea abstracta. Pero después,
la mesa que puede tener cada uno en su casa es distinta, y esas serían
las distintas instancias de la clase Mesa. |image0|

A su vez, cada mesa es un objeto distinto, por más que sean todas de la
misma clase. Y cada uno de esos objetos, puede estar compuesto por otros
objetos, como pueden ser una tabla y una o varias patas.

POO en python
-------------

En realidad, en Python todo es un objeto. Los strings, por ejemplo, son
objetos de la clase
`str <https://docs.python.org/2/library/functions.html#str>`__. Y tienen
`los
métodos <https://docs.python.org/2/library/stdtypes.html#string-methods>`__
upper, capitalize, center, expandtabs, etc. Para crear un objeto de una
en particular lo que tenemos que hacer es invocar a la clase poniendo su
nombre seguido de paréntesis. Por ejemplo:

.. code:: python

    mi_string = str()
    mi_lista = list()

Y para invocar uno de sus métodos sólo es necesario usar una variable la
clase en cuestión, poner un punto, y el nombre de un método seguido por
paréntesis:

.. code:: python

    en_mayusculas = mi_string.upper()

Creando nuestras propias clases
-------------------------------

Pero más allá de las clases estándares que nos provee Python, también
podemos crear nuestras propias clases. Y para eso usamos la palabra
reservada *class*.

.. code:: python

    class Mesa(object):
        pass

Ahora, esa mesa puede tener distintas características, como pueden ser
la cantidad de patas, el color o el material del que están hechas:

.. code:: python

    class Mesa(object):
        cantidad_de_patas = None
        color = None
        material = None

Entonces, cuando quiera usar esa idea abstracta voy a tener que definir
esas características:

.. |image0| image:: mesas.png

.. code:: python

    class Mesa(object):
        cantidad_de_patas = None
        color = None
        material = None
        
    mi_mesa = Mesa()
    mi_mesa.cantidad_de_patas = 4
    mi_mesa.color = 'Marrón'
    mi_mesa.material = 'Madera'
    
    print 'Tendo una mesa de {0.cantidad_de_patas} patas de color {0.color} y esta hecha de {0.material}'.format(mi_mesa)


.. parsed-literal::

    Tendo una mesa de 4 patas de color Marrón y esta hecha de Madera


Ahora, si siempre voy a tener que definir esas características de la
mesa para poder usarla, lo más cómodo es definir el método ``__init__``
que sirve para inicializar el objeto:

.. code:: python

    class Mesa(object):
        cantidad_de_patas = None
        color = None
        material = None
        
        def __init__(self, patas, color, material):
            self.cantidad_de_patas = patas
            self.color = color
            self.material = material
        
    mi_mesa = Mesa(4, 'Marrón', 'Madera')
    
    print 'Tendo una mesa de {0.cantidad_de_patas} patas de color {0.color} y esta hecha de {0.material}'.format(mi_mesa)


.. parsed-literal::

    Tendo una mesa de 4 patas de color Marrón y esta hecha de Madera


Como vemos, el método ``__init__`` (aunque en realidad pasará lo mismo
con casi todos los métodos de la clase), recibe como primer parámetro
uno que se llama **self**. En realidad el nombre no tiene por qué ser
ese, pero se suele usar por convención. La traducción de *self* es *uno
mismo*, y con eso quieren decir que en el primer parámetro que Python
siempre será el mismo objeto (la instancia) del cual están ejecutando el
método. Si bien self aparece entre los parámetros formales, no se ve
entre los parámetros actuales, y eso es porque lo inserta el interprete
automáticamente. No tiene que hacerlo uno mismo. Así como este objeto
esta compuesto por tres objetos estándar de Python (un *int* y dos
*str*), también podría estar compuesto por objetos creados por nosotros:

.. code:: python

    class TablaRectangular(object):
        base = None
        altura = None
        
        def __init__(self, base, altura):
            self.base = base
            self.altura = altura
    
    
    class TablaRedonda(object):
        radio = None
        
        def __init__(self, radio):
            self.radio = radio
    
    class Pata(object):
        altura = None
        
        def __init__(self, altura):
            self.altura = altura
            
    class Mesa(object):
        tabla = None
        patas = None
        
        def __init__(self, tabla, patas):
            self.tabla = tabla
            self.patas = patas
    
    tabla = TablaRectangular(100, 150)
    pata_1 = Pata(90)
    pata_2 = Pata(90)
    pata_3 = Pata(90)
    pata_4 = Pata(90)
    mi_mesa = Mesa(tabla, [pata_1, pata_2, pata_3, pata_4])

Y como dijimos antes, una objeto no sólo agrupa sus características,
sino también los métodos que nos permiten trabajar con él, como por
ejemplo, podría ser calcular su superficie de apoyo:

.. code:: python

    import math
    
    class TablaRectangular(object):
        base = None
        altura = None
        
        def __init__(self, base, altura):
            self.base = base
            self.altura = altura
            
        def calcular_superficie(self):
            return self.base * self.altura
    
    
    class TablaRedonda(object):
        radio = None
        
        def __init__(self, radio):
            self.radio = radio
            
        def calcular_superficie(self):
            return math.pi * self.radio**2
    
    class Pata(object):
        altura = None
        
        def __init__(self, altura):
            self.altura = altura
            
    class Mesa(object):
        tabla = None
        patas = None
        
        def __init__(self, tabla, patas):
            self.tabla = tabla
            self.patas = patas
    
        def obtener_superficie_de_apoyo(self):
            return self.tabla.calcular_superficie()
            
    tabla = TablaRectangular(100, 150)
    pata_1 = Pata(90)
    pata_2 = Pata(90)
    pata_3 = Pata(90)
    pata_4 = Pata(90)
    mi_mesa = Mesa(tabla, [pata_1, pata_2, pata_3, pata_4])
    
    sup = mi_mesa.obtener_superficie_de_apoyo()
    print 'La superficie de la mesa es {} cm2'.format(sup)


.. parsed-literal::

    La superficie de la mesa es 15000 cm2


En este caso, no sólo es importante ver cómo se hace para invocar un
método de un objeto (que es poniendo el nombre del objeto, un punto y el
nombre del método seguido por todos sus parámetros entre paréntesis)
sino también cómo se puede conjugar el uso de los objetos. En la función
``obtener_superficie_de_apoyo`` de la clase ``Mesa`` podemos ver que la
única responsabilidad que tiene ese objeto es redirigir la consulta que
se le hizo al objeto ``tabla``. Es decir, podía preguntárselo a
cualquiera de sus patas o a la tabla, pero sabía a quién tenía que
preguntarselo. Y no importa si es una tabla redonda o rectangular, las
dos clases saben cómo responder la pregunta de ``calcular_superficie``.

.. code:: python

        def obtener_superficie_de_apoyo(self):
            return self.tabla.calcular_superficie()

Otro ejemplo
------------

Volviendo un poco al ejemplo planteado antes de querer modelar una
materia, podríamos implementar los alumnos de la siguiente manera:

.. code:: python


    class Alumno(object):

        def __init__(self, padron, nombre, apellido):
            self.padron = padron
            self.nombre = nombre
            self.apellido = apellido
            self.parciales = []
            self.tps = []
            self.coloquios = []
        
        def rendir_parcial(self, nota):
            self.parciales.append(nota)
        
        def entregar_trabajo_practico(self, nota):
            self.tps.append(nota)
        
        def rendir_coloquio(self, nota):
            self.coloquios.append(nota)
            
        def aprobo_algun_parcial(self):
            aprobo_alguno = False
            for nota in self.parciales:
                if nota >= 4:
                    aprobo_alguno = True
            
            return aprobo_alguno
        
        def aprobo_todos_los_tp(self):
            aprobo_todos = True
            for nota in self.parciales:
                if nota < 4:
                    aprobo_todos = False
            
            return aprobo_todos
        
        def puede_rendir_coloquio(self):
            return self.aprobo_algun_parcial() and self.aprobo_todos_los_tp()

Después, para usa estas variables sólo es necesario definir una variable
de la clase ``Alumno`` pasandole los parametros necesarios para poder
inicializarlo:

.. code:: python

    alum = Alumno(12345, 'Juan', 'Perez')
    alum.rendir_parcial(2)
    alum.entregar_trabajo_practico(7)
    alum.rendir_parcial(7)
    alum.entregar_trabajo_practico(9)

    if alum.puede_rendir_coloquio():
        print 'El alumno puede rendir coloquio'
    else:
        print 'El alumno no puede rendor coloquio'

.. code:: python

    class Alumno(object):
    
        def __init__(self, padron, nombre, apellido):
            self.padron = padron
            self.nombre = nombre
            self.apellido = apellido
            self.parciales = []
            self.tps = []
            self.coloquios = []
        
        def rendir_parcial(self, nota):
            self.parciales.append(nota)
        
        def entregar_trabajo_practico(self, nota):
            self.tps.append(nota)
        
        def rendir_coloquio(self, nota):
            self.coloquios.append(nota)
            
        def aprobo_algun_parcial(self):
            aprobo_alguno = False
            for nota in self.parciales:
                if nota >= 4:
                    aprobo_alguno = True
    
            return aprobo_alguno
        
        def aprobo_todos_los_tp(self):
            aprobo_todos = True
            for nota in self.tps:
                if nota < 4:
                    aprobo_todos = False
            
            return aprobo_todos
        
        def puede_rendir_coloquio(self):
            return self.aprobo_algun_parcial() and self.aprobo_todos_los_tp()
        
    
    alum = Alumno(12345, 'Juan', 'Perez')
    alum.rendir_parcial(2)
    alum.entregar_trabajo_practico(7)
    alum.entregar_trabajo_practico(9)
    
    if alum.puede_rendir_coloquio():
        print 'El alumno puede rendir coloquio'
    else:
        print 'El alumno no puede rendor coloquio'
    
    print '¿Y si después rinde el parcial y se saca un 7?'
    alum.rendir_parcial(7)
    
    if alum.puede_rendir_coloquio():
        print 'El alumno puede rendir coloquio'
    else:
        print 'El alumno no puede rendor coloquio'


.. parsed-literal::

    El alumno no puede rendor coloquio
    ¿Y si después rinde el parcial y se saca un 7?
    El alumno puede rendir coloquio


