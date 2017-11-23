
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



