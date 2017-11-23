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



