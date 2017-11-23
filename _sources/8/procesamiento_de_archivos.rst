
.. raw:: html

   <!--
   03/11
   Archivos binarios. Pickles.
   Apareo de archivos secuenciales.
   CLASE DE LABORATORIO 
   (Gonzalo)
   -->

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


