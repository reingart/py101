Ejercicios
==========

1.  Se leen dos listas A y B, de N y M elementos respectivamente.
    Construir un algoritmo que halle las listas unión e intersección de
    A y B. Previamente habrá que ordenarlos.
2.  Escribir una función que reciba una lista desordenada y un elemento,
    que:
3.  Busque todos los elementos coincidan con el pasado por parámetro y
    devuelva la cantidad de coincidencias encontradas.
4.  Busque la primera coincidencia del elemento en la lista y devuelva
    su posición.
5.  Escribir una función que reciba una lista de números no ordenada,
    que:
6.  Devuelva el valor máximo.
7.  Devuelva una tupla que incluya el valor máximo y su posición.
8.  ¿Qué sucede si los elementos son cadenas de caracteres? Nota: no
    utilizar ``lista.sort()`` ni la función ``sorted``.
9.  Se cuenta con una lista ordenada de productos, en la que uno
    consiste en una tupla de (identificador, descripción, precio), y una
    lista de los productos a facturar, en la que cada uno consiste en
    una tupla de (identificador, cantidad). Se desea generar una factura
    que incluya la cantidad, la descripción, el precio unitario y el
    precio total de cada producto comprado, y al final imprima el total
    general. Escribir una función que reciba ambas listas e imprima por
    pantalla la factura solicitada.
10. Leer de teclado (usando la función raw\_input) los datos de un
    listado de alumnos terminados con padrón 0. Para cada alumno deben
    leer: # Padrón # Nombre # Apellido # Nota del primer parcial # Nota
    del primer recuperatorio (en caso de no haber aprobado el parcial) #
    Nota del segundo recuperatorio (en caso de no haber aprobado en el
    primero) # Nombre del grupo # Nota del TP 1 # Nota del TP 2 Si el
    padrón es 0, no deben seguir pidiendo el resto de los campos. Tanto
    el padrón, como el nombre y apellido deben leerse como strings
    (existen padrones que comienzan con una letra b), pero debe
    validarse que se haya ingresado algo de por lo menos 2 caracteres.
    Todas las notas serán números enteros entre 0 y 10, aunque puede ser
    que el usuario accidentalmente ingrese algo que no sea un número,
    por lo que deberán validar la entrada y volver a pedirle los datos
    al usuario hasta que ingrese algo válido. También deben validar que
    las notas pertenezcan al rango de 0 a 10. Se asume que todos los
    alumnos se presentan a todos los parciales hasta aprobar o completar
    sus 3 chances. Al terminar deben:
11. imprimir por pantalla un listado de todos los alumnos en condiciones
    de rendir coloquio (último parcial aprobado y todos los TP
    aprobados) en el mismo orden en el que el usuario los ingreso.
12. imprimir por pantalla un listado de todos los alumnos en condiciones
    de rendir coloquio (último parcial aprobado y todos los TP
    aprobados) ordenados por padrón en forma creciente.
13. imprimir por pantalla un listado de todos los alumnos en condiciones
    de rendir coloquio (último parcial aprobado y todos los TP
    aprobados) ordenados por nota y, en caso de igualdad, por padrón
    (ambos en forma creciente).
14. Calcular para cada alumno el promedio de sus notas del parcial y
    luego el promedio del curso como el promedio de todos los promedios.
15. Informar cuál es la nota que más se repite entre todos los parciales
    (sin importar si es primer, segundo o tercer parcial) e indicar la
    cantidad de ocurrencias.
16. listar todas las notas que se sacaron los alumnos en el primer
    parcial y los padrones de quienes se sacaron esas notas con el
    siguiente formato:

``Nota: 2   * nnnn1   * nnnn2   * nnnn3   * nnnn4 Nota: 4   * nnnn1   * nnnn2   ...``
Tener en cuenta que las notas pueden ser del 2 al 10 y puede ocurrir que
nadie se haya sacado esa nota (y en dicho caso no esa nota no tiene que
aparecer en el listado)
