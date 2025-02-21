##### Jetpack Compose
- Fases de Jetpack Compose
- Composición/Recomposición 
- Características de la Recomposición (omisiones, optimista, frecuencia, paralelo, orden) 
- Datos/Eventos: Arriba-abajo y abajo-arriba, respectivamente.
##### Asignación de variables y paso de parámetros por valor o por referencia

##### Funciones Stateless/Stateful

##### Callbacks

##### State hoisting

##### State y Composition
 - val mutableState = remember { mutableStateOf(default) } 
 - var value by remember { mutableStateOf(default) } 
 - val (value, setValue) = remember { mutableStateOf(default) }

##### Unidirectional Data Flow

##### Lista de Modificadores en Compose

##### Activities
- Concepto
- Lifecycle

##### Theming

##### Navigation
- Principios de navegación 
- Conceptos clave (Controller, Host, Graph, Destination, Route)
- Cómo crear un controlador de navegación 
- Navegación con funciones composable. 
- Gráfico de navegación 
- Cómo navegar a un destino 
- Bottom navigation 
- Navigation y ViewModels
##### ViewModel
- El ciclo de vida de un ViewModel 
- Por qué son necesarios los ViewModels 
- Implementación de ViewModels con estados de Activity
##### Empaquetamiento y distribución de aplicaciones
- APK
- Firma de software: claves asimétricas (pública/privada), entidad de certificación, hash
##### Ciclo de vida, documentación y pruebas de un proyecto de desarrollo

##### Interfaces naturales de usuario
RA2 - Lenguajes naturales: se pueden recibir lenguajes naturales como entrada (sí.)