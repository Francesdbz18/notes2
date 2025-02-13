 1. **Se han identificado diferentes protocolos estándar de comunicación para la implementación de servicios en red.** 
El modelo TCP/IP está compuesto por 4 capas. La capa de aplicación define las aplicaciones de red y los servicios estándar. Estos servicios utilizan la capa de transporte para enviar y recibir datos. Existen varios protocolos de capa de aplicación.
	- TELNET (Telecommunication Network) es un protocolo de emulación de terminal. Permite a un usuario acceder a una máquina remota y manejarla como si estuviese en ella. Su talón de Aquiles es la seguridad, ya que los nombres de usuario y las contraseñas viajan por la red como texto plano. El puerto estándar Telnet es el 23. Hoy en día está obsoleto, en su lugar se utilizan “Conexión a escritorio remoto”, VNC, SSH o Wine.
	- SMTP (Simple Mail Transfer Protocol). Es un protocolo simple de transferencia de correo electrónico. Este estándar especifica el formato exacto de los mensajes que un cliente en una máquina debe enviar al servidor de correo. Los puertos SMTP más habituales son: 25, 465, 587 y 2525.
	- FTP (File Transfer Protocol). Es un protocolo de transferencia de archivos. Se trata de un servicio confiable orientado a conexión que se utiliza para transferir ficheros. Los puertos estándar usados por FTP son el 20 y el 21.
	- TFTP (Trivial File Transfer Protocol) Protocolo trivial de transferencia de ficheros. Es una versión básica de FTP. Utiliza el puerto 69 UDP.
	- HTTP (HyperText Transfer Protocol) Protocolo de transferencia de hipertexto. Es el protocolo que usan los navegadores web para realizar las comunicaciones con los servidores web. El protocolo especifica los mensajes involucrados en un intercambio petición-respuesta, los métodos, argumentos y resultados y las reglas para representar todo ello en los mensajes. Los puertos estándar HTTP son el 80 y el 8080.
	- NFS (Network File System) Sistema de archivos en red. Desarrollado por Sun Microsystems. Utiliza el puerto 2049.
	- SMB (Server Message Block) Sistema de servicios en red, no solo de archivos. Desarrollado originalmente por IBM, la implementación más extendida es la de Microsoft. La versión para Linux/Unix se llama SAMBA. Utiliza el puerto TCP 445.
	- SNMP (Simple Network Management Protocol) Protocolo simple de administración de red. Facilita el intercambio de información de administración entre dispositivos de red. El puerto SNMP es el 161 UDP.
	- DNS (Domain Name System). Sistema de nombres de dominio. Es un sistema que utiliza servidores distribuidos por toda la red para resolver nombres de host en direcciones IP. Utiliza los puertos 53 TCP y UDP.

2. **Se han reconocido las ventajas de la utilización de protocolos estándar para la comunicación entre aplicaciones y procesos.** 
#### Interoperabilidad 
- Comunicación entre diferentes sistemas.
- Integración de sistemas heredados.
- Ampliación de la vida útil de las aplicaciones.
#### Eficiencia
- Reducción del tiempo de desarrollo.
- Optimización de recursos.
- Facilidad de mantenimiento.
#### Escalabilidad
- Adaptación a cargas de trabajo variables.
- Integración de nuevos sistemas.
#### Otros beneficios
- Mayor seguridad.
- Reducción de costos.
- Fomento de la innovación.

3. **Se han analizado librerías que permitan implementar servicios en red utilizando protocolos estándar de comunicación.**
#### Librerías de bajo nivel
- java.net
- Java NIO
#### Librerías de alto nivel
- Netty
- Spring WebFlux
#### Librerías específicas para protocolos
- Java Mail API.
- JDBC.
- JMS.
- Apache Commons Net

|                           | Apache Commons Net    | Netty           | Spring WebFlux            | java.net / NIO |
| ------------------------- | --------------------- | --------------- | ------------------------- | -------------- |
| **Nivel de abstracción**  | Alto                  | Medio-bajo      | Alto                      | Bajo           |
| **Rendimiento**           | Bueno                 | Muy bueno       | Bueno                     | Muy bueno      |
| **Facilidad de uso**      | Fácil                 | Moderada        | Fácil (si conoces Spring) | Difícil        |
| **Flexibilidad**          | Moderada              | Alta            | Alta                      | Alta           |
| **Protocolos soportados** | FTP, SMTP, POP3, etc. | Personalizables | HTTP, WebSocket           | Todos          |
