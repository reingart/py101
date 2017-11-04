Ejercicios
==========

1. Dado un número N, calcular su factorial
2. Procesar una lista de números enteros, e imprimir para cada uno de
   ellos:

-  el número que se esta procesando
-  la suma parcial de los mismos

3. La relación entre temperaturas Celsius y Fahrenheit está dada por:

   .. math:: C = 5/9 * (F-32)

   Escribir un algoritmo que haga una tabla de valores
   Celsius-Fahrenheit, para valores entre O F y 200 F , con intervalos
   de 10 grados.
4. Procesar una lista de números enteros, e imprimir para cada uno de
   ellos:

-  el número que se esta procesando
-  la suma parcial de los mismos
-  True si el número era mayor al anterior y False en caso contrario

Cortar cuando se los haya procesado a todos, o al alcanzar una suma
parcial mayor o igual a 100 5. Procesar una lista de números y generar
un diccionario con dos claves llamadas "par" e "impar". Al terminar de
procesar la lista el diccionario debe tener todos los números que
proceso agrupados en pares e impares.

Por ejemplo, si contamos con la lista [1, 5, 2, 6, 9, 3, 8], el
diccionario que se obtenga debería ser: {"par": [2, 6, 8], "impar": [1,
5, 9, 3]} 6. Escribir un programa que dadas dos listas de igual longitud
imprima la suma de ellas posición a posición. 7. Suponiendo que cuenta
con una lista en la que en cada posición tiene la información de un
alumno en un registro:
``Python [{'nombre': 'XX', 'padrón': 1, 'nota': 4, 'grupo': 1}, ...]``
1. Se desea imprimir el nombre y padrón de todos los alumnos aprobados.
2. Asumiendo que la lista se encuentra ordenada por número de grupo, se
pide indicar aquellos grupos para los cuales todos sus integrantes hayan
aprobado el parcial recorriendo sólo una vez la lista. 8. Se cuenta con
dos listas de números ordenadas de forma creciente y se desea obtener
una nueva lista ordenada que contenga todos los números, pero sin
ordenarla nuevamente. 10. Procesar una lista de strings e ir guardando
en un diccionario la cantidad de ocurrencias de cada palabra (distinguir
mayúsculas y minúsculas). Por ejemplo, para la lista
``Python ['Otra', 'posible', 'clasificacion', 'radica', 'en', 'si', 'una', 'variable', 'puede', 'cambiar', 'el', 'tipo', 'de', 'dato', 'que', 'se', 'puede', 'almacenar', 'en', 'ella', 'entre', 'una', 'sentencia', 'y', 'la', 'siguiente', '(', 'tipado', 'dinamico', ')', 'O', 'si', 'en', 'la', 'etapa', 'de', 'definicion', 'se', 'le', 'asigna', 'un', 'tipo', 'de', 'dato', 'a', 'una', 'variable', 'y', 'por', 'mas', 'que', 'se', 'puede', 'cambiar', 'el', 'contenido', 'de', 'la', 'misma', 'no', 'cambie', 'el', 'tipo', 'de', 'dato', 'de', 'lo', 'que', 'se', 'almacena', 'en', 'ella', '(', 'tipado', 'estatico', ')']``
El resultado sería:

.. activecode:: py_27
    :nocodelens:

      {'el': 3, 'en': 4, 'etapa': 1, 'por': 1, 'Otra': 1, 'contenido': 1, 'almacenar': 1, 'sentencia': 1, 'le': 1, 'tipo': 3, 'la': 3, ')': 2, '(': 2, 'almacena': 1, 'estatico': 1, 'dinamico': 1, 'mas': 1, 'cambiar': 2, 'tipado': 2, 'ella': 2, 'de': 6, 'definicion': 1, 'puede': 3, 'dato': 3, 'que': 3, 'O': 1, 'variable': 2, 'asigna': 1, 'entre': 1, 'a': 1, 'siguiente': 1, 'posible': 1, 'clasificacion': 1, 'no': 1, 'radica': 1, 'una': 3, 'si': 2, 'un': 1, 'misma': 1, 'lo': 1, 'y': 2, 'cambie': 1, 'se': 4}
