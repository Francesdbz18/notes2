[Acquiring Core ABAP Skills](https://learning.sap.com/learning-journeys/acquire-core-abap-skills)
![[Pasted image 20250324105634.png]]
### Transacciones
- SE38: Editor de código
- SE37: Módulo funciones
- SE80: Navegador de objetos
- SE11: Diccionario de datos, tablas
- SE16: BD (deprecated, use SE11 & SE16N)
- SE16N: BD
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

### Field symbols
LOOP AT *tabla* ASSIGNING *field-symbols*
LOOP AT screen: modificar atributos de elementos por pantalla.

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