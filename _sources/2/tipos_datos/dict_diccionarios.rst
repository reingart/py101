Diccionarios (dict)
-------------------

El equivalente a los registros de Pascal serían los
`diccionarios <https://docs.python.org/3/tutorial/datastructures.html#dictionaries>`__,
pero éstos también ofrecen mayor flexibilidad:

.. activecode:: py_11
    :nocodelens:

    registros_con_campos_variables = {'campo1': 12, 
                                      'campo2': 'valor campo2'}
    print(registros_con_campos_variables)
    print(type(registros_con_campos_variables))
    print()
    
    print('Le agrego un campo al diccionario')
    registros_con_campos_variables['otro_campo'] = 432
    print(registros_con_campos_variables)
    print()
    
    print('Y ahora otro, pero con un int como índice')
    registros_con_campos_variables[123] = 'también puede usarse ' \
        'los números como clave'
    print(registros_con_campos_variables)



Además, se pueden usar los campos de un registro para armar una forma
más simple los strings:

.. activecode:: py_12
    :nocodelens:

    alumno = {
        'nombre': 'Juan',
        'apellido': 'Perez',
        'nota': 2
    }
    
    print('El alumno %(nombre)s %(apellido)s se sacó un %(nota)s' % alumno)
    print('El alumno {nombre} {apellido} se sacó un {nota}'
        .format(**alumno))


Y si le queremos modificar la nota a un alumno, sólo tenemos que acceder
a ese campo y asignarle un nuevo valor:

.. activecode:: py_13
    :nocodelens:

    alumno = {
        'nombre': 'Juan',
        'apellido': 'Perez',
        'nota': 2
    }
    print(alumno)
    
    alumno['nota'] = 5
    print(alumno)



O incluso se le puede cambiar el tipo de dato a un campo y agregar uno
nuevo:

.. activecode:: py_14
    :nocodelens:

    alumno = {
        'nombre': 'Juan',
        'apellido': 'Perez',
        'parcial': 2
    }
    print('Alumno:', alumno)
    
    
    alumno['parcial'] = [2, 6]  # Cambio el tipo de dato de int a list
    print('Agrego la nota del recuperatorio:', alumno)
    
    alumno['coloquio'] = 8  # Agrego un nuevo campo
    print('Agrego la nota del coloquio:', alumno)
    
    del alumno['parcial']  # Elimino el campo nota
    print('Elimino las notas del parcial:', alumno)


Algo que hay que tener en cuenta es que el orden en que se asignan los
campos a un registro no es el orden interno de esos campos.

