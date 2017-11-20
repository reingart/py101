
.. raw:: html

   <!--
   03/11
   Archivos binarios. Pickles.
   Apareo de archivos secuenciales.
   CLASE DE LABORATORIO 
   (Gonzalo)
   -->

Persistencia de datos
=====================

Pero todo lo que vimos por el momento se guarda en memoria dinámica, por
lo que al apagar la computadora, o simplemente con cerrar el programa y
volver a abrirlo perdimos todos los datos que nos teníamos. La
alternativa para esto siguen siendo los
`archivos <https://docs.python.org/2/library/stdtypes.html#bltin-file-objects>`__.

Apertura de archivos
--------------------

Al igual que en C, en Python en el mismo momento que abrimos el archivo,
se lo asignamos a uno físico y elegimos el modo de apertura, que si no
le indicamos nada, tomará por defecto el de *lectura*. El modo de
apertura puede ser cualquier combinación de:

-  **'r'** *Lectura*: el archivo debe existir. Similar al ``reset`` de
   Pascal.
-  **'w'** *Escritura*: no es necesario que el archivo exista, pero si
   existe lo sobre escribe. Similar al ``rewrite`` de Pascal.
-  **'a'** *Append*: Solo agrega al final y no es necesario que el
   archivo exista. Similar al ``append`` de Pascal.
-  **'t'** *Texto*: Archivo de texto
-  **'b'** *Binario*: Archivo binario
-  **'+'** \*Permite lectura y escrituras simultáneas

La primitiva del lenguaje para abrir y asignar un archivo es
`**open** <https://docs.python.org/2/library/functions.html#open>`__, la
cual puede recibir uno o dos parámetros. El primero es obligatorio, y
corresponde a la ubicación relativa o absoluta del archivo físico. El
segundo parámetro indica el modo de apertura y es opcional. Si no se lo
pasamos asumirá que lo queremos abrir en modo *Lectura*. Supongamos que
estamos usando el intérprete en un escenario en el que solo tenemos un
archivo que se llama f2.txt y queremos trabajar con los archivos f1.txt
y f2.txt.

.. code:: python

    >>> # Lanza una excepción de IOError por no existir el archivo e 
    >>> # intentar abrirlo en modo lectura.
    >>> file1 = open("f1.txt")  
    Traceback (most recent call last):
      File "<stdin>", line 1, in <module>
    IOError: [Errno 2] No such file or directory: 'f1.txt'
    >>> # Intento abrir el archivo f1.txt, pero en modo escritura,
    >>> # por lo crea y no falla. Si hubiera existido, lo hubiera 
    >>> # truncado y creado vacío.
    >>> file1 = open("f1.txt", "w")
    >>> # Abro el archivo f2.txt en modo lectura sin problemas, ya
    >>> # que éste si existe.
    >>> file2 = open("f2.txt")

Cerrar un archivo
-----------------

Para cerrar un archivo solo tenemos que indicarlo poniendo la variable
seguida de un punto y la primitiva
`**close** <https://docs.python.org/2/library/stdtypes.html#file.close>`__.
La única restricción es que la variable sea de tipo archivo, si cerramos
un archivo cerrado este sigue cerrado; y si cerramos uno abierto, el
mismo cambia de estado.

.. code:: python

    >>> file2 = open("f2.txt")  # Abro el archivo en modo lectura
    >>> file2.close()  # Cierro el archivo

Lectura de archivos
-------------------

Supongamos que tenemos un archivo llamado *ejemplo.txt* y tiene el
siguiente texto:

::

    Python was created in the early 1990s by Guido van Rossum at Stichting
    Mathematisch Centrum (CWI, see http://www.cwi.nl) in the Netherlands
    as a successor of a language called ABC.  Guido remains Python's
    principal author, although it includes many contributions from others.

    In 1995, Guido continued his work on Python at the Corporation for
    National Research Initiatives (CNRI, see http://www.cnri.reston.va.us)
    in Reston, Virginia where he released several versions of the
    software.

    In May 2000, Guido and the Python core development team moved to
    BeOpen.com to form the BeOpen PythonLabs team.  In October of the same
    year, the PythonLabs team moved to Digital Creations (now Zope
    Corporation, see http://www.zope.com).  In 2001, the Python Software
    Foundation (PSF, see http://www.python.org/psf/) was formed, a
    non-profit organization created specifically to own Python-related
    Intellectual Property.  Zope Corporation is a sponsoring member of
    the PSF.

    All Python releases are Open Source (see http://www.opensource.org for
    the Open Source Definition).  Historically, most, but not all, Python
    releases have also been GPL-compatible.

Para leer un archivo podemos usar la primitiva
`**read** <https://docs.python.org/2/library/stdtypes.html#file.read>`__,
la cual puede recibir un parámetro que indique la cantidad de caracteres
a leer. Si no se pasa ese parámetro el intérprete leerá todo el archivo
y lo retornará.

.. code:: python

    arch = open("ejemplo.txt")
    cadena = arch.read(15)
    print "# Imprimo los primeros 15 caracteres del archivo. Tiene que ser 'Python was crea'"
    print cadena
    
    print "# Leo otros 7 caracteres y dejo el cursor del archivo en la siguiente posición. Tiene que ser 'ted in '"
    cadena = arch.read(7)
    print cadena
    
    print "# Ahora leo el resto del archivo."
    cadena = arch.read()
    print cadena
    
    print '# Cierro el archivo'
    arch.close()


.. parsed-literal::

    # Imprimo los primeros 15 caracteres del archivo. Tiene que ser 'Python was crea'
    Python was crea
    # Leo otros 7 caracteres y dejo el cursor del archivo en la siguiente posición. Tiene que ser 'ted in '
    ted in 
    # Ahora leo el resto del archivo.
    the early 1990s by Guido van Rossum at Stichting
    Mathematisch Centrum (CWI, see http://www.cwi.nl) in the Netherlands
    as a successor of a language called ABC.  Guido remains Python's
    principal author, although it includes many contributions from others.
    
    In 1995, Guido continued his work on Python at the Corporation for
    National Research Initiatives (CNRI, see http://www.cnri.reston.va.us)
    in Reston, Virginia where he released several versions of the
    software.
    
    In May 2000, Guido and the Python core development team moved to
    BeOpen.com to form the BeOpen PythonLabs team.  In October of the same
    year, the PythonLabs team moved to Digital Creations (now Zope
    Corporation, see http://www.zope.com).  In 2001, the Python Software
    Foundation (PSF, see http://www.python.org/psf/) was formed, a
    non-profit organization created specifically to own Python-related
    Intellectual Property.  Zope Corporation is a sponsoring member of
    the PSF.
    
    All Python releases are Open Source (see http://www.opensource.org for
    the Open Source Definition).  Historically, most, but not all, Python
    releases have also been GPL-compatible.
    
    # Cierro el archivo


La única condición que tenemos para usar este método es que el archivo
lo hayamos abierto en modo lectura.

.. code:: python

    arch2 = open("ejemplo2.txt", "w")
    arch2.read()


::


    ---------------------------------------------------------------------------

    IOError                                   Traceback (most recent call last)

    <ipython-input-17-14fdc854ce4e> in <module>()
          1 arch2 = open("ejemplo2.txt", "w")
    ----> 2 arch2.read()
    

    IOError: File not open for reading


.. code:: python

    # Y si intentamos con un append?
    arch3 = open("ejemplo1.txt", "a")
    arch3.read()


::


    ---------------------------------------------------------------------------

    IOError                                   Traceback (most recent call last)

    <ipython-input-18-2ccb79e17cdc> in <module>()
          1 # Y si intentamos con un append?
          2 arch3 = open("ejemplo1.txt", "a")
    ----> 3 arch3.read()
    

    IOError: File not open for reading


Otra primitiva que podemos usar es
`**readline** <https://docs.python.org/2/library/stdtypes.html#file.readline>`__,
que al igual que
`**read** <https://docs.python.org/2/library/stdtypes.html#file.read>`__,
también puede recibir un parámetro que indique la cantidad máxima de
bytes a leer. Si no se le pasa ningún parámetro, lee toda la línea.

.. code:: python

    arch = open("ejemplo.txt")
    linea = arch.readline()  # Notar que también imprime el Enter o \n
    print linea
    linea = arch.readline(7)  # La segunda línea es 'Mathematisch Centrum (CWI, see http://www.cwi.nl) in the Netherlands'
    print linea
    arch.close()


.. parsed-literal::

    Python was created in the early 1990s by Guido van Rossum at Stichting
    
    Mathema


Pero no es necesario que leamos de a una sola línea, sino que también
podemos leer todas las líneas del archivo y guardarlas en una lista
haciendo uso de la primitiva
`**readlines** <https://docs.python.org/2/library/stdtypes.html#file.readlines>`__.

.. code:: python

    arch = open("ejemplo.txt")
    lineas = arch.readlines()
    print lineas
    arch.close()


.. parsed-literal::

    ['Python was created in the early 1990s by Guido van Rossum at Stichting\n', 'Mathematisch Centrum (CWI, see http://www.cwi.nl) in the Netherlands\n', "as a successor of a language called ABC.  Guido remains Python's\n", 'principal author, although it includes many contributions from others.\n', '\n', 'In 1995, Guido continued his work on Python at the Corporation for\n', 'National Research Initiatives (CNRI, see http://www.cnri.reston.va.us)\n', 'in Reston, Virginia where he released several versions of the\n', 'software.\n', '\n', 'In May 2000, Guido and the Python core development team moved to\n', 'BeOpen.com to form the BeOpen PythonLabs team.  In October of the same\n', 'year, the PythonLabs team moved to Digital Creations (now Zope\n', 'Corporation, see http://www.zope.com).  In 2001, the Python Software\n', 'Foundation (PSF, see http://www.python.org/psf/) was formed, a\n', 'non-profit organization created specifically to own Python-related\n', 'Intellectual Property.  Zope Corporation is a sponsoring member of\n', 'the PSF.\n', '\n', 'All Python releases are Open Source (see http://www.opensource.org for\n', 'the Open Source Definition).  Historically, most, but not all, Python\n', 'releases have also been GPL-compatible.\n']


Sin embargo, la forma más *Pythonic* de leer el archivo por líneas es
usando la estructura **for** y quedaría casi como lo diríamos en
castellano: *"Para cada línea del archivo*. Por ejemplo, si queremos
imprimir la cantidad de caracteres de cada línea podríamos hacer:

.. code:: python

    arch = open("ejemplo.txt")
    for linea in arch:
        print len(linea)
    
    arch.close()


.. parsed-literal::

    71
    69
    65
    71
    1
    67
    71
    62
    10
    1
    65
    71
    63
    69
    63
    67
    67
    9
    1
    71
    70
    40


Escritura de archivos
---------------------

Para escribir en un archivo podemos usar las las primitivas
`**write(string)** <https://docs.python.org/2/library/stdtypes.html#file.write>`__
y
`**writelines(lista\_strings)** <https://docs.python.org/2/library/stdtypes.html#file.writelines>`__,
que la primera es para escribir una cadena de caracteres y la segunda
para escribir una lista de strings, uno a continuación del otro. Es
importante destacar que en ningún caso se escribe algún carácter que no
figure en los strings, como por ejemplo, caracteres de fin de línea. El
uso de **writelines** es equivalente a recorrer la lista y hacerle un
**write** a cada elemento. Pero el costo de escribir algo en el disco es
mucho mayor a escribirlo en memoria por lo que, al igual que en C, se
usa un *buffer*, que no es más que una porción de memoria para ir
guardando en forma temporal los datos y cuando alcanzan un tamaño
considerable se lo manda a escribir al disco. Otra forma de asegurarse
que se haga la escritura es usando la primitiva *flush*, la cual guarda
en el disco el contenido del buffer y lo vacía.

.. code:: python

    arch2 = open("ejemplo2.txt", "w")
    arch2.write("Es la primer cadena")
    arch2.write("Seguida de la segunda con un fin de linea\n")
    arch2.writelines(["1. Primero de la lista sin fin de línea. ", "2. Segundo string con fin de línea.\n", "3. Tercero con\\n.\n", "4. y último."])
    arch2.flush()
    arch2.close()
    arch2 = open("ejemplo2.txt", "r+a")
    strfile = arch2.read()
    print strfile


.. parsed-literal::

    Es la primer cadenaSeguida de la segunda con un fin de linea
    1. Primero de la lista sin fin de línea. 2. Segundo string con fin de línea.
    3. Tercero con\n.
    4. y último.


¿Y qué pasa si le quiero agregar algunas líneas a este archivo?

.. code:: python

    arch2.write("Esto lo estoy agregando.\n.")
    arch2.writelines("Y estas dos líneas también con un \\n al final\n de cada una.\n")
    arch2.flush()
    arch2 = open("ejemplo2.txt", "r")  # El open hace que me mueva a la primer posición del archivo.
    print arch2.read()
    arch2.close()



.. parsed-literal::

    Es la primer cadenaSeguida de la segunda con un fin de linea
    1. Primero de la lista sin fin de línea. 2. Segundo string con fin de línea.
    3. Tercero con\n.
    4. y último.Esto lo estoy agregando.
    .Y estas dos líneas también con un \n al final
     de cada una.
    


Otra forma de asegurarse que se escriba lo que hay en el disco es
cerrándolo.

Moverse en un archivo
---------------------

Al igual que en los archivos binarios de *Pascal*, en *Python* también
podemos saltar a distintas posiciones mediante la primitiva
`**seek(pos)** <https://docs.python.org/2/library/stdtypes.html#file.seek>`__
la cual recibe, como mínimo un parámetro que indica la posición a la que
nos queremos mover. Opcionalmente puede recibir un segundo parámetro: \*
**0:** La posición es desde el inicio del archivo y debe ser mayor o
igual a 0 \* **1:** La posición es relativa a la posición actual; puede
ser positiva o negativa \* **2:** La posición es desde el final del
archivo, por lo que debe ser negativa

.. code:: python

    arch = open("ejemplo.txt")  
    arch.seek(30)        # Voy a la posición número 30 del archivo
    print arch.read(7)   # Debería salir 'y 1990s'
    arch.seek(-5,1)      # Me muevo 5 posiciones para atrás desde mi posición actual.
    print arch.read(7)   # Debería imprimir '1990s b'
    arch.seek(-12,2)     # Me muevo a la posición número 12, comenzando a contar desde el final.
    print arch.read(10)  # Debería imprimir 'compatible'
    
    arch.close()


.. parsed-literal::

    y 1990s
    1990s b
    compatible


Y así como podemos movernos en un archivo, también podemos averiguar
nuestra posición usando la primitiva
`**tell()** <https://docs.python.org/2/library/stdtypes.html#file.tell>`__.

.. code:: python

    arch = open("ejemplo.txt")  
    arch.seek(30)
    print arch.tell()    # Debería imprimir 30
    arch.seek(-5,1)      # Retrocedo 5 posiciones
    print arch.tell()    # Debería imprimir 25
    arch.seek(-12,2)     # Voy a 12 posiciones antes del fin de archivo
    print arch.tell()    # Debería imprimir 1132
    print arch.read(10)  # Leo 10 caracteres
    print arch.tell()    # Debería imprimir 1142



.. parsed-literal::

    30
    25
    1132
    compatible
    1142


¿Cómo recorrer todo un archivo?
-------------------------------

Cuando llegamos al final de un archivo de texto usando la función *read*
o *readline* Python no arroja ningún valor, pero tampoco retorna ningún
caracter, por lo que podríamos usar eso como condición de corte:

.. code:: python

    arch = open("ejemplo.txt")  
    
    # El archivo ejemplo.txt tiene 22 líneas, por lo que
    # si quiero imprimirlo completo anteponiendo el 
    # número de línea y la cantidad de caracteres
    # puedo hacer:
    
    for x in range(1, 25):
        linea = arch.readline()
        print '{:2}[{:02}] - {}'.format(x, len(linea), linea)
    
    arch.close()


.. parsed-literal::

     1[71] - Python was created in the early 1990s by Guido van Rossum at Stichting
    
     2[69] - Mathematisch Centrum (CWI, see http://www.cwi.nl) in the Netherlands
    
     3[65] - as a successor of a language called ABC.  Guido remains Python's
    
     4[71] - principal author, although it includes many contributions from others.
    
     5[01] - 
    
     6[67] - In 1995, Guido continued his work on Python at the Corporation for
    
     7[71] - National Research Initiatives (CNRI, see http://www.cnri.reston.va.us)
    
     8[62] - in Reston, Virginia where he released several versions of the
    
     9[10] - software.
    
    10[01] - 
    
    11[65] - In May 2000, Guido and the Python core development team moved to
    
    12[71] - BeOpen.com to form the BeOpen PythonLabs team.  In October of the same
    
    13[63] - year, the PythonLabs team moved to Digital Creations (now Zope
    
    14[69] - Corporation, see http://www.zope.com).  In 2001, the Python Software
    
    15[63] - Foundation (PSF, see http://www.python.org/psf/) was formed, a
    
    16[67] - non-profit organization created specifically to own Python-related
    
    17[67] - Intellectual Property.  Zope Corporation is a sponsoring member of
    
    18[09] - the PSF.
    
    19[01] - 
    
    20[71] - All Python releases are Open Source (see http://www.opensource.org for
    
    21[70] - the Open Source Definition).  Historically, most, but not all, Python
    
    22[40] - releases have also been GPL-compatible.
    
    23[00] - 
    24[00] - 


Como pueden ver, todas las líneas hasta la 22 (que es la última linea
del arhcivo) tienen una longitud mayor a 0; incluso las 5, 10 y 19 que
aparentemente no tienen ningún caracter. Eso es así ya que siempre
tienen por lo menos uno, que es el Enter o ``\n``. Otra cosa a tener en
cuenta es que, por más que intentamos leer más allá del fin de archivo,
en ningún momento el interprete nos lanzó una excepción. Por lo tanto,
si no sabemos la longitud del archivo como era este caso, podríamos usar
esta información para darnos cuenta cuándo dejar de leer:

.. code:: python

    arch = open("ejemplo.txt")  
    
    # Si no sabemos la cantidad de líneas que tiene 
    # el archivo que queremos recorrer podemos hacer:
    
    linea = arch.readline()
    x = 0
    
    while linea:  # Es decir, mientras me devuelva algo 
                  # distinto al sting vacío
        x += 1
        print '{:2}[{:02}] - {}'.format(x, len(linea), linea)
        linea = arch.readline()
    
    arch.close()


.. parsed-literal::

     1[71] - Python was created in the early 1990s by Guido van Rossum at Stichting
    
     2[69] - Mathematisch Centrum (CWI, see http://www.cwi.nl) in the Netherlands
    
     3[65] - as a successor of a language called ABC.  Guido remains Python's
    
     4[71] - principal author, although it includes many contributions from others.
    
     5[01] - 
    
     6[67] - In 1995, Guido continued his work on Python at the Corporation for
    
     7[71] - National Research Initiatives (CNRI, see http://www.cnri.reston.va.us)
    
     8[62] - in Reston, Virginia where he released several versions of the
    
     9[10] - software.
    
    10[01] - 
    
    11[65] - In May 2000, Guido and the Python core development team moved to
    
    12[71] - BeOpen.com to form the BeOpen PythonLabs team.  In October of the same
    
    13[63] - year, the PythonLabs team moved to Digital Creations (now Zope
    
    14[69] - Corporation, see http://www.zope.com).  In 2001, the Python Software
    
    15[63] - Foundation (PSF, see http://www.python.org/psf/) was formed, a
    
    16[67] - non-profit organization created specifically to own Python-related
    
    17[67] - Intellectual Property.  Zope Corporation is a sponsoring member of
    
    18[09] - the PSF.
    
    19[01] - 
    
    20[71] - All Python releases are Open Source (see http://www.opensource.org for
    
    21[70] - the Open Source Definition).  Historically, most, but not all, Python
    
    22[40] - releases have also been GPL-compatible.
    


Aunque Python también nos ofrece otra forma de recorer un archivo, y es
usando una de las estructuras que ya conocemos: **for**

.. code:: python

    arch = open("ejemplo.txt")  
    
    # Si no sabemos la cantidad de líneas que tiene 
    # el archivo que queremos recorrer podemos hacer:
    
    x = 0
    for linea in arch:
        x += 1
        print '{:2}[{:02}] - {}'.format(x, len(linea), linea)
    
    arch.close()



.. parsed-literal::

     1[71] - Python was created in the early 1990s by Guido van Rossum at Stichting
    
     2[69] - Mathematisch Centrum (CWI, see http://www.cwi.nl) in the Netherlands
    
     3[65] - as a successor of a language called ABC.  Guido remains Python's
    
     4[71] - principal author, although it includes many contributions from others.
    
     5[01] - 
    
     6[67] - In 1995, Guido continued his work on Python at the Corporation for
    
     7[71] - National Research Initiatives (CNRI, see http://www.cnri.reston.va.us)
    
     8[62] - in Reston, Virginia where he released several versions of the
    
     9[10] - software.
    
    10[01] - 
    
    11[65] - In May 2000, Guido and the Python core development team moved to
    
    12[71] - BeOpen.com to form the BeOpen PythonLabs team.  In October of the same
    
    13[63] - year, the PythonLabs team moved to Digital Creations (now Zope
    
    14[69] - Corporation, see http://www.zope.com).  In 2001, the Python Software
    
    15[63] - Foundation (PSF, see http://www.python.org/psf/) was formed, a
    
    16[67] - non-profit organization created specifically to own Python-related
    
    17[67] - Intellectual Property.  Zope Corporation is a sponsoring member of
    
    18[09] - the PSF.
    
    19[01] - 
    
    20[71] - All Python releases are Open Source (see http://www.opensource.org for
    
    21[70] - the Open Source Definition).  Historically, most, but not all, Python
    
    22[40] - releases have also been GPL-compatible.
    


O, incluso, usar enumerate para saber qué línea estoy leyendo:

.. code:: python

    arch = open("ejemplo.txt")  
    
    # Si no sabemos la cantidad de líneas que tiene 
    # el archivo que queremos recorrer podemos hacer:
    
    # Usando enumerate y comenzando en 1
    for x, linea in enumerate(arch, 1):
        print '{:2}[{:02}] - {}'.format(x, len(linea), linea)
    
    arch.close()



.. parsed-literal::

     1[71] - Python was created in the early 1990s by Guido van Rossum at Stichting
    
     2[69] - Mathematisch Centrum (CWI, see http://www.cwi.nl) in the Netherlands
    
     3[65] - as a successor of a language called ABC.  Guido remains Python's
    
     4[71] - principal author, although it includes many contributions from others.
    
     5[01] - 
    
     6[67] - In 1995, Guido continued his work on Python at the Corporation for
    
     7[71] - National Research Initiatives (CNRI, see http://www.cnri.reston.va.us)
    
     8[62] - in Reston, Virginia where he released several versions of the
    
     9[10] - software.
    
    10[01] - 
    
    11[65] - In May 2000, Guido and the Python core development team moved to
    
    12[71] - BeOpen.com to form the BeOpen PythonLabs team.  In October of the same
    
    13[63] - year, the PythonLabs team moved to Digital Creations (now Zope
    
    14[69] - Corporation, see http://www.zope.com).  In 2001, the Python Software
    
    15[63] - Foundation (PSF, see http://www.python.org/psf/) was formed, a
    
    16[67] - non-profit organization created specifically to own Python-related
    
    17[67] - Intellectual Property.  Zope Corporation is a sponsoring member of
    
    18[09] - the PSF.
    
    19[01] - 
    
    20[71] - All Python releases are Open Source (see http://www.opensource.org for
    
    21[70] - the Open Source Definition).  Historically, most, but not all, Python
    
    22[40] - releases have also been GPL-compatible.
    


Ejercicios
----------

4.  Escribir un programa que reciba un nombre de archivo al ejecutarse,
    lo procese e imprima por pantalla cuántas líneas, cuantas palabras y
    la cantidad de caracteres tiene.
5.  Escribir un programa que reciba un nombre de archivo al ejecutarse,
    lo procese e imprima por pantalla un diccionario con la cantidad de
    ocurrencias de cada palabra (no distinguir mayúsculas y minúsculas).
    Además, se pide mostrar la palabra que más veces se repitió y
    cuántas ocurrencias tuvo.
6.  Escribir un programa que reciba un nombre de archivo y una palabra.
    Luego, deberá mostrar todas las líneas de ese archivo que contengan
    esa palabra. Si ninguna línea contiene esa palabra no mostrará nada.
7.  Leer un archivo de texto llamado ``curso.csv`` en el que cada línea
    tendrá el siguiente formato:

    ::

        padron,nombre,apellido,nota_parcial,nombre_de_grupo,nota_tp1,nota_tp2

    .. raw:: html

       <!--
       Puede ocurrir que algunas líneas no cuenten con todos los campos, o que los campos numéricos no sean números, o que no pertenezcan al rango de 0 a 10. En dichos casos se deberán guardar esas líneas para mostrarlas una vez leído todo el archivo indicando que tienen algún error (no es necesario especificar cuál es el error). <br>
       -->

    Suponiendo que todas las líneas tendrán el formato esperado y datos
    válidos, se pide:
8.  Imprimir por pantalla un listado de todos los alumnos en condiciones
    de rendir coloquio (parcial y todos los TP aprobados) en el mismo
    orden en el que se encontraban en el archivo.
9.  Imprimir por pantalla un listado de todos los alumnos en condiciones
    de rendir coloquio (parcial y todos los TP aprobados) ordenados por
    padrón en forma creciente.
10. Calcular para cada alumno el promedio de sus notas del parcial y
    luego el promedio del curso como el promedio de todos los promedios.
11. Informar cuál es la nota que más se repite entre todos los parciales
    e indicar la cantidad de ocurrencias.
12. Listar todas las notas que se sacaron los alumnos en el parcial y
    los padrones de quienes se sacaron esas notas con el siguiente
    formato:

``Nota: 2   * nnnn1   * nnnn2   * nnnn3   * nnnn4 Nota: 4   * nnnn1   * nnnn2   ...``
Tener en cuenta que las notas pueden ser del 2 al 10 y puede ocurrir que
nadie se haya sacado esa nota (y en dicho caso esa nota no tiene que
aparecer en el listado)

Procesamiento de archivos
=========================

Por lo general, cuando se trabaja con un archivo se hacen tres
operaciones seguidas:

1. Abrir el archivo
2. Procesar el archivo
3. Cerrar el archivo

Y hay que tener cuidado, porque si ocurre algún error con el archivo en
algún punto de su procesamiento es necesario encargarse de cerrarlo,
antes de que la excepción siga subiendo niveles.

Trabajando con archivo de una forma segura
------------------------------------------

Para trabajar con los archivos de una forma más simple es que se agregó
la sentencia **with** que define un contexto dentro del cual nos asegura
que, ocurra una excepción o no, el archivo se cerrará al momento de
salir de ese contexto:

.. code:: python

    try:
        with open('ejemplo.txt') as fd:
            print '¿El archivo se encuentra cerrado?', fd.closed
            a += 2  # Como la variable a no existe, va a tirar
                    # una excepción del tipo NameError
            print 'Estas líneas nunca se van a mostrar porque'
            print 'antes va a ocurrir un error'
    except NameError:
        print 'Ocurrio un error'
        
    print '¿El archivo se encuentra cerrado?', fd.closed


.. parsed-literal::

    ¿El archivo se encuentra cerrado? False
    Ocurrio un error
    ¿El archivo se encuentra cerrado? True


.. code:: python

    with open('ejemplo.txt', 'r') as archivo:
        print '¿El archivo se encuentra cerrado?: {}'.format(archivo.closed)
        print
        for linea in archivo:
            longitud = len(linea[:-1])
            print '{:2}: {}'.format(longitud, linea[:-1])
    
    print
    print '¿El archivo se encuentra cerrado?: {}'.format(archivo.closed)


.. parsed-literal::

    ¿El archivo se encuentra cerrado?: False
    
    70: Python was created in the early 1990s by Guido van Rossum at Stichting
    68: Mathematisch Centrum (CWI, see http://www.cwi.nl) in the Netherlands
    64: as a successor of a language called ABC.  Guido remains Python's
    70: principal author, although it includes many contributions from others.
     0: 
    66: In 1995, Guido continued his work on Python at the Corporation for
    70: National Research Initiatives (CNRI, see http://www.cnri.reston.va.us)
    61: in Reston, Virginia where he released several versions of the
     9: software.
     0: 
    64: In May 2000, Guido and the Python core development team moved to
    70: BeOpen.com to form the BeOpen PythonLabs team.  In October of the same
    62: year, the PythonLabs team moved to Digital Creations (now Zope
    68: Corporation, see http://www.zope.com).  In 2001, the Python Software
    62: Foundation (PSF, see http://www.python.org/psf/) was formed, a
    66: non-profit organization created specifically to own Python-related
    66: Intellectual Property.  Zope Corporation is a sponsoring member of
     8: the PSF.
     0: 
    70: All Python releases are Open Source (see http://www.opensource.org for
    69: the Open Source Definition).  Historically, most, but not all, Python
    39: releases have also been GPL-compatible.
    
    ¿El archivo se encuentra cerrado?: True


Si bien no cerramos explícitamente el archivo usando la función close,
al salir del bloque de código que encierra el with el archivo se
encontrará cerrado.

Pickles
-------

Los
`*pickles* <https://docs.python.org/2/library/pickle.html#module-pickle>`__
son una forma de guardar estructuras de datos complejas y recuperarlas
fácilmente, sin necesidad de convertirlas a texto y luego parsearlas:

Ejemplo 1: Guardar de a un elemento
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Se puede usar los pickles como se hacía con los viejos archivos de
Pascal, donde se guardaba un registro detrás del otro; pero con la
diferencia de que en este caso no es necesario que todos los registros
sean del mismo tipo:

.. code:: python

    import pickle  # Importo la biblioteca necesaria
    
    # Creo la variable archivo
    with open('ejemplo.pkl', 'wb') as archivo:
        pkl = pickle.Pickler(archivo)  # Creo mi punto de acceso a los datos a partir del archivo
    
        lista1 = [1, 2, 3]
        lista2 = [4, 5]
        diccionario = {'campo1': 1, 'campo2': 'dos'}
    
        pkl.dump(lista1)         # Guardo la lista1 de [1, 2, 3]
        pkl.dump(None)           # Guardo el valor None
        pkl.dump(lista2)
        pkl.dump('Hola mundo')
        pkl.dump('')
        pkl.dump(diccionario)
        pkl.dump(1)

Para leer de un archivo pickle no puedo usar el método readline que usa
la estructura for, por lo que no me queda otra que siempre intentar leer
hasta que lance una excepción del tipo *EOFError*:

.. code:: python

    import pickle
    with open('ejemplo.pkl', 'rb') as archivo:
        print pickle.load(archivo)  # lista1
        print pickle.load(archivo)  # None
        print pickle.load(archivo)  # lista2
        print pickle.load(archivo)  # Hola mundo
        print pickle.load(archivo)  # ''
        print pickle.load(archivo)  # diccionario
        print pickle.load(archivo)  # 1
        print pickle.load(archivo)  # Fin de archivo
        


.. parsed-literal::

    [1, 2, 3]
    None
    [4, 5]
    Hola mundo
    
    {'campo1': 1, 'campo2': 'dos'}
    1


::


    ---------------------------------------------------------------------------

    EOFError                                  Traceback (most recent call last)

    <ipython-input-4-08b16b682993> in <module>()
          8     print pickle.load(archivo)  # diccionario
          9     print pickle.load(archivo)  # 1
    ---> 10     print pickle.load(archivo)  # Fin de archivo
         11 


    /usr/lib/python2.7/pickle.pyc in load(file)
       1382 
       1383 def load(file):
    -> 1384     return Unpickler(file).load()
       1385 
       1386 def loads(str):


    /usr/lib/python2.7/pickle.pyc in load(self)
        862             while 1:
        863                 key = read(1)
    --> 864                 dispatch[key](self)
        865         except _Stop, stopinst:
        866             return stopinst.value


    /usr/lib/python2.7/pickle.pyc in load_eof(self)
        884 
        885     def load_eof(self):
    --> 886         raise EOFError
        887     dispatch[''] = load_eof
        888 


    EOFError: 


.. code:: python

    with open('ejemplo.pkl', 'rb') as archivo:
        seguir_leyendo = True
        while seguir_leyendo:
            try:
                dato = pickle.load(archivo)  # Leo del archivo un elemento
                print dato
            except EOFError:
                seguir_leyendo = False



.. parsed-literal::

    [1, 2, 3]
    None
    [4, 5]
    Hola mundo
    
    {'campo1': 1, 'campo2': 'dos'}
    1


Ejemplo 2: Guardo una lista de elementos
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Así como en el ejemplo anterior guardamos de a un elemento por vez,
también podríamos guardar una lista completa que tenga todos los
elementos en memoria. De ésta forma, los archivos podrían usarse para
cargar los datos al comenzar el programa y guardarlos todos juntos antes
de terminar. Suponiendo que estoy desarrollando un juego en que no van a
haber muchos jugadores compitiendo entre si, podría tener una lista con
los puntajes y hacer:

.. code:: python

    lista = [  # Creo la lista que quiero guardar
        {'usuario': 'csanchez', 'puntaje': 5}, 
        {'usuario': 'pperez', 'puntaje': 3}, 
        {'usuario': 'jromero', 'puntaje': 1}, 
    ]
    
    # Guardo la lista en el archiv
    with open('ejemplo_2.pkl', 'wb') as archivo:
        pkl = pickle.Pickler(archivo)
        pkl.dump(lista)

Y si ahora quiero sumarle 3 puntos a un usuario en particular tendría
que:

1. Leer todo el archivo en una lista
2. Buscar el usuario y actualizarle los puntos
3. Guardar toda la lista en el archivo

.. code:: python

    def imprimir_puntajes(lista_puntajes):
        for puntaje in lista_puntajes:
            print '    ', puntaje
    
    
    # Leo del archivo
    with open('ejemplo_2.pkl', 'rb') as archivo:
        lista_puntajes = pickle.load(archivo)
    
    
    # Actualizo el puntaje
    print 'La lista antes de hacer el cambio es:'
    imprimir_puntajes(lista_puntajes)
    
    pos =  0
    lista_puntajes[pos]['puntaje'] += 3
    
    print 'La lista una vez hecho el cambio es:'
    imprimir_puntajes(lista_puntajes)
    
    # Guardo la lista en el archiv
    with open('ejemplo_2.pkl', 'wb') as archivo:
        pkl = pickle.Pickler(archivo)
        pkl.dump(lista_puntajes)


.. parsed-literal::

    La lista antes de hacer el cambio es:
         {'puntaje': 5, 'usuario': 'csanchez'}
         {'puntaje': 3, 'usuario': 'pperez'}
         {'puntaje': 1, 'usuario': 'jromero'}
    La lista una vez hecho el cambio es:
         {'puntaje': 8, 'usuario': 'csanchez'}
         {'puntaje': 3, 'usuario': 'pperez'}
         {'puntaje': 1, 'usuario': 'jromero'}


Si bien es muy práctica esta alternativa, tiene el gran inconveniente de
no hacer un uso eficiente de la memoria. Si el archivo contiene millones
de usuarios, los estaríamos levantando todos a memoria, con el gran
costo que tiene eso (no sólo en espacio, sino también en tiempo) con el
único objetivo de sumarle 3 puntos a un único usuario. Y una vez que
actualizamos el puntaje de ese usuario, tendríamos que volver a guardar
todo el archivo en el disco.

Abstrayendonos del uso de los pickles
-------------------------------------

Si bien el uso de los pickles puede resultar muy útil, la forma de leer
la información guardada en ellos no suele ser muy cómoda. Por lo que
podríamos implementar en un archivo ``utils.py`` las siguientes dos
funciones para abstraernos un poco de cómo se accede a los datos:

.. code:: python

    # encoding: utf8
    import pickle

    def guardar_en_archivo(archivo, contenido):
        """Guarda lo que le pasen como segundo parámetro en el archivo 
        que recibe como primer parámetro.
        El parámetro llamado archivo tiene que estar abieto en modo 
        binario y para escritura (wb)
        """
        pickler = pickle.Pickler(archivo)
        pickler.dump(contenido)


    def leer_desde_archivo(archivo, valor_por_defecto=None):
        """Lee del archivo archivo un registro y lo retorna junto con una
        variable booleana que indica si llegó al fin de archivo o no.
        El parámetro llamado archivo tiene que estar abieto en modo 
        binario y para lectura (rb).
        Si se intenta leer más allá del fin de archivo, data valdrá lo que le 
        hayan pasado en valor_por_defecto (si no le pasan nada será None)
        y fin_de_archivo será True. En cualquier otro caso fin_de_archivo
        será False.
        """
        try:
            data = pickle.load(archivo)
            fin_de_archivo = False
        except EOFError:
            data = valor_por_defecto
            fin_de_archivo = True
        return data, fin_de_archivo

En este caso, se podría considerar que la función ``leer_desde_archivo``
funciona similar a cómo lo hacen los archivos con un registro
centinella. Por lo que podríamos usar:

.. code:: python

    import utils
    
    
    curso = [
        {'nombre': 'Sanchez, Lucas', 'nota': 8, 'padron': 90431, 'grupo': 1},
        {'nombre': 'Alvarez, Javier', 'nota': 2, 'padron': 92953, 'grupo': 1},
        {'nombre': 'Perez, Matias', 'nota': 10, 'padron': 92407, 'grupo': 1},
        {'nombre': 'Lopez, Pablo', 'nota': 9, 'padron': 96556, 'grupo': 2},
        {'nombre': 'Gonzalez, Marcelo', 'nota': 7, 'padron': 92143, 'grupo': 2},
        {'nombre': 'Rodriguez, Pablo', 'nota': 9, 'padron': 92431, 'grupo': 2},
        {'nombre': 'Gomez, Matias', 'nota': 4, 'padron': 98306, 'grupo': 3},
        {'nombre': 'Diaz, Juan', 'nota': 8, 'padron': 97972, 'grupo': 3},
        {'nombre': 'Garcia, Matias', 'nota': 2, 'padron': 93108, 'grupo': 4},
        {'nombre': 'Rodriguez, Agustin', 'nota': 5, 'padron': 96739, 'grupo': 5},
    ]
    
    print 'Creo el archivo vacío usando el modo "wb"'
    print 'Si tenía algo, ya lo borre...'
    MAX = {'padron': 999999999999}
    with open('curso.pkl', 'wb') as archivo:
        for alumno in curso:
            print 'Guardando el alumno {} en el archivo'.format(alumno)
            utils.guardar_en_archivo(archivo, alumno)
    
    print
    print 'Abro el archivo en modo lectura...'
    with open('curso.pkl', 'rb') as archivo:
        alumno, fin_de_archivo = utils.leer_desde_archivo(archivo)
        while not fin_de_archivo:
            print 'Leyendo el alumno {} en el archivo'.format(alumno)
            alumno, fin_de_archivo = utils.leer_desde_archivo(archivo)



.. parsed-literal::

    Creo el archivo vacío usando el modo "wb"
    Si tenía algo, ya lo borre...
    Guardando el alumno {'nombre': 'Sanchez, Lucas', 'grupo': 1, 'nota': 8, 'padron': 90431} en el archivo
    Guardando el alumno {'nombre': 'Alvarez, Javier', 'grupo': 1, 'nota': 2, 'padron': 92953} en el archivo
    Guardando el alumno {'nombre': 'Perez, Matias', 'grupo': 1, 'nota': 10, 'padron': 92407} en el archivo
    Guardando el alumno {'nombre': 'Lopez, Pablo', 'grupo': 2, 'nota': 9, 'padron': 96556} en el archivo
    Guardando el alumno {'nombre': 'Gonzalez, Marcelo', 'grupo': 2, 'nota': 7, 'padron': 92143} en el archivo
    Guardando el alumno {'nombre': 'Rodriguez, Pablo', 'grupo': 2, 'nota': 9, 'padron': 92431} en el archivo
    Guardando el alumno {'nombre': 'Gomez, Matias', 'grupo': 3, 'nota': 4, 'padron': 98306} en el archivo
    Guardando el alumno {'nombre': 'Diaz, Juan', 'grupo': 3, 'nota': 8, 'padron': 97972} en el archivo
    Guardando el alumno {'nombre': 'Garcia, Matias', 'grupo': 4, 'nota': 2, 'padron': 93108} en el archivo
    Guardando el alumno {'nombre': 'Rodriguez, Agustin', 'grupo': 5, 'nota': 5, 'padron': 96739} en el archivo
    
    Abro el archivo en modo lectura...
    Leyendo el alumno {'nombre': 'Sanchez, Lucas', 'grupo': 1, 'nota': 8, 'padron': 90431} en el archivo
    Leyendo el alumno {'nombre': 'Alvarez, Javier', 'grupo': 1, 'nota': 2, 'padron': 92953} en el archivo
    Leyendo el alumno {'nombre': 'Perez, Matias', 'grupo': 1, 'nota': 10, 'padron': 92407} en el archivo
    Leyendo el alumno {'nombre': 'Lopez, Pablo', 'grupo': 2, 'nota': 9, 'padron': 96556} en el archivo
    Leyendo el alumno {'nombre': 'Gonzalez, Marcelo', 'grupo': 2, 'nota': 7, 'padron': 92143} en el archivo
    Leyendo el alumno {'nombre': 'Rodriguez, Pablo', 'grupo': 2, 'nota': 9, 'padron': 92431} en el archivo
    Leyendo el alumno {'nombre': 'Gomez, Matias', 'grupo': 3, 'nota': 4, 'padron': 98306} en el archivo
    Leyendo el alumno {'nombre': 'Diaz, Juan', 'grupo': 3, 'nota': 8, 'padron': 97972} en el archivo
    Leyendo el alumno {'nombre': 'Garcia, Matias', 'grupo': 4, 'nota': 2, 'padron': 93108} en el archivo
    Leyendo el alumno {'nombre': 'Rodriguez, Agustin', 'grupo': 5, 'nota': 5, 'padron': 96739} en el archivo


Cortes de control
-----------------

Cuando estamos hablando de archivos y nos referimos a ***corte de
control*** estamos haciendo referencia al algoritmo que toma un archivo
ordenado, por una o más claves, y como resultado del mismo nos devuelve
un *"resumen"* del mismo. Por ejemplo, si tenemos el siguiente archivo
ordenado por código de cliente:

+-------------------------+-------------------------+---------------------------+
| **Código de cliente**   | **Número de factura**   | **Monto de la factura**   |
+=========================+=========================+===========================+
| 001                     | 2020452                 | 916                       |
+-------------------------+-------------------------+---------------------------+
| 002                     | 12069115                | 772                       |
+-------------------------+-------------------------+---------------------------+
| 002                     | 14534467                | 264                       |
+-------------------------+-------------------------+---------------------------+
| 002                     | 1424980                 | 752                       |
+-------------------------+-------------------------+---------------------------+
| 002                     | 16214863                | 424                       |
+-------------------------+-------------------------+---------------------------+
| 003                     | 6882583                 | 590                       |
+-------------------------+-------------------------+---------------------------+
| 003                     | 18817277                | 654                       |
+-------------------------+-------------------------+---------------------------+
| 003                     | 1944327                 | 211                       |
+-------------------------+-------------------------+---------------------------+
| 003                     | 16837776                | 595                       |
+-------------------------+-------------------------+---------------------------+
| 003                     | 10145610                | 444                       |
+-------------------------+-------------------------+---------------------------+
| 004                     | 4671025                 | 393                       |
+-------------------------+-------------------------+---------------------------+
| 004                     | 13453769                | 556                       |
+-------------------------+-------------------------+---------------------------+
| 005                     | 7126081                 | 35                        |
+-------------------------+-------------------------+---------------------------+
| 005                     | 16497082                | 367                       |
+-------------------------+-------------------------+---------------------------+

Y queremos calcular cuánta plata gastó cada cliente en nuestro negocio:

::

    El cliente 001 gastó  916
    El cliente 002 gastó 2212
    El cliente 003 gastó 2494
    El cliente 004 gastó  949
    El cliente 005 gastó  402

Podríamos usar el siguiente algoritmo para generar el reporte:

.. code:: python

    import utils
    
    
    def crear_archivo_de_ventas():
        ventas = [
            {'cliente': '001', 'nro_factura': 2020452, 'monto': 916},
            {'cliente': '002', 'nro_factura': 12069115, 'monto': 772},
            {'cliente': '002', 'nro_factura': 14534467, 'monto': 264},
            {'cliente': '002', 'nro_factura': 1424980, 'monto': 752},
            {'cliente': '002', 'nro_factura': 16214863, 'monto': 424},
            {'cliente': '003', 'nro_factura': 6882583, 'monto': 590},
            {'cliente': '003', 'nro_factura': 18817277, 'monto': 654},
            {'cliente': '003', 'nro_factura': 1944327, 'monto': 211},
            {'cliente': '003', 'nro_factura': 16837776, 'monto': 595},
            {'cliente': '003', 'nro_factura': 10145610, 'monto': 444},
            {'cliente': '004', 'nro_factura': 4671025, 'monto': 393},
            {'cliente': '004', 'nro_factura': 13453769, 'monto': 556},
            {'cliente': '005', 'nro_factura': 7126081, 'monto': 35},
            {'cliente': '005', 'nro_factura': 16497082, 'monto': 367}
        ]
    
        print 'Creo el archivo vacío usando el modo "wb"'
        with open('ventas.pkl', 'wb') as archivo:
            for venta in ventas:
                utils.guardar_en_archivo(archivo, venta)
                
                
    def mostrar_ventas_por_cliente(archivo):
        valor_por_defecto = {'cliente': None, 'monto':0}
        total = 0
        # Leo el primer registro del archivo
        venta, fin_de_archivo = utils.leer_desde_archivo(archivo, valor_por_defecto)
        codigo_cliente = venta['cliente']
        while not fin_de_archivo:
            codigo_cliente = venta['cliente']
            subtotal = 0  # Inicializo las ventas de este cliente
            # Mientras siga procesando el mismo cliente...
            while venta['cliente'] == codigo_cliente:
                total += venta['monto']  # Acumulo las ventas totales
                subtotal += venta['monto']  # Acumulo las ventas de este cliente
                venta, fin_de_archivo = utils.leer_desde_archivo(archivo, valor_por_defecto)
    
            print '      El cliente {cliente} gastó {monto:4}'.format(cliente=codigo_cliente, monto=subtotal)
    
        print 'El total es de ${}'.format(total)
        
    
    crear_archivo_de_ventas()
    print 'Abro el archivo en modo lectura...'
    
    # Abro el archivo usando el with para asegurarme 
    # que, pase lo que pase, el archivo quede cerrado
    with open('ventas.pkl', 'rb') as archivo:
        mostrar_ventas_por_cliente(archivo)


.. parsed-literal::

    Creo el archivo vacío usando el modo "wb"
    Abro el archivo en modo lectura...
          El cliente 001 gastó  916
          El cliente 002 gastó 2212
          El cliente 003 gastó 2494
          El cliente 004 gastó  949
          El cliente 005 gastó  402
    El total es de $6973


*¿Y si el archivo fuera de texto?* Es simple, tratamos de llevar el
problema a la solución que conocemos. Para eso podríamos crearnos una
función que se comporte de una forma similar a la que se encuentra en
*utils*:

.. code:: python

    def leer_desde_archivo(archivo, valor_por_defecto):
        try:
            linea = archivo.readline()
            codigo_cliente, factura, monto = linea.strip().split(',')
            data = {
                'cliente': codigo_cliente,
                'factura': int(factura),
                'monto': int(monto)
            }
            fin_de_archivo = False
        except StopIteration:
            data = valor_por_defecto
            fin_de_archivo = True
        
        return data, fin_de_archivo

Esta función, no sólo lee cada línea, sino que una vez leída: 1. usa de
la función ``strip`` para quitar el ``\n`` que tiene al final de la
línea 1. usa la función ``split`` para separar el string por comas 1.
hace uso del *unpacking* para guardar en 3 variables distintas cada uno
de los campos de la línea 1. crea un diccionario con cada uno de los
datos que obtuvo de la línea, pero antes, convierte el número de factura
y el monto a entero usando la función ``int``

Por último, si ya habíamos llegado al final del archivo e intentamos
leer de nuevo, el intérprete va a lanzar la excepción ``StopIteration``
que la capturamos con el ``try-except`` y, en ese caso, devolvemos el
valor que nos pasaron por parámetro.

Entonces, después el algoritmo nos queda igual, a excepción de que ahora
no importamos a la utils y la forma de crear y abrir el archivo va a ser
distinta:

.. code:: python

    def leer_desde_archivo(archivo, valor_por_defecto):
        try:
            linea = archivo.readline()
            codigo_cliente, factura, monto = linea.strip().split(',')
            data = {
                'cliente': codigo_cliente,
                'factura': int(factura),
                'monto': int(monto)
            }
            fin_de_archivo = False
        except Exception:
            data = valor_por_defecto
            fin_de_archivo = True
        
        return data, fin_de_archivo
    
    
    def crear_archivo_de_ventas():
        ventas = """001,2020452,916
    002,12069115,772
    002,14534467,264
    002,1424980,752
    002,16214863,424
    003,6882583,590
    003,18817277,654
    003,1944327,211
    003,16837776,595
    003,10145610,444
    004,4671025,393
    004,13453769,556
    005,7126081,35
    005,16497082,367
    """
        print 'Creo el archivo vacío usando el modo "wt"'
        with open('ventas.csv', 'wt') as archivo:
            archivo.write(ventas)
                
                
    def mostrar_ventas_por_cliente(archivo):
        valor_por_defecto = {'cliente': None, 'monto':0}
        total = 0
        # Leo el primer registro del archivo
        venta, fin_de_archivo = leer_desde_archivo(archivo, valor_por_defecto)
        codigo_cliente = venta['cliente']
        while not fin_de_archivo:
            codigo_cliente = venta['cliente']
            subtotal = 0  # Inicializo las ventas de este cliente
            # Mientras siga procesando el mismo cliente...
            while venta['cliente'] == codigo_cliente:
                total += venta['monto']  # Acumulo las ventas totales
                subtotal += venta['monto']  # Acumulo las ventas de este cliente
                venta, fin_de_archivo = leer_desde_archivo(archivo, valor_por_defecto)
    
            print '      El cliente {cliente} gastó {monto:4}'.format(cliente=codigo_cliente, monto=subtotal)
    
        print 'El total es de ${}'.format(total)
        
    
    crear_archivo_de_ventas()
    print 'Abro el archivo en modo lectura...'
    # Abro el archivo usando el with para asegurarme 
    # que, pase lo que pase, el archivo quede cerrado
    with open('ventas.csv', 'rt') as archivo:
        mostrar_ventas_por_cliente(archivo)


.. parsed-literal::

    Creo el archivo vacío usando el modo "wt"
    Abro el archivo en modo lectura...
          El cliente 001 gastó  916
          El cliente 002 gastó 2212
          El cliente 003 gastó 2494
          El cliente 004 gastó  949
          El cliente 005 gastó  402
    El total es de $6973


Merge de archivos
-----------------

El merge, o apareo, de archivos consiste en tener dos o más archivos que
se encuentran ordenados por una misma clave y se quieren procesar
leyéndolos una única vez y generar un reporte o un nuevo archivo con
dicha información consolidada. Supongamos que tenemos el siguiente
código para crear unos archivos de prueba:

.. code:: python

    import utils
    oper = [
        {'cta': 1, 'imp': 800},
        {'cta': 1, 'imp': 250},
        {'cta': 2, 'imp': 700},
        {'cta': 2, 'imp': 700},
        {'cta': 10, 'imp': 1000},
    ]
    with open('movs1.pkl', 'wb') as archivo:
        for movimiento in oper:
            print 'Guardando la operacion {} en el archivo movs1.pkl'.format(movimiento)
            utils.guardar_en_archivo(archivo, movimiento)
    
    print
    
    operaciones_2 = [
        {'cta': 1, 'imp': 800},
        {'cta': 2, 'imp': 700},
        {'cta': 3, 'imp': 700},
        {'cta': 10, 'imp': 100},
        {'cta': 15, 'imp': 3},
    ]
    with open('movs2.pkl', 'wb') as archivo:
        for movimiento in operaciones_2:
            print 'Guardando la operacion {} en el archivo movs2.pkl'.format(movimiento)
            utils.guardar_en_archivo(archivo, movimiento)



.. parsed-literal::

    Guardando la operacion {'imp': 800, 'cta': 1} en el archivo movs1.pkl
    Guardando la operacion {'imp': 250, 'cta': 1} en el archivo movs1.pkl
    Guardando la operacion {'imp': 700, 'cta': 2} en el archivo movs1.pkl
    Guardando la operacion {'imp': 700, 'cta': 2} en el archivo movs1.pkl
    Guardando la operacion {'imp': 1000, 'cta': 10} en el archivo movs1.pkl
    
    Guardando la operacion {'imp': 800, 'cta': 1} en el archivo movs2.pkl
    Guardando la operacion {'imp': 700, 'cta': 2} en el archivo movs2.pkl
    Guardando la operacion {'imp': 700, 'cta': 3} en el archivo movs2.pkl
    Guardando la operacion {'imp': 100, 'cta': 10} en el archivo movs2.pkl
    Guardando la operacion {'imp': 3, 'cta': 15} en el archivo movs2.pkl


Entonces si lo que quiero es mostrar el estado de cada una de estas
cuentas podría hacer:

.. code:: python

    import utils
    
    with open('movs1.pkl', 'rb')as movs1, open('movs2.pkl', 'rb') as movs2:
        MAX = {'cta': 99999999, 'imp':0}
        oper1, eof1 = utils.leer_desde_archivo(movs1, MAX)
        oper2, eof2 = utils.leer_desde_archivo(movs2, MAX)
        total = 0
        while not eof1 or not eof2:
             totcta = 0
             men = min(oper1['cta'], oper2['cta'])
             print 'La menor de las cuentas entre {} y {} es {}'.format(
                oper1['cta'],
                oper2['cta'],
                men
            )
             while oper1['cta'] == men:
                        print 'Procesando la cuenta {} de movs1'.format(oper1['cta'])
                        total += oper1['imp']
                        totcta += oper1['imp']
                        oper1, eof1 = utils.leer_desde_archivo(movs1, MAX)
    
             while  oper2['cta'] == men:
                        print 'Procesando la cuenta {} de movs2'.format(oper2['cta'])
                        total += oper2['imp']
                        totcta += oper2['imp']
                        oper2, eof2 = utils.leer_desde_archivo(movs2, MAX)
    
             print 'Total por cta:', men , totcta
    
    print 'Total Gral:', total


.. parsed-literal::

    La menor de las cuentas entre 1 y 1 es 1
    Procesando la cuenta 1 de movs1
    Procesando la cuenta 1 de movs1
    Procesando la cuenta 1 de movs2
    Total por cta: 1 1850
    La menor de las cuentas entre 2 y 2 es 2
    Procesando la cuenta 2 de movs1
    Procesando la cuenta 2 de movs1
    Procesando la cuenta 2 de movs2
    Total por cta: 2 2100
    La menor de las cuentas entre 10 y 3 es 3
    Procesando la cuenta 3 de movs2
    Total por cta: 3 700
    La menor de las cuentas entre 10 y 10 es 10
    Procesando la cuenta 10 de movs1
    Procesando la cuenta 10 de movs2
    Total por cta: 10 1100
    La menor de las cuentas entre 99999999 y 15 es 15
    Procesando la cuenta 15 de movs2
    Total por cta: 15 3
    Total Gral: 5753


Actualizar archivo con novedades
--------------------------------

Cuando tiene toda la información en un único archivo (comúnmente llamado
archivo *maestro*) y en cierto momento se la quiere actualizar a partir
de un segundo archivo llamado *novedades* se genera un tercer archivo
con toda la información consolidada. Los archivos maestro y novedades
deberán estar ordenados por la misma clave, por lo que el nuevo archivo
maestro también debe quedar ordenado. Por ejemplo, si contamos con un
archivo llamado *cuentas.pkl* que en casa posición tiene la información
correspondiente a una cuenta bancaria:

-  **nro\_cuenta**: Número de cuenta
-  **tituar**: Titular de la cuenta
-  **saldo**: Saldo de la cuenta
-  **tipo\_cuenta**: Tipo de cuenta
-  **moneda**: Moneda en la cual opera la cuenta

Y uno que tenga las novedades diarias llamado *movimientos.pkl* con la
siguiente información:

-  **tipo**: Tipo de movimiento, es un string de una letra que puede ser
   A (alta), B (baja), M (modificación)
-  **nro\_cuenta**
-  Si es:
-  *alta*\ (se asume saldo 0):

   -  **titular**
   -  **tipo\_cuenta**
   -  **moneda**

-  *modificación*:

   -  **tipo\_movimiento**: Un string que será una de las siguientes
      opciones: "credito" (cuando ingresa plata a la cuenta) o "debito"
      (cuando extraen plata de la cuenta)
   -  **monto**: Monto a acreditar o debitar de la cuenta

-  *baja*: no es necesario agregar más campos

.. code:: python

    import utils
    
    
    def crear_archivo_maestro():
        cuentas = [
            {'nro_cuenta': 1, 'saldo': 7094, 'moneda': '$', 
             'tipo_cuenta': 'debito', 'titular': 'cliente_1'}, 
            {'nro_cuenta': 2, 'saldo': 2896, 'moneda': '$', 
             'tipo_cuenta': 'debito', 'titular': 'cliente_2'}, 
            {'nro_cuenta': 3, 'saldo': 14424, 'moneda': '$', 
             'tipo_cuenta': 'corriente', 'titular': 'cliente_3'}, 
            {'nro_cuenta': 5, 'saldo': 7156, 'moneda': '$', 
             'tipo_cuenta': 'corriente', 'titular': 'cliente_5'}, 
            {'nro_cuenta': 8, 'saldo': 7500, 'moneda': '$', 
             'tipo_cuenta': 'corriente', 'titular': 'cliente_8'}, 
            {'nro_cuenta': 9, 'saldo': 2128, 'moneda': '$', 
             'tipo_cuenta': 'debito', 'titular': 'cliente_9'}, 
            {'nro_cuenta': 13, 'saldo': 13524, 'moneda': '$', 
             'tipo_cuenta': 'corriente', 'titular': 'cliente_13'}, 
            {'nro_cuenta': 15, 'saldo': 9479, 'moneda': '$', 
             'tipo_cuenta': 'debito', 'titular': 'cliente_15'}, 
            {'nro_cuenta': 21, 'saldo': 8462, 'moneda': '$', 
             'tipo_cuenta': 'debito', 'titular': 'cliente_21'}, 
            {'nro_cuenta': 25, 'saldo': 6258, 'moneda': '$', 
             'tipo_cuenta': 'debito', 'titular': 'cliente_25'}, 
            {'nro_cuenta': 32, 'saldo': 14082, 'moneda': '$', 
             'tipo_cuenta': 'debito', 'titular': 'cliente_32'}
        ]
        with open('cuentas.pkl', 'wb') as archivo:
            for cuenta in cuentas:
                utils.guardar_en_archivo(archivo, cuenta)
    
    
    def crear_archivo_novedades():
        novedades = [
            {'nro_cuenta': 1, 'tipo': 'B'},
            {'nro_cuenta': 2, 'monto': 731, 
             'tipo_movimiento': 'debito', 'tipo': 'M'},
            {'nro_cuenta': 3, 'monto': 791, 
             'tipo_movimiento': 'debito', 'tipo': 'M'},
            {'nro_cuenta': 4, 'moneda': '$', 
             'tipo_cuenta': 'corriente', 
             'titular': 'cliente_4', 'tipo': 'A'},
            {'nro_cuenta': 8, 'monto': 750, 
             'tipo_movimiento': 'debito', 'tipo': 'M'},
            {'nro_cuenta': 11, 'moneda': '$', 
             'tipo_cuenta': 'corriente', 'titular': 'cliente_11', 
             'tipo': 'A'},
            {'nro_cuenta': 13, 'monto': 481, 
             'tipo_movimiento': 'debito', 'tipo': 'M'},
            {'nro_cuenta': 15, 'tipo': 'B'},
            {'nro_cuenta': 16, 'moneda': '$', 
             'tipo_cuenta': 'debito', 'titular': 'cliente_16', 
             'tipo': 'A'},
            {'nro_cuenta': 19, 'moneda': '$', 
             'tipo_cuenta': 'corriente', 'titular': 'cliente_19', 
             'tipo': 'A'},
            {'nro_cuenta': 21, 'monto': 653, 
             'tipo_movimiento': 'debito', 'tipo': 'M'},
            {'nro_cuenta': 25, 'tipo': 'B'},
            {'nro_cuenta': 32, 'tipo': 'B'},
        ]
        with open('movimientos.pkl', 'wb') as archivo:
            for nov in novedades:
                utils.guardar_en_archivo(archivo, nov)
    
    
    ################### Apareo ###################
    
    def dar_de_alta(archivo, novedad):
        del novedad['tipo']  # Le borro el campo tipo que no
                             # existe en el archivo maestro
        novedad['saldo'] = 0  # Inicializo el saldo en 0
        utils.guardar_en_archivo(archivo, novedad)
    
        
    def modificar_cuenta(archivo, cuenta, novedad):
        if novedad['tipo_movimiento'] == 'credito':
            monto = novedad['monto']
        else:
            monto = -1 * novedad['monto']
    
        cuenta['saldo'] += monto
        utils.guardar_en_archivo(archivo, cuenta)
        
    def apareo(maestro, novedades, nuevo):
        cuenta, eof_ctas = utils.leer_desde_archivo(maestro)
        nov, eof_novs = utils.leer_desde_archivo(novedades)
        while not eof_ctas and not eof_novs:
            print 'Procesando cuenta nro {} y novedad {} del tipo {}'.format(
                cuenta['nro_cuenta'], nov['nro_cuenta'], nov['tipo']
            )
            if nov['nro_cuenta'] < cuenta['nro_cuenta'] and nov['tipo'] == 'A':
                # Si es un alta, acomodo el registro y lo guardo
                dar_de_alta(nuevo, nov)
                nov, eof_novs = utils.leer_desde_archivo(novedades)
    
                # No puede ser una B o M porque habría un error
            elif nov['nro_cuenta'] == cuenta['nro_cuenta']:
                if nov['tipo'] == 'M':
                    # Si es una modificación, actualizo la cuenta, 
                    # guardo y leo de los dos archivos
                    modificar_cuenta(nuevo, cuenta, nov)
    
                cuenta, eof_ctas = utils.leer_desde_archivo(maestro)
                nov, eof_novs = utils.leer_desde_archivo(novedades)
    
                # Si fuera una B, tendría que ignorarlos y leer de 
                # los archivos igual.
    
                # No puede ser una A porque habría un error
            elif nov['nro_cuenta'] > cuenta['nro_cuenta']:
                # Si la novedad tiene un número de cuenta mayor, 
                # significa que para esa cuenta no hubo novedades
                # por lo que la guardo tal cual esta sin modificar
                # y leo la siguiente
                utils.guardar_en_archivo(nuevo, cuenta)
                cuenta, eof_ctas = utils.leer_desde_archivo(maestro)
    
        # Como salí del while, termine con al menos uno de los
        # dos archivos, por lo que ahora puedeo leer lo que
        # quedaba y guardarlo casi tal cual vienen
        while not eof_ctas:
            print 'Procesando cuenta nro {}'.format(cuenta['nro_cuenta'])
            utils.guardar_en_archivo(nuevo, cuenta)
            cuenta, eof_ctas = utils.leer_desde_archivo(maestro)
    
        while not eof_novs:
            print 'Procesando la novedad {} del tipo {}'.format(
                nov['nro_cuenta'], nov['tipo']
            )
            del nov['tipo']
            nov['saldo'] = 0
            utils.guardar_en_archivo(nuevo, nov)
            nov, eof_novs = utils.leer_desde_archivo(novedades)
    
    
    def mostrar_archivo_nuevo():
        print 'El archivo nuevo tiene los registros:'
        with open('nuevo.pkl', 'rb') as nuevo:
            cuenta, eof_ctas = utils.leer_desde_archivo(nuevo)
            while not eof_ctas:
                print cuenta
                cuenta, eof_ctas = utils.leer_desde_archivo(nuevo)            
    
    
    crear_archivo_maestro()
    crear_archivo_novedades()
    
    with open('cuentas.pkl', 'rb') as maestro, \
        open('movimientos.pkl', 'rb') as novedades, \
        open('nuevo.pkl', 'wb') as nuevo:
            apareo(maestro, novedades, nuevo)
    
    mostrar_archivo_nuevo()


.. parsed-literal::

    Procesando cuenta nro 1 y novedad 1 del tipo B
    Procesando cuenta nro 2 y novedad 2 del tipo M
    Procesando cuenta nro 3 y novedad 3 del tipo M
    Procesando cuenta nro 5 y novedad 4 del tipo A
    Procesando cuenta nro 5 y novedad 8 del tipo M
    Procesando cuenta nro 8 y novedad 8 del tipo M
    Procesando cuenta nro 9 y novedad 11 del tipo A
    Procesando cuenta nro 13 y novedad 11 del tipo A
    Procesando cuenta nro 13 y novedad 13 del tipo M
    Procesando cuenta nro 15 y novedad 15 del tipo B
    Procesando cuenta nro 21 y novedad 16 del tipo A
    Procesando cuenta nro 21 y novedad 19 del tipo A
    Procesando cuenta nro 21 y novedad 21 del tipo M
    Procesando cuenta nro 25 y novedad 25 del tipo B
    Procesando cuenta nro 32 y novedad 32 del tipo B
    El archivo nuevo tiene los registros:
    {'nro_cuenta': 2, 'saldo': 2165, 'moneda': '$', 'titular': 'cliente_2', 'tipo_cuenta': 'debito'}
    {'nro_cuenta': 3, 'saldo': 13633, 'moneda': '$', 'titular': 'cliente_3', 'tipo_cuenta': 'corriente'}
    {'nro_cuenta': 4, 'saldo': 0, 'moneda': '$', 'tipo_cuenta': 'corriente', 'titular': 'cliente_4'}
    {'nro_cuenta': 5, 'saldo': 7156, 'moneda': '$', 'titular': 'cliente_5', 'tipo_cuenta': 'corriente'}
    {'nro_cuenta': 8, 'saldo': 6750, 'moneda': '$', 'titular': 'cliente_8', 'tipo_cuenta': 'corriente'}
    {'nro_cuenta': 9, 'saldo': 2128, 'moneda': '$', 'titular': 'cliente_9', 'tipo_cuenta': 'debito'}
    {'nro_cuenta': 11, 'saldo': 0, 'moneda': '$', 'tipo_cuenta': 'corriente', 'titular': 'cliente_11'}
    {'nro_cuenta': 13, 'saldo': 13043, 'moneda': '$', 'titular': 'cliente_13', 'tipo_cuenta': 'corriente'}
    {'nro_cuenta': 16, 'saldo': 0, 'moneda': '$', 'tipo_cuenta': 'debito', 'titular': 'cliente_16'}
    {'nro_cuenta': 19, 'saldo': 0, 'moneda': '$', 'tipo_cuenta': 'corriente', 'titular': 'cliente_19'}
    {'nro_cuenta': 21, 'saldo': 7809, 'moneda': '$', 'titular': 'cliente_21', 'tipo_cuenta': 'debito'}


.. raw:: html

   <!--
   ## JSON

   Otra forma de guardar datos estructurados es usar un módulo llamado [json](https://docs.python.org/2/tutorial/inputoutput.html#saving-structured-data-with-json) y para esto se usan las funciones [dump](https://docs.python.org/2/library/json.html#json.dump) y [load](https://docs.python.org/2/library/json.html#json.load). <br>
   Como ventaja tenemos que 
   -->

Ejercicios
----------

1. Hacer el corte de control para un archivo que tenga la información
   del curso de algoritmos 1 y nos diga si todos sus integrantes
   aprobaron el parcial y el promedio de sus notas.
2. Hacer el apareo, pero asumiendo que pueden venir más de un movimiento
   por cuenta (puede ser un alta, varios debitos/creditos e incluso una
   baja).
3. Hacer un merge de dos archivos ordenados, que no es más que mezclar
   dos archivos del mismo tipo (por ejemplo, dos archivos maestro de
   cuentas bancarias) y generar un tercero donde se encuentren todos los
   registros de los primeros dos.
4. Suponiendo que existe un archivo llamado utils.py donde se encuentran
   las funciones:

.. code:: python

    def guardar_en_archivo(archivo, contenido):
        """Guarda lo que le pasen como segundo parámetro en el archivo 
        que recibe como primer parámetro.
        El parámetro llamado archivo tiene que estar abieto en modo 
        binario y para escritura (wb)
        """
        ...


    def leer_desde_archivo(archivo, valor_por_defecto=None):
        """Lee del archivo archivo un registro y lo retorna junto con una
        variable booleana que indica si llegó al fin de archivo o no.
        El parámetro llamado archivo tiene que estar abieto en modo 
        binario y para lectura (rb).
        Si se intenta leer más allá del fin de archivo, data valdrá lo que le 
        hayan pasado en valor_por_defecto (si no le pasan nada será None)
        y fin_de_archivo será True. En cualquier otro caso fin_de_archivo
        será False.
        """
        ...
        return data, fin_de_archivo

Leer dos archivos (61\_matematica.dat y 75\_computacion.dat) que tendrán
registros con los campos: \* padron \* nombre \* apellido \* nota \*
codigo\_departamento \* codigo\_materia y armar uno nuevo donde sólo
figuren las notas de los alumnos aprobados ordenados por padrón. Ambos
archivos están ordenados por padrón y se deben leer una única vez. Como
los archivos pueden ser muy grandes, no se pueden guardar en memoria.
Una vez procesados los dos archivos se tienen que informar, para cada
materia, cuántos alumnos aprobaron y cuántos desaprobaron.
