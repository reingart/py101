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


