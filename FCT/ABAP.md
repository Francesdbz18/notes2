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
