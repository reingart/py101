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

.. datafile:: ejemplo.txt
   :edit:
   :rows: 20
   :cols: 60

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

.. activecode:: py_01
    :nocodelens:

    arch = open("ejemplo.txt")
    cadena = arch.read(15)
    print("# Imprimo los primeros 15 caracteres del archivo. Tiene que ser 'Python was crea'")
    print(cadena)
    
    print("# Leo otros 7 caracteres y dejo el cursor del archivo en la siguiente posición. Tiene que ser 'ted in '")
    cadena = arch.read(7)
    print(cadena)
    
    print("# Ahora leo el resto del archivo.")
    cadena = arch.read()
    print(cadena)
    
    print('# Cierro el archivo')
    arch.close()


La única condición que tenemos para usar este método es que el archivo
lo hayamos abierto en modo lectura.

.. activecode:: py_02
    :nocodelens:

    # en el navegador no se pueden escribir archivos;
    # en su máquina la siguiente instrucción genera un error:
    arch2 = open("ejemplo.txt", "w")
    arch2.read()


.. activecode:: py_03
    :nocodelens:

    # Y si intentamos con un append? (idem)
    arch3 = open("ejemplo.txt", "a")
    arch3.read()


Otra primitiva que podemos usar es
`**readline** <https://docs.python.org/2/library/stdtypes.html#file.readline>`__,
que al igual que
`**read** <https://docs.python.org/2/library/stdtypes.html#file.read>`__,
también puede recibir un parámetro que indique la cantidad máxima de
bytes a leer. Si no se le pasa ningún parámetro, lee toda la línea.

.. activecode:: py_04
    :nocodelens:

    arch = open("ejemplo.txt")
    linea = arch.readline()  # Notar que también imprime el Enter o \n
    print(linea)
    linea = arch.readline(7)  # La segunda línea es 'Mathematisch Centrum (CWI, see http://www.cwi.nl) in the Netherlands'
    print(linea)
    arch.close()



Pero no es necesario que leamos de a una sola línea, sino que también
podemos leer todas las líneas del archivo y guardarlas en una lista
haciendo uso de la primitiva
`**readlines** <https://docs.python.org/2/library/stdtypes.html#file.readlines>`__.

.. activecode:: py_05
    :nocodelens:

    arch = open("ejemplo.txt")
    lineas = arch.readlines()
    print(lineas)
    arch.close()



Sin embargo, la forma más *Pythonic* de leer el archivo por líneas es
usando la estructura **for** y quedaría casi como lo diríamos en
castellano: *"Para cada línea del archivo*. Por ejemplo, si queremos
imprimir la cantidad de caracteres de cada línea podríamos hacer:

.. activecode:: py_06
    :nocodelens:

    arch = open("ejemplo.txt")
    for linea in arch:
        print(len(linea))
    
    arch.close()



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

.. datafile:: ejemplo2.txt
   :hide:

   Es la primer cadenaSeguida de la segunda con un fin de linea
   1. Primero de la lista sin fin de línea. 2. Segundo string con fin de línea.
   3. Tercero conn.
   4. y último.


.. activecode:: py_07
    :nocodelens:

    # en el navegador no se pueden crear archivos, este es un ejemplo simulado:
    arch2 = open("ejemplo2.txt", "w")
    arch2.write("Es la primer cadena")
    arch2.write("Seguida de la segunda con un fin de linea\n")
    for linea in ["1. Primero de la lista sin fin de línea. ", 
                  "2. Segundo string con fin de línea.\n",
                  "3. Tercero con\\n.\n", "4. y último."]:
        arch2.write(linea)
    arch2.flush()
    arch2.close()
    arch2 = open("ejemplo2.txt", "r+a")
    strfile = arch2.read()
    print(strfile)



¿Y qué pasa si le quiero agregar algunas líneas a este archivo?

.. activecode:: py_08
    :nocodelens:

    # en el navegador no se pueden modificar archivos, correrlo en su máquina:
    arch2.write("Esto lo estoy agregando.\n.")
    arch2.writelines("Y estas dos líneas también con un \\n al final\n de cada una.\n")
    arch2.flush()
    arch2 = open("ejemplo2.txt", "r")  # El open hace que me mueva a la primer posición del archivo.
    print(arch2.read())
    arch2.close()

    

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

.. activecode:: py_09
    :nocodelens:

    arch = open("ejemplo.txt")  
    arch.seek(30)        # Voy a la posición número 30 del archivo
    print(arch.read(7))  # Debería salir 'y 1990s'
    arch.seek(-5,1)      # Me muevo 5 posiciones para atrás desde mi posición actual.
    print(arch.read(7))  # Debería imprimir '1990s b'
    arch.seek(-12,2)     # Me muevo a la posición número 12, comenzando a contar desde el final.
    print(arch.read(10)) # Debería imprimir 'compatible'
    
    arch.close()



Y así como podemos movernos en un archivo, también podemos averiguar
nuestra posición usando la primitiva
`**tell()** <https://docs.python.org/2/library/stdtypes.html#file.tell>`__.

.. activecode:: py_10
    :nocodelens:

    arch = open("ejemplo.txt")  
    arch.seek(30)
    print(arch.tell())   # Debería imprimir 30
    arch.seek(-5,1)      # Retrocedo 5 posiciones
    print(arch.tell())   # Debería imprimir 25
    arch.seek(-12,2)     # Voy a 12 posiciones antes del fin de archivo
    print(arch.tell())   # Debería imprimir 1132
    print(arch.read(10)) # Leo 10 caracteres
    print(arch.tell())   # Debería imprimir 1142



¿Cómo recorrer todo un archivo?
-------------------------------

Cuando llegamos al final de un archivo de texto usando la función *read*
o *readline* Python no arroja ningún valor, pero tampoco retorna ningún
caracter, por lo que podríamos usar eso como condición de corte:

.. activecode:: py_11
    :nocodelens:

    arch = open("ejemplo.txt")  
    
    # El archivo ejemplo.txt tiene 22 líneas, por lo que
    # si quiero imprimirlo completo anteponiendo el 
    # número de línea y la cantidad de caracteres
    # puedo hacer:
    
    for x in range(1, 25):
        linea = arch.readline()
        print('{:2}[{:02}] - {}'.format(x, len(linea), linea))
    
    arch.close()



Como pueden ver, todas las líneas hasta la 22 (que es la última linea
del arhcivo) tienen una longitud mayor a 0; incluso las 5, 10 y 19 que
aparentemente no tienen ningún caracter. Eso es así ya que siempre
tienen por lo menos uno, que es el Enter o ``\n``. Otra cosa a tener en
cuenta es que, por más que intentamos leer más allá del fin de archivo,
en ningún momento el interprete nos lanzó una excepción. Por lo tanto,
si no sabemos la longitud del archivo como era este caso, podríamos usar
esta información para darnos cuenta cuándo dejar de leer:

.. activecode:: py_12
    :nocodelens:

    arch = open("ejemplo.txt")  
    
    # Si no sabemos la cantidad de líneas que tiene 
    # el archivo que queremos recorrer podemos hacer:
    
    linea = arch.readline()
    x = 0
    
    while linea:  # Es decir, mientras me devuelva algo 
                  # distinto al sting vacío
        x += 1
        print('{:2}[{:02}] - {}'.format(x, len(linea), linea))
        linea = arch.readline()
    
    arch.close()



Aunque Python también nos ofrece otra forma de recorer un archivo, y es
usando una de las estructuras que ya conocemos: **for**

.. activecode:: py_13
    :nocodelens:

    arch = open("ejemplo.txt")  
    
    # Si no sabemos la cantidad de líneas que tiene 
    # el archivo que queremos recorrer podemos hacer:
    
    x = 0
    for linea in arch:
        x += 1
        print('{:2}[{:02}] - {}'.format(x, len(linea), linea))
    
    arch.close()



O, incluso, usar enumerate para saber qué línea estoy leyendo:

.. activecode:: py_14
    :nocodelens:

    arch = open("ejemplo.txt")  
    
    # Si no sabemos la cantidad de líneas que tiene 
    # el archivo que queremos recorrer podemos hacer:
    
    # Usando enumerate y comenzando en 1
    for x, linea in enumerate(arch, 1):
        print('{:2}[{:02}] - {}'.format(x, len(linea), linea))
    
    arch.close()



