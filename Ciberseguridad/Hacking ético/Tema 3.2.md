# Fingerprinting

# Enumeración de servicios

Tras la primera fase de reconocimiento, donde identificamos los nombres de dominio e IP de nuestros objetivos, pasaremos a una segunda fase, donde vamos a interactuar con el objetivo para obtener:

- Host activos: dentro de las redes del objetivo, no todas las máquinas estarán activas
- Puertos abiertos: que puertos y servicios tienen expuestos
- Según el servicio indagaremos un poco más, si es un servidor web, haremos fuzzing para ver carpetas y ficheros accesibles; en el caso de otros servicios, buscaremos usuarios, cuentas, grupos, ...
- Detalles del sistema operativo del host: indagaremos sobre la plataforma sobre la que corre el servicio, si es real o virtual, sistema operativo y versión, ...

Para esta tarea podemos emplear diversas herramientas, las principales son:

- nmap: la referencia para este comentido, potente y actualizada. Disponible en [https://nmap.org/](https://nmap.org/) 
- rustscan: reaizada en el lenguaje rust, promete mucha velocidad, aunque no siempre lo logra. Disponible en [https://github.com/bee-san/RustScan](https://github.com/bee-san/RustScan) 
- masscan: enfocada a escaneos masivos, permite barrer grandes segmentos de redes. Disponible en [https://github.com/robertdavidgraham/masscan](https://github.com/robertdavidgraham/masscan) 

Nmap es sin duda la más empleada, a pesar de ser la más antigua, pero está muy actualizada.

|                                                                                                                                         |                                                                                             |
| --------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| ![nmap](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/215572/mod_exescorm/content/21/nmap-300x136.jpg) | Nmap es sin duda la más empleada, a pesar de ser la más antigua, pero está muy actualizada. |
# Análisis de host y puertos

# Estados posibles de un puerto

En un host activo, los puertos pueden estar:

- abierto: disponible y con un servicio detrás
- cerrado: accesible pero sin una aplicación detrás
- filtrado: existe un cortafuegos que impide alcanzarlo, tras el cortafuegos puede estar abierto o cerrado.

En el caso de puertos UDP, pueden estar abiertos pero no responder a los datagramas enviados.

Descubrir puertos expuestos, su estado y el servicio que tienen detrás es el objetivo de la enumeración. Por otra parte, el sondeo de puertos puede servir para detectar host activos que no responden a otro tipo de peticiones, como puede ser un ping.

# Conexión completa

# Three way handshake

Este análisis se basa en intentar realizar conexiones tcp y posteriormente recoger el banner de conexión para ver el servicio que se encuentra al otro lado. Tanto si se detecta un puerto como abierto o como cerrado, se puede ver que el host está activo.

![handshake](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/215572/mod_exescorm/content/21/tcp_three_way_handshake.png)

Para determinar el estado del puerto, si se completa el handshake el puerto estará abierto, pero pueden darse estos otros casos:

![sondeo](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/215572/mod_exescorm/content/21/sondeo.png)# Half-connect

# TCP-SYN

En este análisis consiste en realizar un inicio de sesión pero no completarlo, en vez de responder con un ACK, en el tercer mensaje se responde con un RST, evitando completar la conexión. De esta forma no se registra en los logs del servicio y obtenemos mayor sigilo. Para este análisis debemos emplear la herramienta como root, ya que hay que hacer segmentos a medida.

![half](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/215572/mod_exescorm/content/21/sondeohalf.png)
# UDP

# Cuando no hay conexiones

El protocolo UDP no está orientado a conexión, por tanto las técnicas anteriores no nos van a servir. Debemos construir y enviar datagramas a los puertos UDP uy analizar la respuesta para poder intuir el estado del puerto. En el caso de nmap lo interpreta de la siguiente manera:

- Si la respuesta es un _ICMP Port Unreachable_, el host está activo y el puerto cerrado.
- Si la respuesta es un error, por ejemplo _TTL agotado_ o _Host/Network unreacheable_, el host no está activo.
- Si no devuelve nada, lo marca como abierto/filtrado. 

Si buscamos servicios UDP conocidos, enviaremos un datagrama compatible con el servicio esperado, por ejemplo una consulta DNS al puerto UDP 53.

# Otros análisis

# Otros posibles segmentos

Además de las conexiones, completas o solo a medias, existen otras alternativas para sondear puertos TCP.

- Análisis ACK: Se envía un segmento con el flag ACK activado, esto nos va a permitir evadir el cortafuegos y llamar menos la anteción.

![ack](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/215572/mod_exescorm/content/21/sondeo3.png)

- Análisis FIN: se envía con el flag FIN activado
- Escanner XMAS: se envía con los flags FIN,URG, y PUSH activos
- Escanner NULL: se envía un segmento con todos los flag a cero

Pueden dar buenos con sistemas Linux, ya que respetan de manera más estricta la RFC 793, Cisco y Windows no lo hacer.

La respuesta debe interpretarse como:

1. RST: puerto cerrado y host activo
2. ICMP Host unreacheable: puerto filtrado
3. sin respuesta: puerto abierto ó filtrado.
# Nmap

# Network Mapper

Es una herramienta open-source multiplataforma, bastante antigua pero con un mantenimiento constante que la convierte en referencia. Es una herramienta manual, a diferencia de otras denominadas de "botón gordo", que están más automatizadas. Permite entre otras cosas:

- mapeo de redes y descubrimiento de equipos
- escaneo de puertos
- detección del sistema operativo del host
- detección de servicio y versión detrás de un puerto
- enumeración de servicios: pruebas adicionales sobre los servicios, por ejemplo carpetas detrás de un http
- detección y evasión de firewalls
- creación de scripts para la herramienta, ofreciendo frameworks para le lenguaje LUA, que es el empleado

La estructura del comando es:

```
nmap [técnica de descrubrimiento] [técnica de análisis de puertos] [otros modificadores] IP o red a analizar
```

```clike
nmap [técnica de descrubrimiento] [técnica de análisis de puertos] [otros modificadores] IP o red a analizar
```

Por defecto analiza los 1000 puertos más habituales, podemos rastrear toda la red del aula con el siguiente comando:

```clike
nmap 10.227.87.0/24
```

Pero si nuestro objetivo es sólo ver los equipos activos este análisis puede resultar lento.

# Descubrimiento de equipos

# ¿Quien está en esta red?

Si consultamos la ayuda de nmap mediante nmap --help, nos muestra un resumen de las principales opciones, vamos a ver la primera parte, el descubrimiento de equipos

![nmap1](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/215572/mod_exescorm/content/21/nmap-discover.png)

Vamos a ver las opciones, debemos tener en cuenta que **se sondean puertos para detectar equipos activos**:

- -Pn : (don't Ping) se salta el descubrimiento de equipos por ping y va directamente al análisis de puertos.
- -PS : usa la técnica half-connect, enviando un SYN al puerto. Se pueden especificar puertos, -PS443
- -PA : emplea sondeo TCP-ACK, por defecto al puerto 80. Se pueden especificar puertos -PA80
- -PU : sondeo UDP, por defecto al puerto 40125
- -PR : ARP Discovery, similar a la herramienta _arp-scan_ o _netdiscover_. Es la técnica por defecto si el objetivo está en el mismo segmento de red que el atacante
- -PE : emplea un simple ping (ICMP echo), facilmente detectable en cortafuegos
- -PP : emple ICMP timestamp, más discreto que el ping
- -PO : emplea ICMP, IGMP e IP a la vez.

Por defecto usará -PR si el objetivo está en el mismo segmento, si está en diferente segmento emplea -PE -PP -PA80 -PS443.

Si no queremos nada más que descubrir host activos, lo combinaremos con la opción -sn, por ejemplo.

```clike
nmap -PR -sn 192.168.1.0/24
```

# Descubrimiento de puertos

La herramienta nmap escanea por defecto 1000 puertos, los más empleados habitualmente, se pueden consultar en  _cd /usr/share/nmap/nmap-services._ Pero podemos modificar este comportamiento:

- -F :(fast) sondea los 100 puertos más populares
- --top-ports: sondela los n puertos más populares
- --port-ratio : sondea por percentil de la frecuencia con que suele estar abierto, se emplea un valor entre 0 y 1.

Se pueden especificar puertos concretos o rangos de puertos:

- -p n1,n2,n3, .. : se sondean los puertos de la lista, separados por comas
- -p n-m : se sondea el rango de puertos
- -p- : se sondean todos los puertos, podemos acelerar el proceso combinando con --min-rate=5000

```clike
sudo nmap -p- scanme.nmap.org --min-rate=5000
```

Una vez especificados los puertos, podemos emplear diversos análisis sobre ellos:

- -sT : TCP connect, establece conexión y recoge el banner del servicio. No requiere privilegios de root
- -sS : TCP half-connect, sólo hace conexiones parciales, es más rápido y sigiloso.
- -sU : UDP scan, rastrea puertos UDP. Envía datagramas vacíos, pero en algunos casos envía solicitudes a servicios que reciben respuesta, y por ese motivo es seguro que están abiertos.
- -sF , -sX , -sN : sondeos FIN, Xmas y Null

Para complementar el análisis de puertos tenemos otras opciones:

- -O : envía diversas pruebas para detectar el sistema operativo, cada uno tiene sus propias "firmas" denominadas OS fingerprints, nmap dispone de una base de datos de las mismas.
- -sV : trata de identificar el software que da soporte al servicio, indicando además la versión. Se puede combinar con --version-intensity  , con el valor entre 0 y 9, siendo el 9 donde más pruebas se aplican. Con esta información se puede buscar un exploit mediante _searchsploit_.
- -A : aggressive scan, genera mucho ruido pero realiza varias opciones a la vez, -O -sV y -sC con los scripts por defecto.

La salida de nmap la podemos volcar a un archivo con tres formatos:

- -oN : salida normal de nmap
- -oX : formato XML
- -oG : formato grepable, que se puede filtrar con grep y expresiones regulares

# Scripts

Nmap tiene el servicIo NSE (Nmap Scripting Engine) para manejo de los scripts. Ofrece un framework para la elaboración de scripts para nmap. El lenguaje de programación empleado es LUA, una de las demandas más frecuentes en esta herramienta es ofrecer soporte para Python, pero no está disponible.

Los scripts preinstalados están en /usr/share/nmap/scripts. Tenemos documentación sobre los mismos en [https://nmap.org/nsedoc/scripts/](https://nmap.org/nsedoc/scripts/) . Además de los instalados, se pueden añadir otros propios o desarrollados por terceros.

Se organizan por categorías, hay 14, y se pueden consultar mediante:

```clike
nmap --script-help [script|categoria]
```

Por ejemplo: 

```clike
nmap --script-help safe
```

También podemos consultar por términos que aparecen y combinarlos mediante _and_ y _or_.

```clike
nmap --script-help "mysql-* and safe"
```

Para emplear un script concreto se indica mediante _--script_.

```clike
 nmap -p 21 --script ftp-anon ftp.rediris.es
```

Se pueden invocar varios scripts separados por comas e incluso emplear comodines, también podemos pasar todos los scripts de una categoría, por ejemplo _nmap --script safe 10.0.1.26 -v_

Para emplear parámetros se pone _--script-args_ y los pares _argumento=valor_ correspondientes separados por comas si son varios.

En este [artículo](https://www.incibe.es/incibe-cert/blog/explorando-el-modulo-de-scripts-de-nmap) de Incibe nos profundiza un poco en el tema.

# Enumeración de servicios

Una vez descubierto un servicio, podemos profundizar sobre él y obtener más información. Este proceso es la enumeración.

Vamos a ver tres casos muy habituales.

- **Enumeración FTP**

Para este servicio podemos:

1. Obtener la versión del servicio instalado con  -sV
2. Obtener el banner, para ello podemos empear varias opciones, como puede ser emplear _nmap -p 21 --script banner 
3. leer el banner mediante telnet: _telnet

Ahora podemos emplear diversos script para encontrar vulnerabilidades:

1. ftp-anon: compueba si hay usuario anonymous activado
2. ftp-bounce: permite saber si el servidor es vulnerable al escaneo de puertos y ataque ftp-bounce, que permite pivotar sobre él para acceder a otras máquinas. Es una vulnerabilidad antigua.
3. ftp-syst: envía comandos SYST y STAT, empleando el usuario anónimo u otro identificado e identifica el sistema operativo y el estado del servidor.

Para descargar contenido de un servidor ftp en línea de comandos podemos emplear:

```clike
curl ftp://usuario:password@servidorftp
wget -m ftp://usuario:password@servidorftp
```

Podemos además tratar de probar credenciales con el script _ftp-brute_ o con las herramientas _hydra_ y _medusa_.

- **Enumeración HTTP**:

Cuando detectamos un servicio web debemos hacer lo siguiente:

1. inspeccionar el sitio y código fuente: html, javascript y css
2. detectar tecnologías usadas: servidor (apache,nginx, ..) y lenguaje detrás (PHP, JSP, ASPX, ...)
3. Fuzzing web: descubrir archivos y carpetas que se ofrecen, subcarpetas ocultas, ...
4. Análisis de vulnerabilidades: hay herramientas automáticas que nos ayudan

Cuando revisamos el código en un sitio web debemos, revisar el javascript y ver qué hace, buscar comentarios en el html, comprobr archivos adicionales del javascript, comprobar las cookies, probar credenciales predeterminadas, identificar si se emplea un CMS y sus plugins, ... Con todo esto podemos buscar vulnerabilidades.

Para detectar tecnologías empleadas podemos usar:

1. wappalyzer: plugin del navegador que permite revisar tecnologías empleadas y CMS.
2. whatweb: herramienta en línea de comandos disponible en Kali, similar a la anterior
3. WPScan: analiza sitios creados con wordpress
4. Joomscan: herramienta para sitios creados en Joomla, realizada en Perl y patrocinada por OWASP
5. Drupwn: realizada en Python y aplicable a drupal 7 y 8.
6. Scripts de nmap: http-wordpress-* , existen diversos para wordpres, por ejemplo http-wordpress-brute permite bucar credenciales mediante diccionarios.

Los CMS se emplean en la mayoría de los sitios web, podemos ver una estadística en: [https://w3techs.com/technologies/history_overview/content_management/all](https://w3techs.com/technologies/history_overview/content_management/all) 

Si no tenemos claro el CMS empleado, podemos emplear _CMSeek_, realizada en python, identifica más de 180 CMS. Disponible en Kali.

- **Fuzzing web**

No siempre se sabe qué carpetas y archivos ofrece un sitio wep, puede haber contenidos no visibles a través de su index. El fuzzing consiste en hacer peticiones al servidor en busca de esos contenidos ocultos, no indexados en ninguna parte.

Las herramientas son muy variadas:

1. **wfuzz**: escrita en python y muy potente, permite varios hilos de ejecución. Permite además hacer fuzzing en sitios donde haya que estar logeado, manejando las cookies de sesión.
2. script http-enum de nmap: es básico pero puede ser un primer paso, tiene el argumento http-enum.basepath para indicar carpeta de inicio del fuzzing.
3. dirbuster: disponible en kali y con interfaz gráfica
4. gobuster: escrita en Go y bastante rápida
5. dirb: instalada en kali
6. dirsearch: disponible en kali
7. ffuf: en Go y bastante eficiente
8. feroxbuster: escrita en rust y permite búsqueda recursiva en carpetas.

Tan importante como la herramienta o más, son los diccionarios, disponemos de varios ya instalados en kali, están en la carpeta _/usr/share/wordlists_.

- **Enumeración SMB**

El protocolo Server Message Block sirve para compartir recursos, como archivos e impresoras, y es nativo en Windows. En Linux se puede emplear instalando samba. 

Hay diversas herramientas y algunos scripts de nmap para hacer la enumeración en este servicio en caso de ser detectado.

1. nbtscan: escanea servicios de NetBIOS en general, como puede ser SMB
2. enum4Linux: combina la salida de 4 herramientas, como son smbclient, rpclient, net y nmblookup
3. scripts de nmap
4. smbmap: enumera shares de smb
5. smbclient: cliente de SMB
6. rpcclient: similar a la anterior

# Análisis automatizado

Las herramientas disponibles para automatizar el proceso serían:

- legion
- Nessus
- OpenVAS
- Nexpose
- Nikto
- Nuclei

# Nikto

![nikto](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/215572/mod_exescorm/content/21/Nikto.jpg)

Herramienta para open-source para escanear vulnerabilidades en sitios web. Disponible en Kali, se puede ejecutar desde docker y en windows.

Genera informes en json con los resultados obtenidos.

El proyecto está en [https://github.com/sullo/nikto](https://github.com/sullo/nikto)

# Nuclei

![nuclei](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/215572/mod_exescorm/content/21/nuclei-cover-image.png)

Herramienta open-source desarrollada en Go para detección de vulnerabilidades, viene integrada en Kali. Se basa en plantillas creadas en YAML y se pueden crear plantillas propias. 

Dispone de versión Pro y enterprise con un sistema en la nube al que se le pueden añadir y ampliar plantillas propias personalizadas para la empresa.

El proyecto está en [https://github.com/projectdiscovery/nuclei](https://github.com/projectdiscovery/nuclei)

# Nessus

![nessus](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/215572/mod_exescorm/content/21/nessus.png)

Es un producto de la empresa Tenable, ofrece un reconocimiento automático de sistemas y dispone de una amplia base de datos de vulnerabilidades.

Es un producto de pago pero con un correo se puede obtener una clave de activación para emplearla con un número limitado de IP. 

Genera un informe de resultados.

# OpenVAS

![openvas](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/215572/mod_exescorm/content/21/openvaslogo.jpg)

Scanner de vulnerabilidades que dispone de una versión community con módulos open-source. Se puede emplear en Kali instalando una serie de paquetes de sus repositorios.

Se maneja con una interfaz web similar a Nessus.

