**a) Se han identificado situaciones en las que resulte útil la utilización de varios hilos en un programa.**
Un hilo (thread), hebra, proceso ligero o subproceso es una secuencia de código en ejecución dentro de un proceso que puede ser ejecutada por un sistema operativo. Los hilos no tienen existencia independiente fuera de los procesos.
El uso de los hilos es muy diverso. Se pueden usar cuando un programa tiene que realizar tareas simultáneamente: 
- Un programa controla sensores en una fábrica.
- Una cola de impresión debe seguir recogiendo documentos mientras se imprime en otro hilo.
- Un procesador de textos puede tener un hilo comprobando la gramática del texto y otro hilo guardando en disco cada cierto tiempo.
- Un servidor web atiende a cada cliente en un hilo diferente.
- 
**i) Se ha analizado el contexto de ejecución de los hilos**

**j) Se han analizado librerías específicas del lenguaje de programación que permiten la programación multihilo.**
Hay dos formas en Java de crear hilos: extendiendo la clase Thread o implementando la interfaz Runnable. 
La clase THREAD. Al extender Thread debemos sobreescribir el método run(). La clase Thread define también los métodos start() y stop() (en desuso) para iniciar y parar la ejecución del hilo. La forma general de declarar un hilo es: Para crear un hilo con las características de NombreHilo escribiríamos: NombreHilo h = new NombreHilo(); Y para iniciarlo: h.start();
Todo hilo en Java debe formar parte de un grupo. Por defecto (si no se especifica en el constructor) los hilos serán miembros del grupo main, que se crea cuando se arranca la aplicación. La clase ThreadGroup se puede usar para manejar grupos de hilos en las aplicaciones Java. La clase Thread tiene constructores en los que se puede especificar el grupo del hilo en el momento de instanciarlo. En el siguiente ejemplo se crea un grupo de hilos de nombre Grupo de hilos. A continuación se crean tres hilos usando el constructor de la clase Thread: Thread(ThreadGroup grupo, Runnable destino, String nombre)
Hay dos formas en Java de crear hilos: extendiendo la clase Thread o implementando la interfaz Runnable. La interfaz RUNNABLE. Si queremos añadir la funcionalidad de hilo a una clase que deriva de otra clase distinta de Thread podemos usar la interfaz Runnable. Por ejemplo, para añadir la funcionalidad de hilo a una aplicación con un Jpanel de Swing definimos la clase como: public class Reloj extends Jpanel implements Runnable {} La interfaz Runnable tiene un único método, el método run(). Éste es ejecutado por el objeto hilo asociado. Para declarar un hilo implementando la interfaz Runnable: 2.3.- Clases para la creación de hilos. Para crear un objeto hilo de tipo NombreHilo escribiríamos: NombreHilo h = new NombreHilo(); Y lo iniciaríamos con el método start(): new Thread(h).start(); O bien lanzaríamos el hilo en dos pasos: Thread h1 = new Thread(h); h1.start(); O en un paso todo: new Thread(new NombreHilo()).start();

**k) Se han reconocido los problemas derivados de la compartición de información entre los hilos de un mismo proceso.**
