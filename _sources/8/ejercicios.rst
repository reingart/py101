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
