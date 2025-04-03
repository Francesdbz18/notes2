[Acquiring Core ABAP Skills](https://learning.sap.com/learning-journeys/acquire-core-abap-skills)
![[Pasted image 20250324105634.png]]
### Transacciones
- SE38: Editor de código
- SE37: Módulo funciones
- SE80: Navegador de objetos
- SE11: Diccionario de datos, tablas
- SE16: BD (deprecated, use SE11 & SE16N)
- SE16N: BD
- SE24: Generador clases.
- SM12: Quitar bloqueos. 
(Z3ENRAYA, ZSHOP)

### Atajos y trucos: 
- /n: cerrar ventana y abrir nueva
- /o: abrir en nueva ventana
- * para especificar que se desconoce el contenido antes o después del texto introducido
- Ctrl + N: abre una nueva ventana
- Intro al escribir: valida el texto introducido
- F8: ejecutar

### Convenciones:
- Los programas deben empezar por Z (o Y).
- Todo se escribe en mayúsculas. Es posible usar minúsculas en textos y tablas.
- Variables: global =gv_, local = lv_, parameters = p_, select options = s_
- Dentro de una subrutina: clear o refresh a estructuras antes de volver a rellenarlas.
- Nombres de clases: ZCL_XXXX.

### Paquete y orden:
- Una orden por proyecto con todo el contenido.
- Nombre de paquete: ZPRACS25_FF
- Tendremos un paquete por persona. Se recomienda agrupar los ejercicios de un mismo tema en una orden.

### Toolbar:
- Cambiar entre editar y ver
- Validar sintaxis.
- Ejecutar
- Visualizar objetos relacionados al programa.
- Módulo: genera llamadas a métodos y funciones.
- Pretty Printer: corrige indentaciones, mayúsculas, minúsculas...
- Elementos de texto
- Buscar texto
- Buscar texto en todo el report
- Finalizar: vuelve al inicio de SE38.

### Debugging:
- /h durante ejecución, empieza línea por línea
- Establecer breakpoint cliqueando crea un breakpoint durante la sesión.
- Escribir BREAK-POINT. establece un breakpoint que no se borra.
- F5: pasa a la siguiente línea ejecutable, incluyendo subrutinas (métodos).
- F6: F5 sin entrar a la subrutina.
- F7: Si se está en un archivo fuera del programa principal, vuelve.
- F8: salta hasta el siguiente breakpoint o, en su defecto, hasta el final.

```ABAP
WRITE: 'pene'.

```
' str ': elimina espacios
acento agudo: no elimina espacios


### Ejercicios:
Nombre: ZEJERCICIO_NUM_XX
1. Declara 2 variables de cada uno de los tipos de variables de tipo numéricos aprendidas y asígnales valores arbitrarios. Realiza las siguientes operaciones entre dos variables de cada tipo: suma, resta, multiplicación, división, división entera, resto, exponenciación
```ABAP
REPORT zejercicio_1_ff.  
DATA: int        TYPE i VALUE 2,  
      int2       TYPE i VALUE 5,  
      float      TYPE f VALUE '1.5',  
      float2     TYPE f VALUE '3.1',  
      decfloat1 TYPE decfloat16 VALUE '4.5',  
      decfloat12 TYPE decfloat16 VALUE '9.5',  
      decfloat2 TYPE decfloat34 VALUE '8.9',  
      decfloat22 TYPE decfloat34 VALUE '4.5',  
      packed1    TYPE p LENGTH 16 DECIMALS 3 VALUE '5.444',  
      packed12    TYPE p LENGTH 16 DECIMALS 4 VALUE '5.4444'.  
  
DATA: resul1 TYPE i.  
resul1 = int + int2.  
WRITE: 'Suma: ', resul1.  
resul1 = int * int2.  
WRITE: 'Multiplicación: ', resul1.  
resul1 = int2 - int.  
WRITE: 'Resta: ',resul1.  
resul1 = int2 / int.  
WRITE: 'DIvisión: ' ,resul1.  
resul1 = int2 DIV int.  
WRITE: 'División entera: ', resul1.  
resul1 = int2 MOD int.  
WRITE: 'Resto: ', resul1.  
resul1 = int2 ** int.  
WRITE: 'Potencia de 2: ', resul1, cl_abap_char_utilities=>cr_lf.  
NEW-LINE.
```
2. Declarar 2 strings, concatenarlas, imprimir substrings de cada una y concatenar los substrings.
```ABAP
DATA: str1 TYPE string VALUE 'Adiós',  
      str2 TYPE string VALUE 'Hola',  
      concatenacion TYPE string,  
      substr1 TYPE string,  
      substr2 TYPE string.  
concatenacion = str1 && str2.  
WRITE: concatenacion.  
NEW-LINE.  
CONCATENATE str1 str2 INTO concatenacion.  
WRITE: concatenacion.  
new-LINE.  
substr1 = str1+2(2).  
WRITE: substr1.  
NEW-LINE.  
substr2 = str2(2).  
WRITE: substr2.  
new-LINE.  
CONCATENATE substr1 substr2 INTO concatenacion.  
WRITE: concatenacion.
```
3.  Declarar e imprimir por pantalla: 
	1. un tipo producto con campos:
		1. ID(C5)
		2. Name(c15)
		3. UPrice(Pd5). 
	2. Un tipo pedido con campos:
		1. ID(C10)
		2. Date (D)
		3. Time (T)
		4. 5x ProductX
		5. TotalPrice (Pd2)
	3. 5 variables Producto
	4. 1 variable pedido
```ABAP
TYPES: BEGIN OF producto,  
         id     TYPE c LENGTH 5,  
         name   TYPE c LENGTH 15,  
         uprice TYPE p DECIMALS 2,  
       END OF producto,  
       BEGIN OF pedido,  
         id         TYPE c LENGTH 10,  
         date       TYPE d,  
         time       TYPE t,  
         producto1   TYPE producto,  
         producto2   TYPE producto,  
         producto3   TYPE producto,  
         producto4   TYPE producto,  
         producto5   TYPE producto,  
         totalprice TYPE p DECIMALS 2,  
       END OF pedido.  
DATA:  
      product1 type producto,  
      product2 type producto,  
      product3 type producto,  
      product4 type producto,  
      product5 type producto.  
  
product1-id = 'AAAAA'.  
product1-name = 'Cuaderno'.  
product1-uprice = '11.55'.  
product2-id = 'BBBBB'.  
product2-name = 'Estuche'.  
product2-uprice = '10.05'.  
product3-id = 'CCCCC'.  
product3-name = 'Bolígrafo'.  
product3-uprice = '1.55'.  
product4-id = 'DDDDD'.  
product4-name = 'Lápiz'.  
product4-uprice = '2.55'.  
product5-id = 'EEEEE'.  
product5-name = 'Corrector'.  
product5-uprice = '5.55'.  
  
DATA: pedido1 type pedido.  
  
pedido1-id = 'aaaaaaaaaaaaaaa'.  
pedido1-date = sy-datum.  
pedido1-time = cl_demo_date_time=>get_user_time( ).  
pedido1-producto1 = product1.  
pedido1-producto2 = product2.  
pedido1-producto3 = product3.  
pedido1-producto4 = product4.  
pedido1-producto5 = product5.  
pedido1-totalprice = pedido1-producto1-uprice + pedido1-producto2-uprice + pedido1-producto3-uprice + pedido1-producto4-uprice + pedido1-producto5-uprice.  
  
WRITE: pedido1-id.  
new-line.  
WRITE: pedido1-date.  
new-line.  
WRITE: pedido1-time.  
new-line.  
WRITE: pedido1-producto1-id.  
new-line.  
WRITE: pedido1-producto1-name.  
new-line.  
WRITE: pedido1-producto1-uprice.  
new-line.  
WRITE: pedido1-producto2-id.  
new-line.  
WRITE: pedido1-producto2-name.  
new-line.  
WRITE: pedido1-producto2-uprice.  
new-line.  
WRITE: pedido1-producto3-id.  
new-line.  
WRITE: pedido1-producto3-name.  
new-line.  
WRITE: pedido1-producto3-uprice.  
new-line.  
WRITE: pedido1-producto4-id.  
new-line.  
WRITE: pedido1-producto4-name.  
new-line.  
WRITE: pedido1-producto4-uprice.  
new-line.  
WRITE: pedido1-producto5-id.  
new-line.  
WRITE: pedido1-producto5-name.  
new-line.  
WRITE: pedido1-producto5-uprice.  
new-line.  
WRITe: pedido1-totalprice.
```
4. Investiga cómo capturar excepciones y cómo dar formato a una variable tipo fecha en la impresión por pantalla.
3.5. Rellenar la información de los productos (ejercicio 3) con parameters y select options. Añadir un campo cantidad al producto.

```ABAP

```
Operadores:
- EQ: Equals
- > o GT: greater than
- < o LT:  menor
- <>
- >=
- <=
- CS
- CP
- BREAK
- CONTINUE
- CHECK

Ejercicios
1. Contar hasta 10 con DO.
```ABAP
DATA i type i value 0.  
do 10 times.  
  i = i + 1.  
  write i.  
  enddo.
```
2. Par o impar con IF.
```ABAP
PARAMETERs p_num TYPE i OBLIGATORY.  
IF p_num MOD 2 EQ 0.  
  WRITE 'par.'.  
ELSE.  
  WRITE 'impar'.  
ENDIF.
```
3. Clasificar notas con CASE.
```ABAP
PARAMETERS p_num TYPE i OBLIGATORY.  
CASE p_num.  
  WHEN 1.  
    WRITE'suspenso'.  
  WHEN 2.  
    WRITE'suspenso'.  
  WHEN 3.  
    WRITE'suspenso'.  
  WHEN 4.  
    WRITE 'suspenso'.  
  WHEN 5.  
    WRITE'bien'.  
  WHEN 6.  
    WRITE 'bien'.  
  WHEN 7.  
    WRITE 'notable'.  
  WHEN 8.  
    WRITE 'notsble'.  
  WHEN 9.  
    WRITE 'sobresaliente'.  
  WHEN 10.  
    WRITE 'sobresaliente'.  
  WHEN OTHERS.  
    WRITE'ingrese una nota válida'.  
ENDCASE.
```
4. Imprimir del 1 al 5 usando WHILE.
```ABAP
WHILE gv_num LT 5.  
  gv_num = gv_num + 1.  
  WRITE gv_num.  
  NEW-LINE.  
ENDWHILE.
```
5. Solicitar N y calcular suma de los primeros N números.
```ABAP
PARAMETERS p_num TYPE i OBLIGATORY.  
DATA:  
  gv_suma TYPE i VALUE 0.  
DO ( p_num ) TIMES.  
  gv_suma = gv_suma + sy-index.  
  WRITE gv_suma.  
ENDDO.
```
6. Tabla de multiplicar con DO.
```ABAP
PARAMETERS p_num TYPE i OBLIGATORY.  
DATA: gv_resul TYPE i VALUE 0,  
      gv_index TYPE i VALUE 1.  
DO 10 TIMES.  
  gv_resul = gv_index * p_num.  
  WRITE gv_resul.  
  gv_index = gv_index + 1.  
ENDDO.
```
7. Positivo, negativo o 0 con if.
```ABAP

```
8. Días de la semana con CASE.
```ABAP
PARAMETERS p_num TYPE i OBLIGATORY.  
CASE p_num.  
  WHEN 1.  
    WRITE 'lunes'.  
  WHEN 2.  
    WRITE 'martes'.  
  WHEN 3.  
    WRITE 'miércoles'.  
  WHEN 4.  
    WRITE 'jueves'.  
  WHEN 5.  
    WRITE 'viernes'.  
  WHEN 6.  
    WRITE 'sábado'.  
  WHEN 7.  
    WRITE 'domingo'.  
  WHEN OTHERS.  
    WRITE 'ERROR: Escriba un número del 1 al 7.'.  
ENDCASE.
```
9. Contar usando WHILE.
```ABAP
REPORT zbucles_9_ff.  
PARAMETERS p_num TYPE i OBLIGATORY.  
WHILE sy-index LE p_num.  
  WRITE sy-index.  
ENDWHILE.
```
10. Sumar numeros pares con DO.
```ABAP
REPORT zbucles_10_ff.  
PARAMETERS p_num TYPE i OBLIGATORY.  
DATA: gv_suma TYPE i VALUE 0.  
DO ( p_num / 2 ) TIMES.  
  gv_suma = gv_suma + 2.  
  CHECK gv_suma lt p_num.  
  WRITE gv_suma.  
ENDDO.
```
11. Detener la ejecución con EXIT.
```ABAP
REPORT ZBUCLES_11_FF.  
while sy-index le 10.  
  write sy-index.  
  check sy-index eq 5.  
  exit.  
  ENDWHILE.
```
12. Saltar pares usando continue.
```ABAP
WHILE sy-index LE 10.  
  IF sy-index MOD 2 NE 0.  
    CONTINUE.  
  ENDIF.  
  WRITE sy-index.  
ENDWHILE.
```
13. Mostrar sólo múltiplos de 3 en while.
```ABAP
WHILE sy-index LE 10.  
  CHECK sy-index MOD 3 EQ 0.  
  WRITE sy-index.  
ENDWHILE.
```
14. Exit dentro de un DO.
```ABAP
PARAMETERS p_num TYPE i OBLIGATORY.  
DATA:  
  gv_suma TYPE i VALUE 0.  
DO ( p_num ) TIMES.  
  gv_suma = gv_suma + sy-index.  
  IF gv_suma GE 50.  
    NEW-LINE.  
    WRITE: 'La suma ha parado en: ', sy-index.  
    EXIT.  
  ENDIF.  
  WRITE gv_suma.  
ENDDO.
```
15.  CHECK dentro de CASE.
```ABAP
PARAMETERS p_num TYPE i OBLIGATORY.  
CASE p_num.  
  WHEN 1 OR 3 OR 5 OR 7 OR 9.  
    CHECK p_num GE 5.  
    WRITE 'Es impar.'.  
  WHEN 2 OR 4 OR 6 OR 8 OR 10.  
    CHECK p_num GE 5.  
    WRITE 'Es par.'.  
ENDCASE.
```
o1. Año bisiesto.
```ABAP
PARAMETERS p_num TYPE i OBLIGATORY.  
IF ( p_num MOD 4 EQ 0 AND p_num MOD 100 NE 0 ) OR ( p_num MOD 400 EQ 0 ).  
  WRITE 'Es un año bisiesto.'.  
ELSE.  
  WRITE ' No es un año bisiesto.'.  
ENDIF.
```
o2. Número aleatorio en rango de notas.
```ABAP
DATA: lo_ran  TYPE REF TO cl_abap_random_int,   lv_i   TYPE i,   lv_seed TYPE i.  
lv_seed = sy-timlo.lo_ran = cl_abap_random_int=>create( min = 5 max = 25 seed = lv_seed ). lv_i = lo_ran->get_next( ).  
PARAMETERS p_str TYPE string OBLIGATORY.  
CASE p_str.  
  WHEN 'SUSPENSO'.  
    lo_ran = cl_abap_random_int=>create( min = 1 max = 4 seed = lv_seed ). lv_i = lo_ran->get_next( ).  
    WRITE lv_i.  
  WHEN 'BIEN'.  
    lo_ran = cl_abap_random_int=>create( min = 5 max = 6 seed = lv_seed ). lv_i = lo_ran->get_next( ).  
    WRITE lv_i.  
  WHEN 'NOTABLE'.  
    lo_ran = cl_abap_random_int=>create( min = 7 max = 8 seed = lv_seed ). lv_i = lo_ran->get_next( ).  
    WRITE lv_i.  
  WHEN 'SOBRESALIENTE'.  
    lo_ran = cl_abap_random_int=>create( min = 9 max = 10 seed = lv_seed ). lv_i = lo_ran->get_next( ).  
    WRITE lv_i.  
  WHEN OTHERS.  
    WRITE 'Introduzca una calificación correcta.'.  
ENDCASE.
```
> [!NOTE] MODIFY TABLE añade nuevos campos si no están en la tabla

- CLEAR y REFRESH para vaciar variables y tablas respectivamente.
- Para crear tablas, estructuras y tipo tablas globales, SE11.
- No se pueden imprimir por pantalla estructuras completas en una única línea.

LOOP AT gt_test INTO DATA(gs_test2).
ENDLOOP.

1. Llenar standard table de ints.
```ABAP
REPORT ztablas_1_ff.  
DATA: int    TYPE i,  
      gt_int TYPE TABLE OF i.  
WHILE sy-index LE 5.  
  APPEND sy-index TO gt_int.  
ENDWHILE.  
  
LOOP AT gt_int INTO int.  
  WRITE: int.  
ENDLOOP.
```
2. Sorted table.
```abap
REPORT ZTABLAS_2_FF.  
TYPES: BEGIN OF gs_clientes,  
  ID TYPE i,  
  name type string,  
  budget type i,  
  end of gs_clientes.  
  
DATA: gt_sorted_table TYPE SORTED TABLE OF gs_clientes with UNIQUE key ID,  
      gv_clientes type gs_clientes.  
  gv_clientes-ID = 1. gv_clientes-name = 'Juanito Alimaña'. gv_clientes-budget = 69420.  
  insert gv_clientes into table gt_sorted_table.  
  gv_clientes-ID = 3. gv_clientes-name = 'Pablo Pueblo'. gv_clientes-budget = 2.  
  insert gv_clientes into table gt_sorted_table.  
  gv_clientes-ID = 1. gv_clientes-name = 'Juanito Alimaña'. gv_clientes-budget = 69420.  
  insert gv_clientes into table gt_sorted_table.  
  gv_clientes-ID = 2. gv_clientes-name = 'Pedrito Navaja'. gv_clientes-budget = 45000.  
  insert gv_clientes into table gt_sorted_table.  
  
  LOOP AT gt_sorted_table into gv_clientes.  
      WRITE: gv_clientes-ID,  
          gv_clientes-name,  
          gv_clientes-budget.  
      ENDLOOP.
```
3. Hashed table
```abap
TYPES: BEGIN OF ty_empleado,  
         id      TYPE i,  
         nombre  TYPE string,  
         salario TYPE p LENGTH 10 DECIMALS 2,  
       END OF ty_empleado.  
  
DATA: lt_empleados TYPE HASHED TABLE OF ty_empleado  
                    WITH UNIQUE KEY id.  
DATA: lv_empleado TYPE ty_empleado.  
lv_empleado-id = 1.  
lv_empleado-nombre = 'Juan Perez'.  
lv_empleado-salario = 3500.  
INSERT lv_empleado INTO TABLE lt_empleados.  
  
lv_empleado-id = 2.  
lv_empleado-nombre = 'Maria Gomez'.  
lv_empleado-salario = 4200.  
INSERT lv_empleado INTO TABLE lt_empleados.  
  
lv_empleado-id = 3.  
lv_empleado-nombre = 'Carlos Ruiz'.  
lv_empleado-salario = 5000.  
INSERT lv_empleado INTO TABLE lt_empleados.  
LOOP AT lt_empleados INTO lv_empleado.  
  WRITE: / 'ID:', lv_empleado-id,  
         'Nombre:', lv_empleado-nombre,  
         'Salario:', lv_empleado-salario.  
ENDLOOP.
```
4. Empleados
```abap
TYPES: BEGIN OF ty_empleado,  
         id      TYPE i,  
         nombre  TYPE string,  
         salario TYPE p LENGTH 10 DECIMALS 2,  
       END OF ty_empleado.  
DATA: lt_empleados TYPE STANDARD TABLE OF ty_empleado.  
DATA: lv_empleado TYPE ty_empleado.  
lv_empleado-id = 1.  
lv_empleado-nombre = 'Juan Perez'.  
lv_empleado-salario = 3500.  
INSERT lv_empleado INTO TABLE lt_empleados.  
  
lv_empleado-id = 2.  
lv_empleado-nombre = 'Maria Gomez'.  
lv_empleado-salario = 4200.  
INSERT lv_empleado INTO TABLE lt_empleados.  
  
lv_empleado-id = 3.  
lv_empleado-nombre = 'Carlos Ruiz'.  
lv_empleado-salario = 5000.  
INSERT lv_empleado INTO TABLE lt_empleados.  
  
LOOP AT lt_empleados INTO lv_empleado.  
  WRITE: / 'ID:', lv_empleado-id,  
         'Nombre:', lv_empleado-nombre,  
         'Salario:', lv_empleado-salario.  
ENDLOOP.
```
5. Eliminar duplicados.
```abap
lv_empleado-id = 1.  
lv_empleado-nombre = 'Juan Perez'.  
lv_empleado-salario = 3500.  
INSERT lv_empleado INTO TABLE lt_empleados.  
  
lv_empleado-id = 2.  
lv_empleado-nombre = 'Maria Gomez'.  
lv_empleado-salario = 4200.  
INSERT lv_empleado INTO TABLE lt_empleados.  
  
lv_empleado-id = 3.  
lv_empleado-nombre = 'Carlos Ruiz'.  
lv_empleado-salario = 5000.  
INSERT lv_empleado INTO TABLE lt_empleados.  
  
LOOP AT lt_empleados INTO lv_empleado.  
  WRITE: / 'ID:', lv_empleado-id,  
         'Nombre:', lv_empleado-nombre,  
         'Salario:', lv_empleado-salario.  
ENDLOOP.  
  
sort lt_empleados.  
DELETE ADJACENT DUPLICATES FROM lt_empleados COMPARING ALL FIELDS.  
  
write /'TABLA TRAS ORDENAR Y ELIMINAR ADYACENTES.'.  
LOOP AT lt_empleados INTO lv_empleado.  
  WRITE: / 'ID:', lv_empleado-id,  
         'Nombre:', lv_empleado-nombre,  
         'Salario:', lv_empleado-salario.  
ENDLOOP.
```
6. Uso de una tabla con estructura y sy index.
```abap
REPORT ztablas_6_ff.  
TYPES: BEGIN OF ty_empleado,  
         nombre TYPE string,  
         orden  TYPE c,  
       END OF ty_empleado.  
  
DATA: lt_empleados TYPE STANDARD TABLE OF ty_empleado,  
      empleado     TYPE ty_empleado.  
  
DO 5 TIMES.  
  empleado-orden = sy-index.  
  if sy-index eq 1.  
    empleado-nombre = sy-uname.  
    else.  
      CONCATENATE 'Empleado ' empleado-orden into empleado-nombre.  
      endif.  
      append empleado to lt_empleados.  
ENDDO.  
  
LOOP AT lt_empleados INTO empleado.  
  WRITE: /  
         'Nombre:', empleado-nombre,  
         'Orden:', empleado-orden.  
ENDLOOP.
```
7. Ordenar tabla manualmente.
```abap
SORT lt_empleados by ID.
```
8. Contar registros.
```abap
DATA(lv_count) = lines( lt_empleados ).  
  
WRITE: / 'La tabla tiene ', lv_count, ' registros.'.
```
9. Buscar valores.
```abap
PARAMETERS p_num TYPE i OBLIGATORY.  
DATA lv_num TYPE i.  
READ TABLE lt_empleados INTO lv_empleado WITH KEY salario = p_num.  
IF sy-subrc = 0.  
  WRITE: / 'El número fue encontrado en la tabla.'.  
ELSE.  
  WRITE: / 'El número no se encuentra en la tabla.'.  
ENDIF.
```
10. Estructuras anidadas.
```
TYPES:  
  BEGIN OF ty_direccion,  
    calle  TYPE string,  
    numero TYPE i,  
  END OF ty_direccion,  
  BEGIN OF ty_empleado,  
    id        TYPE i,  
    nombre    TYPE string,  
    salario   TYPE p LENGTH 10 DECIMALS 2,  
    direccion TYPE ty_direccion,  
  END OF ty_empleado.  
  
DATA: lt_empleados TYPE STANDARD TABLE OF ty_empleado.  
DATA: lv_empleado TYPE ty_empleado.  
DATA: lv_direccion TYPE ty_direccion.  
lv_empleado-id = 1.  
lv_empleado-nombre = 'Juan Perez'.  
lv_empleado-salario = 3500.  
lv_direccion-calle = 'Plaza de Chueca'.  
lv_direccion-numero = 3.  
lv_empleado-direccion = lv_direccion.  
INSERT lv_empleado INTO TABLE lt_empleados.  
  
lv_empleado-id = 2.  
lv_empleado-nombre = 'Maria Gomez'.  
lv_empleado-salario = 4200.  
lv_direccion-calle = 'Calle de Válgame Dios'.  
lv_direccion-numero = 2.  
lv_empleado-direccion = lv_direccion.  
INSERT lv_empleado INTO TABLE lt_empleados.  
  
lv_empleado-id = 3.  
lv_empleado-nombre = 'Carlos Ruiz'.  
lv_empleado-salario = 5000.  
lv_direccion-calle = 'Calle de Augusto Figueroa'.  
lv_direccion-numero = 30.  
lv_empleado-direccion = lv_direccion.  
INSERT lv_empleado INTO TABLE lt_empleados.  
  
LOOP AT lt_empleados INTO lv_empleado.  
  WRITE: / 'ID:', lv_empleado-id,  
         ' Nombre:', lv_empleado-nombre,  
         ' Salario:', lv_empleado-salario,  
         ' Calle:', lv_empleado-direccion-calle,  
         ' Número:', lv_empleado-direccion-numero.  
ENDLOOP.
```
11. Fusión de dos tablas.
```
DATA: lt_tabla1    TYPE STANDARD TABLE OF i,  
      lt_tabla2    TYPE STANDARD TABLE OF i,  
      lt_resultado TYPE STANDARD TABLE OF i,  
      lv_numero    TYPE i.  
APPEND 10 TO lt_tabla1.  
APPEND 20 TO lt_tabla1.  
APPEND 30 TO lt_tabla1.  
APPEND 40 TO lt_tabla1.  
APPEND 20 TO lt_tabla2.  
APPEND 50 TO lt_tabla2.  
APPEND 60 TO lt_tabla2.  
APPEND 30 TO lt_tabla2.  
LOOP AT lt_tabla1 INTO lv_numero.  
  INSERT lv_numero INTO TABLE lt_resultado.  
ENDLOOP.  
LOOP AT lt_tabla2 INTO lv_numero.  
  READ TABLE lt_resultado TRANSPORTING NO FIELDS WITH KEY table_line = lv_numero.  
  IF sy-subrc <> 0.  
    INSERT lv_numero INTO TABLE lt_resultado.  
  ENDIF.  
ENDLOOP.  
LOOP AT lt_resultado INTO lv_numero.  
  WRITE: / lv_numero.  
ENDLOOP.
```
12. Contar frecuencia.
```

```
12. Tablas anidadas.
```
TYPES: BEGIN OF ty_proyecto,  
         nombre_proyecto TYPE c LENGTH 30,  
       END OF ty_proyecto.  
  
TYPES: ty_tabla_proyectos TYPE STANDARD TABLE OF ty_proyecto WITH EMPTY KEY.  
  
TYPES: BEGIN OF ty_empleado,  
         id        TYPE c LENGTH 5,  
         nombre    TYPE c LENGTH 20,  
         proyectos TYPE ty_tabla_proyectos,  
       END OF ty_empleado.  
  
DATA: gt_empleados TYPE STANDARD TABLE OF ty_empleado,  
      gs_empleado  TYPE ty_empleado,  
      gs_proyecto  TYPE ty_proyecto.  
  
gs_empleado-id = '1'.  
gs_empleado-nombre = 'Juan'.  
  
CLEAR gs_empleado-proyectos.  
APPEND VALUE ty_proyecto( nombre_proyecto = 'Desarrollo multiplataforma' ) TO gs_empleado-proyectos.  
APPEND VALUE ty_proyecto( nombre_proyecto = 'Campaña de marketing' ) TO gs_empleado-proyectos.  
  
APPEND gs_empleado TO gt_empleados.  
  
gs_empleado-id = '2'.  
gs_empleado-nombre = 'Pepe'.  
  
CLEAR gs_empleado-proyectos.  
APPEND VALUE ty_proyecto( nombre_proyecto = 'Compra de mercadería' ) TO gs_empleado-proyectos.  
  
APPEND gs_empleado TO gt_empleados.  
  
LOOP AT gt_empleados INTO gs_empleado.  
  WRITE:gs_empleado-id, gs_empleado-nombre.  
  LOOP AT gs_empleado-proyectos INTO gs_proyecto.  
    WRITE gs_proyecto-nombre_proyecto.  
  ENDLOOP.  
ENDLOOP.
```
### Subrutinas

1. Cuadrado de un número.

```abap
REPORT zsubrutinas_1_ff.  
PARAMETERS p_num TYPE i OBLIGATORY.  
  
FORM square USING n TYPE i.  
  n = n * n.  
  WRITE n.  
ENDFORM.  
  
START-OF-SELECTION.  
  PERFORM square USING p_num.
```
2. Conversión de grados Celsius a grados Fahrenheit.
3. Suma de dos números.
```abap
REPORT zsubrutinas_3_ff.  
PARAMETERS p_num TYPE i OBLIGATORY.  
PARAMETERS p_num2 TYPE i OBLIGATORY.  
DATA suma TYPE i.  
  
FORM sumar USING num TYPE i num2 TYPE i CHANGING suma.  
  suma = num + num2.  
ENDFORM.  
  
START-OF-SELECTION.  
  PERFORM sumar USING p_num p_num2 CHANGING suma.  
  WRITE suma.
```
4. Contar vocales.
```abap
REPORT zsubrutinas_4_ff.  
PARAMETERS p_str TYPE string OBLIGATORY.  
  
  
FORM countVowels USING p_str TYPE string.  
  TRANSLATE p_str TO UPPER CASE.  
  DATA(resultado) = count_any_of(     val = p_str sub   = `AEIOU` ).  
  WRITE resultado.  
ENDFORM.  
  
START-OF-SELECTION.  
  PERFORM countVowels USING p_str.
```
5. Invertir una cadena.
```abap
PARAMETERS p_str TYPE string OBLIGATORY.  
  
  
FORM invert USING p_str TYPE string.  
  data(lv_length) = strlen( p_str ).  
  data(i) = lv_length.  
  data(reversed) = p_str.  
  reversed = reverse( reversed ).  
  write reversed.  
  ENDFORM.  
  
  START-OF-SELECTION.  
  perform invert using p_str.
```
### Eventos del programa
1. INITIALIZATION
```abap
REPORT ZEVENTOS_1_FF.  
data gv_num type i.  
  
INITIALIZATION.  
gv_num = 69420.  
  
START-OF-SELECTION.  
write gv_num.
```
2. AT SELECTION-SCREEN
```abap
PARAMETERS: p_num TYPE i.  
  
AT SELECTION-SCREEN.  
  IF p_num <= 0.  
*IMPORTANTE: La siguiente línea es un mensaje de error.  
    message 'El número debe ser positivo.' type 'E'.  
  ENDIF.
```
3. AT SELECTION-SCREEN OUTPUT
```abap
REPORT ZEVENTOS_3_FF.  
PARAMETERS: p_str TYPE string.  
  
AT SELECTION-SCREEN OUTPUT.  
  MESSAGE 'Si ejecutas este programa, el servidor va a explotar.' TYPE 'W'.  
  
END-OF-SELECTION.  
  write 'Te lo advertí. *kaboom*'.
```
4. start-of-selection
```abap
REPORT ZEVENTOS_4_FF.  
PARAMETERS: p_num TYPE i.  
  
START-OF-SELECTION.  
  WRITE: / p_num.
```
5. END-OF-SELECTION
```abap
DATA: lt_values TYPE TABLE OF i,  
      lv_value  TYPE i.  
  
START-OF-SELECTION.  
  DO 10 TIMES.  
    lv_value = sy-index.  
    APPEND lv_value TO lt_values.  
  ENDDO.  
  LOOP AT lt_values INTO lv_value.  
    WRITE: / lv_value.  
  ENDLOOP.  
  
END-OF-SELECTION.  
  WRITE: / 'Se acabó.'.
```
### Field-symbols
1. Modificar valores
```
DATA: lt_nombres TYPE TABLE OF string,  
      lv_nombre  TYPE string.  
APPEND 'Álex' TO lt_nombres.  
APPEND 'Andrés' TO lt_nombres.  
APPEND 'Francesco' TO lt_nombres.  
READ TABLE lt_nombres ASSIGNING FIELD-SYMBOL(<fs>) INDEX 2.  
<fs> = 'Natalia'.  
LOOP AT lt_nombres INTO lv_nombre.  
  WRITE: / lv_nombre.  
ENDLOOP.
```
2. Suma de elementos de una tabla interna (con varios campos)
3. Copiar valores de una tabla a otra sin LOOP AT.
```abap
REPORT zfieldsymbols_3_ff.  
DATA: lt_tabla1 TYPE TABLE OF string,  
      lt_tabla2 TYPE TABLE OF string,  
      lv_str    TYPE string.  
  
lv_str = 'Juanito'.  
APPEND lv_str TO lt_tabla1.  
  
lv_str = 'Pepita'.  
APPEND lv_str TO lt_tabla1.  
  
FIELD-SYMBOLS <fs_tabla>.  
  
ASSIGN lt_tabla1 TO <fs_tabla>.  
lt_tabla2 = <fs_tabla>.  
  
LOOP AT lt_tabla2 INTO lv_str.  
  WRITE / lv_str.  
ENDLOOP.
```
4. Ordenar tabla.
```abap
REPORT ZFIELDSYMBOLS_4_FF.  
DATA: lt_tabla1 TYPE TABLE OF string,  
      lv_str    TYPE string.  
  
lv_str = 'Juanito'.  
APPEND lv_str TO lt_tabla1.  
  
lv_str = 'Pepita'.  
APPEND lv_str TO lt_tabla1.  
  
lv_str = 'Fulanito'.  
APPEND lv_str TO lt_tabla1.  
  
FIELD-SYMBOLS <fs_tabla>.  
  
ASSIGN lt_tabla1 TO <fs_tabla>.  
sort <fs_tabla>.  
  
LOOP AT lt_tabla1 INTO lv_str.  
  WRITE / lv_str.  
ENDLOOP.
```
5. Buscar y modificar un valor.
```abap
REPORT ZFIELDSYMBOLS_5_FF.  
DATA: lt_tabla1 TYPE TABLE OF string,  
      lv_str    TYPE string,  
      lv_buscado type string,  
      lv_nuevo type string.  
  
lv_str = 'Juanito'.  
APPEND lv_str TO lt_tabla1.  
  
lv_str = 'Pepita'.  
APPEND lv_str TO lt_tabla1.  
  
lv_str = 'Fulanito'.  
APPEND lv_str TO lt_tabla1.  
  
lv_buscado = 'Pepita'.  
lv_nuevo = 'Francesco'.  
  
FIELD-SYMBOLS <fs_tabla>.  
  
LOOP AT lt_tabla1 ASSIGNING <fs_tabla>.  
  IF <fs_tabla> = lv_buscado.  
    " Reemplazar el valor si coincide  
    <fs_tabla> = lv_nuevo.  
  ENDIF.  
ENDLOOP.  
  
LOOP AT lt_tabla1 INTO lv_str.  
  WRITE / lv_str.  
ENDLOOP.
```
sel -> sub con subrutina con loop at screen. incluye radiobuttons y parameters
sub -> métodos
principal -> mostrar en pantalla
top -> variables globales


### Clases y métodos.

1. Llamar a un método.
```
REPORT ZCLASES_01_FF.  
  
DATA: alv_grid TYPE REF TO cl_gui_alv_grid,  
      lt_hola type table of string.  
CREATE OBJECT alv_grid  
  EXPORTING  
    i_parent = cl_gui_container=>screen0.  
CALL METHOD alv_grid->set_table_for_first_display  
*  EXPORTING  
*    i_buffer_active               =  
*    i_bypassing_buffer            =  
*    i_consistency_check           =  
*    i_structure_name              =  
*    is_variant                    =  
*    i_save                        =  
*    i_default                     = 'X'  
*    is_layout                     =  
*    is_print                      =  
*    it_special_groups             =  
*    it_toolbar_excluding          =  
*    it_hyperlink                  =  
*    it_alv_graphics               =  
*    it_except_qinfo               =  
*    ir_salv_adapter               =  
  CHANGING  
    it_outtab                     = lt_hola  
*    it_fieldcatalog               =  
*    it_sort                       =  
*    it_filter                     =  
*  EXCEPTIONS  
*    invalid_parameter_combination = 1  
*    program_error                 = 2  
*    too_many_lines                = 3  
*    others                        = 4  
        .  
IF sy-subrc <> 0.  
* Implement suitable error handling here  
ENDIF.
```
* En el método file_open_dialog, los parámetros obligatorios son: file_table, que recibe un tipo filetable, y rc, que recibe un entero. Muestra un cuadro de diálogo de abrir un archivo.
* En el método file_save_dialog, los parámetros obligatorios son: filename, path y fullpath, que reciben una cadena de caracteres cada uno. Muestra un cuadro de diálogo de guardar un archivo.
* En el método gui_download, son obligatorios los parámetros filelength (i) y data_tab (standard table). Descarga datos al PC cliente.
* En gui_upload son obligatorios los mismos que en gui_download, con la adición de header (xstring). Recibe datos del PC cliente.

3. Crear una clase Empleado.
```
CLASS lcl_empleado DEFINITION.  
  PUBLIC SECTION.  
    DATA: nombre       TYPE string,  
          apellido     TYPE string,  
          edad         TYPE i,  
          puesto       TYPE string,  
          departamento TYPE string,  
          salario      TYPE p DECIMALS 2.  
    METHODS: set_nombre IMPORTING valor TYPE string,  
      set_apellido IMPORTING valor TYPE string,  
      set_edad IMPORTING valor TYPE i,  
      set_puesto IMPORTING valor TYPE string,  
      set_departamento IMPORTING valor TYPE string,  
      set_salario IMPORTING valor TYPE i.  
    METHODS: get_nombre RETURNING VALUE(resultado) TYPE string,  
      get_apellido RETURNING VALUE(resultado) TYPE string,  
      get_edad RETURNING VALUE(resultado) TYPE i,  
      get_puesto RETURNING VALUE(resultado) TYPE string,  
      get_departamento RETURNING VALUE(resultado) TYPE string,  
      get_salario RETURNING VALUE(resultado) TYPE i. "Quise hacerlo de tipo packed con 2 decimales, pero daba un error lol  
ENDCLASS.  
  
CLASS lcl_empleado IMPLEMENTATION.  
  
  METHOD set_nombre.  
    nombre = valor.  
  ENDMETHOD.  
  METHOD set_apellido.  
    apellido = valor.  
  ENDMETHOD.  
  METHOD set_edad.  
    edad = valor.  
  ENDMETHOD.  
  METHOD set_puesto.  
    puesto = valor.  
  ENDMETHOD.  
  METHOD set_departamento.  
    departamento = valor.  
  ENDMETHOD.  
  METHOD set_salario.  
    salario = valor.  
  ENDMETHOD.  
  METHOD get_nombre.  
    resultado = nombre.  
  ENDMETHOD.  
  METHOD get_apellido.  
    resultado = apellido.  
  ENDMETHOD.  
  METHOD get_edad.  
    resultado = edad.  
  ENDMETHOD.  
  METHOD get_puesto.  
    resultado = puesto.  
  ENDMETHOD.  
  METHOD get_departamento.  
    resultado = departamento.  
  ENDMETHOD.  
  METHOD get_salario.  
    resultado = salario.  
  ENDMETHOD.  
  
ENDCLASS.  
  
START-OF-SELECTION. "Sin esto me daba un error de código no accesible...  
  
  DATA(lo_empleado) = NEW lcl_empleado( ).  
  lo_empleado->set_nombre( 'Francesco' ).  
  lo_empleado->set_apellido( 'Fevoli' ).  
  lo_empleado->set_edad( 20 ).  
  lo_empleado->set_puesto( 'Desarrollador' ).  
  lo_empleado->set_departamento( 'IT' ).  
  lo_empleado->set_salario( 15000 ).  
  
  WRITE: / lo_empleado->get_nombre( ),  
           / lo_empleado->get_apellido( ),  
           / lo_empleado->get_edad( ),  
           / lo_empleado->get_puesto( ),  
           / lo_empleado->get_departamento( ),  
           / lo_empleado->get_salario( ).
```
4. Clase Producto.
```
CLASS lcl_producto DEFINITION.  
  PUBLIC SECTION.  
    DATA: codigo      TYPE string,  
          descripcion TYPE string,  
          stock       TYPE i,  
          precio      TYPE i,  
          unidad      TYPE string VALUE 'EUR'.  
  
    METHODS: set_datos IMPORTING p_codigo      TYPE string  
                                 p_descripcion TYPE string  
                                 p_stock       TYPE i  
                                 p_precio      TYPE i,  
      get_datos RETURNING VALUE(r_datos) TYPE string,  
      calcular_precio_total RETURNING VALUE(r_total) TYPE i,  
      actualizar_stock IMPORTING p_nuevo_stock TYPE i.  
ENDCLASS.  
  
CLASS lcl_producto IMPLEMENTATION.  
  METHOD set_datos.  
    codigo = p_codigo.  
    descripcion = p_descripcion.  
    stock = p_stock.  
    precio = p_precio.  
  ENDMETHOD.  
  
  METHOD get_datos.  
    DATA: stock_str  TYPE string,  
          precio_str TYPE string.  
  
    stock_str = CONV string( stock ).  
    precio_str = CONV string( precio ).  
    CONCATENATE 'Código:' codigo 'Descripción:' descripcion 'Stock:' stock_str 'Precio:' precio_Str unidad INTO r_datos SEPARATED BY space.  
  ENDMETHOD.  
  
  METHOD calcular_precio_total.  
    r_total = stock * precio.  
  ENDMETHOD.  
  
  METHOD actualizar_stock.  
    stock = p_nuevo_stock.  
  ENDMETHOD.  
ENDCLASS.  
  
START-OF-SELECTION.  
  DATA: producto1 TYPE REF TO lcl_producto,  
        producto2 TYPE REF TO lcl_producto,  
        producto3 TYPE REF TO lcl_producto,  
        datos     TYPE string,  
        total     TYPE p DECIMALS 2.  
  
  CREATE OBJECT producto1.  
  CREATE OBJECT producto2.  
  CREATE OBJECT producto3.  
  
  producto1->set_datos( p_codigo = 'P001' p_descripcion = 'Laptop' p_stock = 10 p_precio = 50 ).  
  producto2->set_datos( p_codigo = 'P002' p_descripcion = 'Mouse' p_stock = 50 p_precio = 20 ).  
  
  WRITE: / 'Datos Producto 1:'.  
  datos = producto1->get_datos( ).  
  WRITE: / datos.  
  
  WRITE: / 'Datos Producto 2:'.  
  datos = producto2->get_datos( ).  
  WRITE: / datos.  
  
  producto3 = producto1.  
  
  
  WRITE: / 'Datos Producto 3:'.  
  datos = producto3->get_datos( ).  
  WRITE: / datos.  
  
  producto3->set_datos( p_codigo = 'P004' p_descripcion = 'Monitor' p_stock = 15 p_precio = 150 ).  
  
  WRITE: / 'Datos Producto 1 después de modificar Producto 3:'.  
  datos = producto1->get_datos( ).  
  WRITE: / datos.
```
5. En el programa ZCLASES_05_XX debes crear dos clases, la de empleado y la de empleado_temporal. Ambos tendrán como atributos el número de empleado, el nombre y el salario; y los temporales contarán además con fecha de inicio y fecha de finalización. Ambos contarán con un método para establecer el salario; los temporales tendrán además, un método para establecer cuántos días tiene el contrato. Se crearán 2 empleados y 2 empleados temporales y se mostrará por pantalla el resultado de sus métodos. 
```
CLASS lcl_empleado DEFINITION.  
  PUBLIC SECTION.  
    DATA: num_empleado TYPE string,  
          nombre       TYPE string,  
          salario      TYPE p DECIMALS 2.  
  
    METHODS: set_salario IMPORTING p_salario TYPE i,  
      get_datos RETURNING VALUE(r_datos) TYPE string.  
ENDCLASS.  
  
CLASS lcl_empleado IMPLEMENTATION.  
  METHOD set_salario.  
    salario = p_salario.  
  ENDMETHOD.  
  
  METHOD get_datos.  
    DATA salario_Str TYPE string.  
    salario_str = CONV string( salario ).  
    CONCATENATE 'Empleado:' num_empleado 'Nombre:' nombre 'Salario:' salario_str INTO r_datos SEPARATED BY space.  
  ENDMETHOD.  
ENDCLASS.  
  
CLASS lcl_empleado_temporal DEFINITION INHERITING FROM lcl_empleado.  
  PUBLIC SECTION.  
    DATA: fecha_inicio TYPE d,  
          fecha_fin    TYPE d.  
  
    METHODS: set_fechas IMPORTING p_inicio TYPE d p_fin TYPE d,  
      calcular_dias_contrato RETURNING VALUE(r_dias) TYPE i,  
      get_datos_temp RETURNING VALUE(r_datos) TYPE string.  
ENDCLASS.  
  
CLASS lcl_empleado_temporal IMPLEMENTATION.  
  METHOD set_fechas.  
    fecha_inicio = p_inicio.  
    fecha_fin = p_fin.  
  ENDMETHOD.  
  
  METHOD calcular_dias_contrato.  
    r_dias = fecha_fin - fecha_inicio.  
  ENDMETHOD.  
  
  METHOD get_datos_temp.  
    DATA: base_datos TYPE string.  
    base_datos = me->get_datos( ).  
  
    CONCATENATE base_datos 'Fecha Inicio:' fecha_inicio 'Fecha Fin:' fecha_fin INTO r_datos SEPARATED BY space.  
  ENDMETHOD.  
ENDCLASS.  
  
START-OF-SELECTION.  
  DATA: empleado1 TYPE REF TO lcl_empleado,  
        empleado2 TYPE REF TO lcl_empleado,  
        temp1     TYPE REF TO lcl_empleado_temporal,  
        temp2     TYPE REF TO lcl_empleado_temporal,  
        datos     TYPE string,  
        dias      TYPE i.  
  
  CREATE OBJECT empleado1.  
  CREATE OBJECT empleado2.  
  CREATE OBJECT temp1.  
  CREATE OBJECT temp2.  
  
  empleado1->num_empleado = '1'.  
  empleado1->nombre = 'Juan'.  
  empleado1->set_salario( 2500 ).  
  
  empleado2->num_empleado = '2'.  
  empleado2->nombre = 'Ana'.  
  empleado2->set_salario( 2700 ).  
  
  temp1->num_empleado = '3'.  
  temp1->nombre = 'Luis'.  
  temp1->set_salario( 1800 ).  
  temp1->set_fechas( p_inicio = '20240301' p_fin = '20240630' ).  
  
  temp2->num_empleado = '4'.  
  temp2->nombre = 'Marta'.  
  temp2->set_salario( 1900 ).  
  temp2->set_fechas( p_inicio = '20240401' p_fin = '20240731' ).  
  
  WRITE: / 'Datos Empleado 1:'.  
  datos = empleado1->get_datos( ).  
  WRITE: / datos.  
  
  WRITE: / 'Datos Empleado 2:'.  
  datos = empleado2->get_datos( ).  
  WRITE: / datos.  
  
  " Mostrar datos de los empleados temporales  
  WRITE: / 'Datos Empleado Temporal 1:'.  
  datos = temp1->get_datos_temp( ).  
  WRITE: / datos.  
  dias = temp1->calcular_dias_contrato( ).  
  WRITE: / 'Días de contrato:', dias.  
  
  WRITE: / 'Datos Empleado Temporal 2:'.  
  datos = temp2->get_datos_temp( ).  
  WRITE: / datos.  
  dias = temp2->calcular_dias_contrato( ).  
  WRITE: / 'Días de contrato:', dias.
```
6. En el programa ZCLASES_06_XX desarrollar un sistema de gestión de inventario para una tienda en línea. Cuando un cliente realiza una compra, se debe actualizar el inventario del producto disponibles (Clase producto). Sin embargo, si un producto está por debajo de un cierto umbral de stock, se debe enviar una notificación al departamento de compras para reabastecer el producto (evento que recoge la clase tienda).

```
CLASS lcl_producto DEFINITION.  
  PUBLIC SECTION.  
    DATA: codigo      TYPE string,  
          descripcion TYPE string,  
          stock       TYPE i,  
          precio      TYPE p DECIMALS 2,  
          umbral      TYPE i.  
  
    EVENTS stock_bajo EXPORTING VALUE(producto) TYPE string.  
  
    METHODS: set_datos IMPORTING  
                         p_codigo      TYPE string  
                         p_descripcion TYPE string  
                         p_stock       TYPE i  
                         p_precio      TYPE i  
                         p_umbral      TYPE i,  
      get_datos RETURNING VALUE(r_datos) TYPE string,  
      actualizar_stock IMPORTING p_cantidad TYPE i.  
ENDCLASS.  
  
CLASS lcl_producto IMPLEMENTATION.  
  METHOD set_datos.  
    codigo = p_codigo.  
    descripcion = p_descripcion.  
    stock = p_stock.  
    precio = p_precio.  
    umbral = p_umbral.  
  ENDMETHOD.  
  
  METHOD get_datos.  
    DATA: stock_str  TYPE string,  
          precio_str TYPE string.  
    stock_str = CONV string( stock ).  
    precio_str = CONV string( precio ).  
    CONCATENATE 'Código:' codigo 'Descripción:' descripcion 'Stock:' stock_str 'Precio:' precio_str INTO r_datos SEPARATED BY space.  
  ENDMETHOD.  
  
  METHOD actualizar_stock.  
    IF stock >= p_cantidad.  
      stock = stock - p_cantidad.  
      IF stock < umbral.  
        RAISE EVENT stock_bajo EXPORTING producto = descripcion.  
      ENDIF.  
    ELSE.  
      WRITE: / 'Stock insuficiente para la venta.'.  
    ENDIF.  
  ENDMETHOD.  
ENDCLASS.  
  
CLASS lcl_tienda DEFINITION.  
  PUBLIC SECTION.  
    METHODS manejar_stock_bajo FOR EVENT stock_bajo OF lcl_producto IMPORTING producto.  
ENDCLASS.  
  
CLASS lcl_tienda IMPLEMENTATION.  
  METHOD manejar_stock_bajo.  
    WRITE: / 'Reabastecer producto:', producto.  
  ENDMETHOD.  
ENDCLASS.  
  
START-OF-SELECTION.  
  DATA: producto1 TYPE REF TO lcl_producto,  
        tienda    TYPE REF TO lcl_tienda.  
  
  CREATE OBJECT producto1.  
  CREATE OBJECT tienda.  
  
  SET HANDLER tienda->manejar_stock_bajo FOR producto1.  
  
  producto1->set_datos( p_codigo = 'P001' p_descripcion = 'Laptop' p_stock = 10 p_precio = 500 p_umbral = 3 ).  
  
  WRITE: / 'Producto antes de la venta:'.  
  WRITE: / producto1->get_datos( ).  
  
  " Simular una venta de 8 unidades "  
  producto1->actualizar_stock( p_cantidad = 8 ).  
  
  WRITE: / 'Producto después de la venta:'.  
  WRITE: / producto1->get_datos( ).
```

### Open SQL
1. Tablas y estructuras.![[Pasted image 20250401110314.png]]
```abap
TABLES: zsql_01_ff.  
  
DATA:  
  ls_persona TYPE zsql_01_ff,  
  lt_persona TYPE TABLE OF zsql_01_ff.  
  
ls_persona-nombre = 'Juanito'.  
ls_persona-apellido = 'García'.  
ls_persona-edad = 16.  
ls_persona-direccion = 'Calle Cristo, 5'.  
  
APPEND ls_persona TO lt_persona.  
  
ls_persona-nombre = 'Pedro'.  
ls_persona-apellido = 'Pérez'.  
ls_persona-edad = 25.  
ls_persona-direccion = 'Avinguda de '.  
  
APPEND ls_persona TO lt_persona.  
  
ls_persona-nombre = 'Pepito'.  
ls_persona-apellido = 'Ermenegildo'.  
ls_persona-edad = 40.  
ls_persona-direccion = 'Calle Ayer'.  
  
APPEND ls_persona TO lt_persona.  
  
modify zsql_01_ff from TABLE lt_persona.  
  
LOOP AT lt_persona INTO ls_persona.  
  WRITE: / ls_persona-nombre, ls_persona-apellido, ls_persona-direccion, ls_persona-edad.  
ENDLOOP.  
  
  
READ TABLE lt_persona INTO ls_persona INDEX 2.  
IF sy-subrc = 0.  
  ls_persona-nombre = 'Amparo'.  
  ls_persona-edad = 75.  
  MODIFY lt_persona INDEX 2 FROM ls_persona.  
  UPDATE zsql_01_ff SET nombre = 'Amparo', edad = 75 WHERE nombre = 'María'.  
  COMMIT WORK.  
ENDIF.  
  
WRITE: /  'Registros después de traer a Amparito :D:'.  
LOOP AT lt_persona INTO ls_persona.  
  WRITE: / ls_persona-nombre, ls_persona-apellido, ls_persona-direccion, ls_persona-edad.  
ENDLOOP.  
  
READ TABLE lt_persona INTO ls_persona WITH KEY edad = 75.  
IF sy-subrc = 0.  
  WRITE: / 'Registro con edad 75 encontrado:', ls_persona-nombre, ls_persona-edad.  
ENDIF.  
  
DELETE FROM zsql_01_ff WHERE nombre = 'Amparo'.  
COMMIT WORK.  
  
DELETE lt_persona WHERE nombre = 'Amparo'.  
  
WRITE: / 'Registros después de eliminar a Amparito :(:'.  
LOOP AT lt_persona INTO ls_persona.  
  WRITE: / ls_persona-nombre, ls_persona-apellido, ls_persona-direccion, ls_persona-edad.  
ENDLOOP.
```

2. Consulta básica
```abap
DATA: lt_spfli TYPE TABLE OF spfli,  
      ls_spfli TYPE spfli.  
  
SELECT * FROM spfli INTO TABLE @lt_spfli WHERE cityfrom = 'FRANKFURT'.  
  
  LOOP AT lt_spfli INTO ls_spfli.  
    WRITE: / 'CARRID: ', ls_spfli-carrid,  
           ' CONNID: ', ls_spfli-connid,  
           ' COUNTRYFR: ', ls_spfli-countryfr,  
           ' COUNTRYTO: ', ls_spfli-countryto.  
  ENDLOOP.
```
3. Where y order by
```abap
DATA: lt_spfli TYPE TABLE OF spfli,  
      lv_message TYPE string.  
  
SELECT *  
  INTO TABLE @lt_spfli  
  FROM spfli  
  WHERE cityto = 'NEW YORK'  
    AND distance < 4000  
  ORDER BY distance ASCENDING.  
  
IF sy-subrc = 0.  
  LOOP AT lt_spfli INTO DATA(ls_spfli).  
    WRITE: / 'CARRID:', ls_spfli-carrid,  
           'CONNID:', ls_spfli-connid,  
           'COUNTRYFR:', ls_spfli-countryfr,  
           'COUNTRYTO:', ls_spfli-countryto,  
           'DISTANCE:', ls_spfli-distance,  
           'DISTID:', ls_spfli-distid.  
  ENDLOOP.  
ELSE.  
  lv_message = 'No se encontraron vuelos.'.  
  WRITE: / lv_message.  
ENDIF.
```
4. Consultas de agregación y agrupación.
```abap
TYPES: BEGIN OF ty_result,  
         airpto TYPE spfli-airpto,  
         total  TYPE i,  
       END OF ty_result.  
  
DATA: lt_results TYPE TABLE OF ty_result,  
      lv_message TYPE string.  
  
SELECT s~airpto AS airpto, COUNT( b~bookid ) AS total  
  FROM spfli AS s  
  INNER JOIN sbook AS b  
  ON s~carrid = b~carrid  
  AND s~connid = b~connid  
  GROUP BY s~airpto  
  ORDER BY total DESCENDING  
  INTO TABLE @lt_results.  
  
LOOP AT lt_results INTO DATA(ls_result).  
  WRITE: / 'Aeropuerto:', ls_result-airpto,  
         'Total asientos:', ls_result-total.  
ENDLOOP.
```
5. Join
```abap
DATA: lt_flights TYPE TABLE OF spfli,  
      lt_bookings TYPE TABLE OF sbook,  
      lv_carrier TYPE spfli-carrid,  
      lv_connid TYPE spfli-connid,  
      lv_fldate TYPE sbook-fldate,  
      lv_reservas TYPE i.  
  
lv_carrier = 'AZ'.  
  
SELECT a~carrid, a~connid, b~fldate, COUNT( b~bookid ) AS reservas  
  FROM spfli AS a  
  INNER JOIN sbook AS b  
    ON a~carrid = b~carrid  
    AND a~connid = b~connid  
  WHERE a~carrid = @lv_carrier  
  GROUP BY a~carrid, a~connid, b~fldate  
  INTO (@lv_carrier, @lv_connid, @lv_fldate, @lv_reservas).  
  
  WRITE: / 'Aerolinea:', lv_carrier,  
           'Conexion:', lv_connid,  
           'Fecha de vuelo:', lv_fldate,  
           'Numero de reservas:', lv_reservas.  
  
ENDSELECT.
```
6. Consultas con operaciones.
```abap
DATA: lt_flights TYPE TABLE OF sflight,  
      lv_carrid TYPE sflight-carrid,  
      lv_connid TYPE sflight-connid,  
      lv_fldat TYPE sflight-fldate,  
      lv_seatsmax TYPE sflight-seatsmax,  
      lv_seatsocc TYPE sflight-seatsocc,  
      lv_seat_diff TYPE i.  
  
SELECT carrid, connid, fldate, seatsmax, seatsocc, ( seatsmax - seatsocc ) AS seat_diff  
  INTO (@lv_carrid, @lv_connid, @lv_fldat, @lv_seatsmax, @lv_seatsocc, @lv_seat_diff)  
  FROM sflight  
  WHERE seatsmax IS NOT NULL  
  AND seatsocc IS NOT NULL.  
  
  WRITE: / 'Aerolinea:', lv_carrid,  
           'Conexion:', lv_connid,  
           'Fecha de vuelo:', lv_fldat,  
           'Max. de sitios:', lv_seatsmax,  
           'Sitios ocupados:', lv_seatsocc,  
           'Diferencia:', lv_seat_diff.  
  
ENDSELECT.
```
7. Repaso de consultas.
```abap
TYPES: BEGIN OF ty_flight_info,  
         company    TYPE sflight-carrid,  
         connection TYPE sflight-connid,  
         flight_date TYPE sflight-fldate,  
         price      TYPE sflight-price,  
         currency   TYPE sflight-currency,  
         planetype  TYPE sflight-planetype,  
         seatmax    TYPE sflight-seatsmax,  
         seatoc     TYPE sflight-seatsocc,  
       END OF ty_flight_info.  
  
DATA: lt_flights TYPE TABLE OF ty_flight_info,  
      ls_flight  TYPE ty_flight_info,  
      lv_carrid  TYPE sflight-carrid.  
  
PARAMETERS: p_carrid TYPE sflight-carrid OBLIGATORY.  
  
lv_carrid = p_carrid.  
  
SELECT carrid, connid, fldate, price, currency, planetype, seatsmax, seatsocc  
  INTO TABLE @lt_flights  
  FROM sflight  
  WHERE carrid = @lv_carrid.  
  
IF lt_flights IS INITIAL.  
  WRITE: / 'No se encontraron vuelos para la aerolínea:', lv_carrid.  
ELSE.  
  LOOP AT lt_flights INTO ls_flight.  
    WRITE: / 'Compañía:', ls_flight-company,  
             'Conexión:', ls_flight-connection,  
             'Fecha:', ls_flight-flight_date,  
             'Precio:', ls_flight-price,  
             'Moneda:', ls_flight-currency,  
             'Avión:', ls_flight-planetype,  
             'Asientos Máx.:', ls_flight-seatmax,  
             'Asientos Ocupados:', ls_flight-seatoc.  
  ENDLOOP.  
ENDIF.
```
8. COnsulta y modificación.
```abap
DATA: ls_persona TYPE zsql_01_ff,  
      lt_persona TYPE TABLE OF zsql_01_ff.  
  
ls_persona-nombre    = 'Juan'.  
ls_persona-apellido  = 'Ortíz'.  
ls_persona-direccion = 'Calle del Pez 39'.  
ls_persona-edad      = 30.  
INSERT INTO zsql_01_ff VALUES ls_persona.  
WRITE: / 'Registro insertado:', ls_persona-nombre, ls_persona-apellido.  
  
ls_persona-nombre    = 'María'.  
ls_persona-apellido  = 'López'.  
ls_persona-direccion = 'Av. de la Libertad'.  
ls_persona-edad      = 25.  
INSERT INTO zsql_01_ff VALUES ls_persona.  
WRITE: / 'Registro insertado:', ls_persona-nombre, ls_persona-apellido.  
  
ls_persona-nombre    = 'Carlos'.  
ls_persona-apellido  = 'Gómez'.  
ls_persona-direccion = 'Plaza Mayor 55'.  
ls_persona-edad      = 40.  
INSERT INTO zsql_01_ff VALUES ls_persona.  
WRITE: / 'Registro insertado:', ls_persona-nombre, ls_persona-apellido.  
  
SELECT SINGLE * FROM zsql_01_ff INTO ls_persona WHERE nombre = 'Juan'.  
IF sy-subrc = 0.  
  ls_persona-direccion = 'Carrer de Navas 259'.  
  MODIFY zsql_01_ff FROM ls_persona.  
  WRITE: / 'Registro modificado:', ls_persona-nombre, ls_persona-apellido, / 'Nueva dirección:', ls_persona-direccion.  
ENDIF.  
  
CLEAR ls_persona.  
ls_persona-nombre    = 'Ana'.  
ls_persona-apellido  = 'Martínez'.  
ls_persona-direccion = 'Calle de Válgame Dios 55'.  
ls_persona-edad      = 35.  
MODIFY zsql_01_ff FROM ls_persona.  
WRITE: / ls_persona-nombre, ls_persona-apellido.  
DELETE FROM zsql_01_ff WHERE nombre = 'Carlos'.  
IF sy-subrc = 0.  
  WRITE: / 'Registro eliminado.'.  
ENDIF.
```

Ejercicio 5: 
Desarrolla un programa en ABAP que permita gestionar un inventario de productos y realizar pedidos. El programa debe permitir que el usuario agregue productos hasta que decida finalizar el pedido, para hacer esta tienes que investigar el uso de botones.

```abap
SELECTION-SCREEN PUSHBUTTON /10(20) boton1 USER-COMMAND add.  
SELECTION-SCREEN PUSHBUTTON /40(20) boton2 USER-COMMAND end.
MODULE user_command_100 INPUT.  
  CASE sy-ucomm.  
    WHEN 'ADD'.  
      lo_inventario->agregar_producto( iv_id = p_cod iv_nombre = p_nom iv_precio = p_precio ).  
    WHEN 'END'.  
      lo_inventario->finalizar_pedido( ).  
  ENDCASE.  
ENDMODULE.
```
