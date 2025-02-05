Ejercicios con XPath y XQuery Dada la colección empresa en eXist-db que contiene los documentos empleados.xml y departamentos.xml 
`<empleado emp_no="1"> <apellido>Martinez</apellido> <oficio>contable</oficio> <dir>calle Marte 23</dir> <fecha_alt>10-03-2000</fecha_alt> <dept_no>10</dept_no> <salario>1000.33</slario> </empleado>`
`<departamentos> <dpto dpto_no="1"> <dnombre>Contabilidad</dnombre> <loc>plata 1</oficio> </dpto> <dpto dpt_no="10"> <dnombre>Comunicaciones</dnombre> <loc>planta 2</loc> </dpto> <dpto dpto_no="12"> <dnombre>Informática</dnombre> <loc>planta 1</loc> </departamentos>`
### Consultas XPath:

1. **Obtener los nombres de los departamentos:**

```xpath
//departamentos/dpto/dnombre
```

2. **Obtener todas las localizaciones:**

```xpath
//departamentos/dpto/loc
```

1. **Obtener los números de departamento de la colección:**

```xpath
//departamentos/dpto/@dpto_no
```

2. **Obtener todos los empleados del departamento 10:**

```xpath
//empleados/empleado[dept_no=10]
```

3. **Obtener los apellidos de los empleados que no son contables:**

```xpath
//empleados/empleado[oficio!='contable']/apellido
```

4. **Obtener los empleados con salario mayor a 800 euros:**

```xpath
//empleados/empleado[salario>800]/apellido
```

5. **Obtener la fecha de alta del segundo empleado:**

```xpath
//empleados/empleado[2]/fecha_alt
```

6. **Devolver los datos del primer departamento:**

```xpath
//departamentos/dpto[1]
```

7. **Obtener el apellido de los empleados cuya posición es menor que dos:**

```xpath
//empleados/empleado[position()<2]/apellido
```

8. **Obtener el número de departamentos:**

```xpath
//departamentos/dpto
```

9. **Obtener el salario total pagado por la empresa a todos los empleados:**

```xpath
sum(//empleados/empleado/salario)
```

10. **Obtener el apellido del empleado con mayor salario:**

```xpath
//empleados/empleado[salario=max(//empleados/empleado/salario)]/apellido
```

11. **Obtener el salario medio pagado por la empresa:**

```xpath
avg(//empleados/empleado/salario)
```

12. **Obtener los nombres de los departamentos que comienzan por 'c':**

```xpath
//departamentos/dpto[dnombre[starts-with(., 'C')]]/dnombre
```

13. **Obtener la localización del departamento de número 12:**

```xpath
//departamentos/dpto[@dpto_no=12]/loc
```

---

### Consultas XQuery:

14. **Obtener los apellidos de todos los empleados junto con su oficio:**

```xquery
for $empleado in //empleados/empleado
return <empleado>
           <apellido>{ $empleado/apellido }</apellido>
           <oficio>{ $empleado/oficio }</oficio>
       </empleado>
```

15. **Obtener los números y nombres de todos los departamentos:**

```xquery
for $dpto in //departamentos/dpto
return <departamento>
           <dpto_no>{ $dpto/@dpto_no }</dpto_no>
           <dnombre>{ $dpto/dnombre }</dnombre>
       </departamento>
```

16. **Obtener los nombres de los empleados que sean telefonistas:**

```xquery
for $empleado in //empleados/empleado
where $empleado/oficio = 'telefonista'
return <empleado>{ $empleado/apellido }</empleado>
```

17. **Obtener los nombres de los departamentos y el número de empleados que tiene cada uno:**

```xquery
for $dpto in //departamentos/dpto
let $empleados := //empleados/empleado[dept_no = $dpto/@dpto_no]
return <departamento>
           <dnombre>{ $dpto/dnombre }</dnombre>
           <num_empleados>{ count($empleados) }</num_empleados>
       </departamento>
```

18. **Obtener los nombres de los departamentos y el salario medio de sus empleados redondeado:**

```xquery
for $dpto in //departamentos/dpto
let $empleados := //empleados/empleado[dept_no = $dpto/@dpto_no]
let $salario_medio := avg($empleados/salario)
return <departamento>
           <dnombre>{ $dpto/dnombre }</dnombre>
           <salario_medio>{ round($salario_medio) }</salario_medio>
       </departamento>
```

19. **Obtener los nombres de los empleados que trabajan en el departamento de Informática:**

```xquery
for $empleado in //empleados/empleado
let $dpto := //departamentos/dpto[dnombre = 'Informática']
where $empleado/dept_no = $dpto/@dpto_no
return <empleado>{ $empleado/apellido }</empleado>
```

20. **Obtener los nombres de los oficios que empiezan por 't':**

```xquery
for $empleado in //empleados/empleado
where starts-with($empleado/oficio, 't')
return <oficio>{ $empleado/oficio }</oficio>
```

21. **Obtener los nombres de los oficios y el número de empleados de cada oficio:**

```xquery
for $oficio in distinct-values(//empleados/empleado/oficio)
let $empleados := //empleados/empleado[oficio = $oficio]
return <oficio>
           <nombre>{ $oficio }</nombre>
           <num_empleados>{ count($empleados) }</num_empleados>
       </oficio>
```

22. **Obtener por cada departamento el nombre del empleado que más gana:**

```xquery
for $dpto in //departamentos/dpto
let $empleados := //empleados/empleado[dept_no = $dpto/@dpto_no]
let $max_salario := max($empleados/salario)
let $empleado_max := $empleados[salario = $max_salario]
return <departamento>
           <dnombre>{ $dpto/dnombre }</dnombre>
           <empleado>{ $empleado_max/apellido }</empleado>
       </departamento>
```

23. **Obtener la planta donde se ubican más departamentos:**

```xquery
let $locaciones := //departamentos/dpto/loc
let $mas_comun := max((for $loc in distinct-values($locaciones) return count($locations[. = $loc])))

return <planta>
           <localizacion>{ $locaciones[. = $mas_comun] }</localizacion>
           <num_departamentos>{ $mas_comun }</num_departamentos>
       </planta>
```