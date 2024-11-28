**a) Se han identificado situaciones en las que resulte útil la utilización de varios hilos en un programa.**
Un hilo (thread), hebra, proceso ligero o subproceso es una secuencia de código en ejecución dentro de un proceso que puede ser ejecutada por un sistema operativo. Los hilos no tienen existencia independiente fuera de los procesos.
El uso de los hilos es muy diverso. Se pueden usar cuando un programa tiene que realizar tareas simultáneamente: 
- Un programa controla sensores en una fábrica.
- Una cola de impresión debe seguir recogiendo documentos mientras se imprime en otro hilo.
- Un procesador de textos puede tener un hilo comprobando la gramática del texto y otro hilo guardando en disco cada cierto tiempo.
- Un servidor web atiende a cada cliente en un hilo diferente.

**i) Se ha analizado el contexto de ejecución de los hilos**
El análisis del contexto de ejecución de los hilos es una parte crucial de la programación concurrente, especialmente en sistemas multitarea o de multiprocesamiento, donde varios hilos pueden ejecutarse simultáneamente, compartiendo recursos del sistema como la CPU, memoria y otros dispositivos. En este sentido, el "contexto de ejecución" de un hilo hace referencia a todos los elementos que definen su estado y su capacidad para ejecutarse. Estos incluyen, pero no se limitan a:

1. **Registros del procesador**: Los hilos utilizan los registros del procesador para ejecutar instrucciones. El contexto de un hilo incluye los valores actuales en estos registros, que permiten la reanudación del hilo en el punto exacto donde se interrumpió.
    
2. **Pila (Stack)**: Cada hilo tiene su propia pila, que es donde se almacenan las variables locales, los parámetros de las funciones y las direcciones de retorno. La pila es crucial para el flujo de ejecución del hilo.
    
3. **Program Counter (PC)**: Es el puntero a la siguiente instrucción que el hilo debe ejecutar. El contexto de ejecución también incluye el valor del contador de programa en el momento de la interrupción.
    
4. **Registros de estado del hilo**: Incluyen información sobre el estado del hilo (por ejemplo, si está en ejecución, en espera, bloqueado, etc.) y otras variables relacionadas con su administración.
    
5. **Memoria**: Aunque los hilos pueden compartir la memoria, cada hilo tiene una parte de la memoria asignada para su propio uso (por ejemplo, la pila). La memoria compartida puede involucrar el uso de mecanismos de sincronización para evitar condiciones de carrera.
    
6. **Prioridad**: En sistemas con planificación de hilos basada en prioridad, el contexto también incluye la prioridad asignada al hilo, que puede influir en su tiempo de ejecución.
    

### Contexto de ejecución en sistemas multitarea:

En sistemas multitarea, el contexto de un hilo se guarda cuando el sistema operativo realiza un _cambio de contexto_ (context switch) de un hilo a otro. Este proceso implica:

1. **Guardar el contexto del hilo actual**: Antes de que el procesador comience a ejecutar otro hilo, el sistema operativo guarda el contexto del hilo en ejecución (en la memoria o en registros especiales).
    
2. **Cargar el contexto del nuevo hilo**: El sistema operativo luego recupera el contexto de un hilo diferente desde su última ejecución, permitiéndole reanudar su tarea desde el punto exacto en que fue suspendido.
    

Este proceso de cambio de contexto tiene un coste en términos de tiempo de CPU, lo que significa que el rendimiento de la aplicación puede verse afectado si el sistema realiza demasiados cambios de contexto innecesarios.

### Importancia del análisis del contexto de ejecución:

El análisis de los contextos de ejecución es fundamental para:

- **Optimización del rendimiento**: Minimizar el tiempo de cambio de contexto y asegurarse de que los hilos se programen eficientemente.
- **Detección de errores**: Ayudar en la detección de errores relacionados con la concurrencia, como condiciones de carrera, bloqueos y fallos de sincronización.
- **Gestión de recursos**: Garantizar que los hilos utilicen los recursos del sistema de manera adecuada, sin interferir entre sí o corromper los datos compartidos.

En resumen, analizar el contexto de ejecución de los hilos permite gestionar la concurrencia de manera eficiente, garantizando que los hilos compartan recursos de manera segura y optimizando el rendimiento del sistema.

**j) Se han analizado librerías específicas del lenguaje de programación que permiten la programación multihilo.**

Hay dos formas en Java de crear hilos: extendiendo la clase Thread o implementando la interfaz Runnable. 
La clase THREAD. Al extender Thread debemos sobreescribir el método run(). La clase Thread define también los métodos start() y stop() (en desuso) para iniciar y parar la ejecución del hilo. La forma general de declarar un hilo es: Para crear un hilo con las características de NombreHilo escribiríamos: NombreHilo h = new NombreHilo(); Y para iniciarlo: h.start();
Todo hilo en Java debe formar parte de un grupo. Por defecto (si no se especifica en el constructor) los hilos serán miembros del grupo main, que se crea cuando se arranca la aplicación. La clase ThreadGroup se puede usar para manejar grupos de hilos en las aplicaciones Java. La clase Thread tiene constructores en los que se puede especificar el grupo del hilo en el momento de instanciarlo. En el siguiente ejemplo se crea un grupo de hilos de nombre Grupo de hilos. A continuación se crean tres hilos usando el constructor de la clase Thread: Thread(ThreadGroup grupo, Runnable destino, String nombre)
Hay dos formas en Java de crear hilos: extendiendo la clase Thread o implementando la interfaz Runnable. La interfaz RUNNABLE. Si queremos añadir la funcionalidad de hilo a una clase que deriva de otra clase distinta de Thread podemos usar la interfaz Runnable. Por ejemplo, para añadir la funcionalidad de hilo a una aplicación con un Jpanel de Swing definimos la clase como: public class Reloj extends Jpanel implements Runnable {} La interfaz Runnable tiene un único método, el método run(). Éste es ejecutado por el objeto hilo asociado. Para declarar un hilo implementando la interfaz Runnable: 2.3.- Clases para la creación de hilos. Para crear un objeto hilo de tipo NombreHilo escribiríamos: NombreHilo h = new NombreHilo(); Y lo iniciaríamos con el método start(): new Thread(h).start(); O bien lanzaríamos el hilo en dos pasos: Thread h1 = new Thread(h); h1.start(); O en un paso todo: new Thread(new NombreHilo()).start();

**k) Se han reconocido los problemas derivados de la compartición de información entre los hilos de un mismo proceso.**

La compartición de información entre hilos dentro de un mismo proceso puede generar diversos problemas debido a la naturaleza concurrente de los hilos. Estos problemas surgen principalmente cuando varios hilos acceden a los mismos recursos o datos sin un control adecuado, lo que puede afectar la coherencia de los datos o incluso causar errores en la ejecución del programa. Algunos de los principales problemas derivados de la compartición de información entre hilos son:
###### 1. **Condiciones de carrera (Race Conditions)**

Una **condición de carrera** ocurre cuando dos o más hilos intentan modificar o leer el mismo dato al mismo tiempo sin la debida sincronización. Esto puede dar lugar a resultados impredecibles o incorrectos, ya que el resultado depende del orden en que se realicen las operaciones. Por ejemplo:

- Un hilo podría leer el valor de una variable mientras otro hilo la está modificando, lo que podría producir un valor erróneo.
- Si dos hilos intentan incrementar el mismo contador simultáneamente, podría ocurrir que ambos lean el mismo valor y luego escriban el mismo valor actualizado, perdiendo una de las actualizaciones.

Este tipo de problema es común en programas que no implementan mecanismos de sincronización adecuados.

###### 2. **Bloqueo mutuo (Deadlock)**

El **deadlock** ocurre cuando dos o más hilos quedan atrapados esperando recursos que están siendo retenidos por otros hilos. Esto puede suceder cuando:

- Un hilo bloquea un recurso y espera otro recurso que está siendo bloqueado por un segundo hilo.
- El segundo hilo, a su vez, espera un recurso que está siendo bloqueado por el primer hilo.

Esto crea una situación en la que ninguno de los hilos puede continuar su ejecución, ya que están esperando indefinidamente por los recursos bloqueados.

###### 3. **Inanición (Starvation)**

La **inanición** se produce cuando un hilo no puede obtener acceso a los recursos que necesita para ejecutar, debido a que otros hilos con mayor prioridad siempre obtienen los recursos primero. En sistemas con planificación basada en prioridades, esto puede suceder si un hilo de baja prioridad es constantemente desplazado por otros hilos de alta prioridad, lo que lleva a que nunca tenga la oportunidad de ejecutarse.

###### 4. **Interferencia entre hilos (Thread Interference)**

La **interferencia entre hilos** se refiere a los errores que ocurren cuando múltiples hilos acceden y modifican variables compartidas de manera no controlada, lo que puede alterar su estado y provocar resultados incorrectos. Esto incluye el problema de que las actualizaciones de datos se realicen de manera desordenada o parcial, lo que puede generar inconsistencias en el programa.

###### 5. **Visibilidad de los cambios (Visibility Issues)**

En sistemas con múltiples hilos, uno de los hilos puede no ser capaz de ver las modificaciones realizadas por otros hilos debido a la **optimización de la memoria** realizada por el procesador. El procesador o la caché pueden almacenar copias locales de las variables compartidas y, como resultado, los cambios que hace un hilo pueden no ser visibles para otros hilos hasta que se sincronice la memoria. Esto puede llevar a situaciones donde los hilos trabajan con información desactualizada.

###### 6. **Acceso simultáneo a recursos limitados**

Cuando varios hilos intentan acceder a un recurso limitado, como un archivo, una base de datos o un dispositivo de entrada/salida, puede haber conflictos si no se gestionan adecuadamente. Sin un mecanismo adecuado de **bloqueo** o **sincronización**, puede ocurrir que los hilos intenten acceder a los recursos simultáneamente, lo que puede causar corrupción de datos, pérdida de información o fallos en el sistema.

###### Soluciones a los problemas de compartición de información entre hilos

Para evitar o mitigar estos problemas, es necesario aplicar estrategias de sincronización y diseño que aseguren un acceso adecuado a los recursos compartidos:

1. **Mutexes (Mutual Exclusion)**: Un mutex es un mecanismo de sincronización que garantiza que solo un hilo pueda acceder a un recurso a la vez. Es útil para evitar condiciones de carrera al acceder a datos compartidos.
    
2. **Semáforos**: Los semáforos son una herramienta que permite coordinar el acceso a los recursos limitados, asegurando que no se exceda el número de hilos que pueden acceder a un recurso en un momento dado.
    
3. **Bloqueo de lectura/escritura**: Los bloqueos de lectura/escritura permiten que múltiples hilos lean simultáneamente un recurso, pero solo uno pueda escribir en él, lo que mejora la concurrencia en escenarios donde la lectura es más frecuente que la escritura.
    
4. **Variables de condición**: Las variables de condición permiten a los hilos esperar hasta que se cumpla una condición específica antes de continuar con su ejecución, lo que es útil para evitar el deadlock y la inanición.
    
5. **Atomicidad**: Las operaciones atómicas son aquellas que se realizan en su totalidad sin ser interrumpidas. Usar operaciones atómicas para modificar variables compartidas puede ayudar a evitar condiciones de carrera.
    
6. **Volatilidad de las variables compartidas**: Declarar variables compartidas como `volatile` (en algunos lenguajes como Java o C++) asegura que los cambios realizados por un hilo sean visibles inmediatamente para otros hilos.
    
7. **Planificación adecuada de hilos**: Implementar algoritmos de planificación que eviten el bloqueo mutuo y la inanición, y que prioricen de manera justa el acceso a los recursos compartidos.
    

###### Conclusión

La compartición de información entre hilos puede ser una fuente de varios problemas que afectan la correcta ejecución de los programas concurrentes. Sin embargo, mediante el uso de técnicas adecuadas de sincronización, coordinación y planificación, estos problemas pueden ser mitigados, lo que permite a los hilos colaborar eficientemente sin interferir negativamente entre sí.
