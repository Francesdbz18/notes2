- Forma de modularizar proyectos.
- Reduce el acoplamiento, aumenta la capacidad de prueba y mejora el mantenimiento del código.
- Un código con acoplamiento fuerte es poco flexible, difícil de probar y tiene responsabilidades mezcladas, al contener lógica de negocio y lógica de construcción en una misma clase.
- Inyectando dependencias se mejora la flexibilidad (permite cambiar las dependencias por otras) y no se mezclan responsabilidades en las clases.

#### Tipos de inyección
- Por constructor (más recomendable)
- Por método setter
- Por campo (con frameworks y anotaciones)
Si no es posible la inyección por constructor, es una práctica típica el uso de un método aparte para la inyección de dependencias.