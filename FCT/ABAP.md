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
2. Declarar 2 strings, concatenarlas, imprimir substrings de cada una y concatenar los substrings.
3. 