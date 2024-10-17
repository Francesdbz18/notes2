Un proceso consiste en 
- El código ejecutable del programa 
- Los datos y la pila del programa 
- El contador del programa 
- El puntero de la pila y otros registros
- Toda la información necesaria para ejecutar el programa
Podemos definir entonces un proceso como: “Una actividad asíncrona susceptible de ser asignada a un procesador.”

CONCURRENCIA: 
- En informática: existencia simultánea de varios procesos en ejecución.
Dos procesos serán concurrentes cuando la primera instrucción de uno de ellos se ejecuta después de la primera instrucción del otro y antes de la última, es decir, hay un solapamiento o intercalado en la ejecución de las instrucciones. No es lo mismo solapamiento que ejecución simultánea, en este caso hablaríamos de programación paralela (que necesita un hardware adecuado: multiprocesador)
La programación concurrente es la disciplina que se encarga del estudio de las notaciones que permiten especificar la ejecución concurrente de las acciones de un programa, así como las técnicas para resolver los problemas inherentes a la ejecución concurrente (comunicación y sincronización).
BENEFICIOS 
• Mejor aprovechamiento de la CPU.
• Velocidad de ejecución. 
• Solución a problemas de naturaleza concurrente: 
	- Sistemas de control: Son sistemas en los que hay captura de datos, normalmente a través de sensores, análisis y actuación en función del análisis. o Tecnologías web: concurrencia de peticiones. 
	- Aplicaciones basadas en GUI: El usuario puede interactuar con la aplicación mientras la aplicación está realizando otra tarea. 
	- Simulación. 
	- SGBD: Cada usuario del sistema puede ser visto como un proceso.
En un sistema monoprocesador el sistema operativo va alternando el tiempo entre los procesos. El S.O. va alternando el tiempo entre los distintos procesos, cuando uno necesita realizar una operación de entrada salida, lo abandona y lo ocupa otro; de esta forma se aprovechan los ciclos del procesador. En la figura se ve como el tiempo de procesador se reparte entre 3 procesos, en cada momento sólo hay un proceso. Esta forma de gestionar los procesos en un sistema monoprocesador se llama multiprogramación: En un sistema monoprocesador todos los procesos comparten la misma memoria. La forma de comunicar y sincronizar procesos se realiza mediante variables compartidas.

En un sistema monoprocesador todos los procesos comparten la misma memoria. La forma de comunicar y sincronizar procesos se realiza mediante variables compartidas. En un sistema multiprocesador podemos tener un proceso en cada procesador Esto permite que exista paralelismo real entre los procesos. Estos pueden ser de memoria compartida (fuertemente acoplados) o con memoria local a cada procesador (débilmente acoplados). Se denomina multiproceso a la gestión de varios procesos dentro de un sistema multiprocesador, donde cada procesador puede acceder a una memoria común. Esta forma de trabajo es la habitual hoy en día.
La programación concurrente, aunque poderosa, presenta varios desafíos inherentes que deben ser gestionados cuidadosamente. Algunos de los problemas más comunes: 
1. Condiciones de carrera. 
2. Puntos muertos (deadlocks). 
3. Inanición (starvation). 
4. Sincronización. 
5. Escalabilidad. 
6. Depuración y pruebas.
La solución a muchos de estos problemas pasa por los hilos. Igual que un programa puede ejecutar varios procesos concurrentemente, dentro de un proceso podemos encontrarnos con varios hilos de ejecución. Un hilo es como una secuencia de control dentro de un proceso que ejecuta sus instrucciones de forma independiente.
Los hilos comparten el contexto del proceso, pero cada hilo mantiene una parte local. 
Diferencias entre proceso e hilo: 
• Los hilos comparten el espacio de memoria del usuario, muchos comparten datos y espacios de direcciones; a diferencia de los procesos que generalmente poseen espacios de memoria independientes en interactúan a través de mecanismos de comunicación dados por el sistema. 
• Hilos y procesos pueden encontrarse en diferentes estados, pero los cambios de estado en los procesos son más costosos ya que los hilos pertenecen al mismo proceso. A los hilos también se les llama procesos ligeros. 
• Se tarda menos tiempo en crear o en terminar un hilo que un proceso.
• En la comunicación entre procesos debe intervenir el núcleo del sistema, entre hilos no se necesita que intervenga el núcleo.

Un programa paralelo es un tipo de programa concurrente diseñado para ejecutarse en un sistema multiprocesador. El sistema puede ser un conjunto de equipos en red, un único equipo multiprocesador, o una combinación de ambos. El problema a resolver se divide en partes independientes de tal forma que cada elemento pueda ejecutar la parte de programa que le corresponda
En un sistema multiprocesador tenemos dos modelos dependiendo del uso de la memoria: 
• Memoria compartida: los procesadores comparten físicamente la memoria, es decir, todos acceden al mismo espacio de direcciones. Un valor escrito en memoria por un procesador puede ser leído directamente por cualquier otro.
• Modelo de paso de mensajes: cada procesador dispone de su propia memoria independiente. Para realizar el intercambio de información cada procesador tiene que enviar la información al procesador que la necesite. El entorno de programación PVM utiliza este modelo.

Programación distribuida
Uno de los motivos principales para construir un sistema distribuido es compartir recursos. El sistema distribuido más conocido por todos es Internet. Entre las aplicaciones más recientes de la computación distribuida se encuentra el Cloud Computing. 
Se define un sistema distribuido como aquel en el que los componentes hardware o software, localizados en computadores en red, comunican y coordinan sus acciones mediante el paso de mensajes. Esta definición tiene como consecuencias: 
• Concurrencia: Lo normal en una red de ordenadores es la ejecución de programas concurrentes. 
• Inexistencia de reloj global. Cuando los programas necesitan cooperar coordinan sus acciones mediante el paso de mensajes. No hay temporalización. 
• Fallos independientes: Cada componente del sistema puede fallar independientemente sin afectar la continuidad de los demás.
La programación distribuida es un paradigma de la programación enfocado a desarrollar sistemas distribuidos, abiertos, escalables, transparentes y tolerantes a fallos.

PROGRAMACIÓN CONCURRENTE, PARALELA Y DISTRIBUIDA
- Programación Concurrente: Tenemos varios elementos de proceso (hilos, procesos) que trabajan de forma conjunta en la resolución de un problema. Se suele llevar a cabo en un único procesador o núcleo. 
- Programación Paralela: Es programación paralela cuando se utiliza para acelerar la resolución de los problemas, normalmente usando varios procesadores o núcleos. 
- Programación Distribuida: Es programación distribuida cuando los sistemas están distribuidos a través de una red. Se usa paso de mensajes.