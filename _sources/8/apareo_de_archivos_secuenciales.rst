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



