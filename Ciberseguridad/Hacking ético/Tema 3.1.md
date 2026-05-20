# Footprinting
# Intelligence gathering

# La obtencíon y relocección de información

Es una de las primeras fases en todos pentest, hay que recopilar toda la información disponible para diseñar una estrategia de ataque efectiva. Desde el punto de vista defensivo, debemos tener en cuenta cuanta información nuestra circula por la red, que sea sólo la necesaria y ver si informa de posibles debilidades.

Hay dos tipos de información:

- Información comercial y legal: Empleados, cargos, correos, relaciones con otras empresas, ...
- Información tecnológica: Servicios, tecnologías empleadas, gestores de contenidos, ip, infraestructuras de red, ...

Se puede obtener a veces mucha información que , en bruto, no es útil. Se debe procesar y organizar, generando lo que se llama Inteligencia, que nos va a permitir tomar mejores decisiones.

![](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/piramide.jpg)

Este modelo, propuesto en 1998, ilustra esta idea. Este proceso se denomina **intelligence gathering**.

Según las fuentes tendremos:

- OSINT: (Open Source) de fuentes abiertas.
- HUMINT: (Human) de fuentes humanas
- SIGINT: (Signal) de señales
- GEOINT: (Geospacial) Geoespacial
- IMINT: (Image) de imágenes
- MASINT: (Measure and Signature) basado en medidas físiscas.

En este [enlace](https://www.dni.gov/index.php/what-we-do/what-is-intelligence) están las definiciones más ampliadas, a los hackers nos interesan los tres primeros tipos.

# OSINT

# Inteligencia en fuentes abiertas

Se basa en buscar información en fuentes públicas, pero no necesariamente gratuitas o digitales. Por ejemplo, podemos recabar información de un domicilio, pidiendo una nota simple en el registro de la propiedad. Esto tiene un coste pero es fuente abierta, nos dará datos catastrales, si está hipotecado, ...

Existen multitud de fuentes abiertas además de lo que podemos obtener en buscadores y redes sociales:

- Medios de comunicación: prensa, radio, tv, ...
- Fuentes gubernamentales: boletines oficiales del estado, autonómicos y provinciales, registros gubernamentales, DGT, ...
- Conferencias, simposios, artículos de investigacióon, bibliotecas on line, ...

En definitiva, todo aquello que podemos acceder legalmente, sin romper ninguna medida de seguridad. Si accedemos al correo privado de alguien mediante por ejemplo, ingeniería social, no sería OSINT.

OSINT nació en 1941 durante la Segunda Guerra Mundial, se escuchaban emisoras de radio extranjeras, se traducían y se elaboraban informes con información estratégica, obtenida de estas fuentes públicas.

En julio de 2014, el avión MH17 fue derribado en el este de Ucrania. Un grupo de personas voluntarias, a partir de vídeos de youtube, mapas de Google Earth y mensajes en redes sociales consiguieron averiguar la trayectoria del misil que impactó en el avion, e incluso los nombres de los responsables. Todo eso empleando sus ordenadores y sin ningún tipo de actividad de espionaje. Esto es un hito en la historia de la investigación sobre fuentes abiertas. Sacar conclusiones relevantes analizando información pública.

Lo más importante es entender que OSINT NO es hackear nada, es acceder a información pública son vulnerar ninguna medida de seguridad.

# HUMINT

# Fuentes humanas

Recogido directamente de personas, esto sería espionaje.

Se capta a alguien que nos pueda servir de fuente, y luego se analiza la información adquirida. 

Otra técnica más discreta barata es, por ejemplo, acudir a la cafetería donde desayunan los trabajadores de la empresa de la que quiero información y escuchar a ver si se obtiene algo útil. A veces se habla de los proyectos en marcha, incidencias, ...

# SIGINT

# Señales

Se obtiene información a partir de procesar datos de cualquier tipo de señales y transmisiones.

Podemos profundizar en lo que es SIGINT en este [video](https://www.youtube.com/watch?v=jYcBDWAWsWo). Su título es Matrioshka SIGINT: Análisis de señales ocultas , realizada por David Marugán. Esta conferencia se presenta en IntelCon 2020.

Un ejemplo de cómo podemos emplear señales para OSINT es [wigle](https://wigle.net/index). Esta herramienta WiGLE.net es una plataforma web y base de datos colaborativa (desde 2001) que mapea la ubicación de redes WiFi, torres de telefonía celular y dispositivos Bluetooth en todo el mundo. Funciona mediante wardriving, donde voluntarios recopilan datos (SSID, BSSID, cifrado) vía GPS, siendo útil para ciberseguridad, análisis de cobertura y búsquedas OSINT.  YouTube +4  
Características clave de WiGLE:

- Mapa Global de Redes: Visualiza concentraciones de redes WiFi en un mapa mundial, mostrando su ubicación geográfica exacta.  
    Datos Recopilados: Almacena información detallada como el nombre de la red (SSID), la dirección MAC (BSSID), el tipo de cifrado (WEP, WPA, etc.) y coordenadas GPS.
- Colaboración (Crowdsourcing): Los usuarios (mediante una app Android) suben datos de redes que detectan mientras se mueven.
- Uso en Ciberseguridad/OSINT:  Es una herramienta muy utilizada para inteligencia de fuentes abiertas (OSINT) y seguridad informática, permitiendo investigar la geolocalización de redes.
- Aplicación Android: Permite a los usuarios escanear redes y contribuir a la base de datos.

En este [vídeo](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/Es%20una%20herramienta%20muy%20utilizada%20para%20inteligencia%20de%20fuentes%20abiertas%20\(OSINT\)%20y%20seguridad%20informática,%20permitiendo%20investigar%20la%20geolocalización%20de%20redes.%20Aplicación%20Android:%20Permite%20a%20los%20usuarios%20escanear%20redes%20y%20contribuir%20a%20la%20base%20de%20datos.) se explica en qué consiste.

# DNS

# ¿Qué es el servicio DNS?

DNS (Domain Name Service) es un servicio distribuido que nos permite traducir nombres de dominio a direcciones IP. Funciona con un sistema jerárquico y en la raiz se sitúan los root-servers.

![](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/dns-root-server.png)

Esta imagen refleja cómo funciona este servicio ([enlace a la fuente](https://www.cloudflare.com/img/learning/dns/glossary/dns-root-server/dns-root-server.png))

Aunque sólo tienen 13 IP, hay muchos más servidores root en el mundo, pero operan con un erutamiento anycast que permite distribuir las peticiones y balancear la carga.

En este [enlace](https://root-servers.org/) podemos ver un mapa y toda la información relativa a los root servers.

# Información Whois

# Registro de diminios

Para registrar un dominio el registrante (registrant) debe proporcionar una información básica (según la RFC 3912), actualmente hay más de 360 millones de dominios. Esta información sería:

- correo electrónico
- dirección
- datos de contacto técnico
- datos de contacto administrativo
- servidores dns

El protocolo whois permite obtener esta información pero no es un servicio centralizado, sino distribuído, y además gran parte de la información personal del registrante se oculta por privacidad. Los actores que intervienen son:

- Agentes Registradores (Registrars): autorizados por los operadores de registro, recogen la solicitudes de los solicitantes de registro.
- Operadores de registro (Registry operators): Su misión es mantener la base de datos maestra de todos los nombres de dominio registrados en cada dominio de alto nivel (TLD) y generar el "archivo de zona".
- ICANN: Organización sin ánimo de lucro que coordina el DNS

![proceso de registro](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/registrar-flow.png)

(imagen procedente de ICAAN)

Podemos usar whois en línea de comandos:

![](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/whois.PNG)

Pero podemos usar servicios online para el mismo propósito:

- whois.net
- who.is
- lookup.icann.org
- goddady

Pero esto no funciona con todos los TLD's, para el dominio .es obtendremos:

![](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/whois_es.PNG)

En este caso podemos consultar la información [online](https://www.dominios.es/es) o registrarnos para poder usar whois en línea de comandos. En este [enlace](https://www.dominios.es/es/sobre-dominios/valores-anadidos/whois-43) explica cómo hacerlo.

# Comandos y herramientas de línea de comandos

En la línea de comandos contamos con varias herramientas que me permiten hacer consultas DNS:

- host
- dig
- nslookup

Estas tres herramientas permiten hacer consultas de diversos tipos de registros (MX, NS, A, AAAA, SOA, TXT,...) hacia cualquier servidor elegido e incluso consultas de resolución inversa.

Para hacer enumeración DNS, es decir, buscar posibles nombres dentro de un dominio a partir de wordlists o intentar transferencias de zona tendremos:

- [dnsrecon](https://github.com/darkoperator/dnsrecon): realizada en python y bastante actualizada
- [dnsenum](https://github.com/fwaeytens/dnsenum): Hecha en perl pero sin mantenimiento desde hace tiempo.
- [dnsmap](https://github.com/resurrecting-open-source-projects/dnsmap): busca subdominios por fuerza bruta
- [dnswalk](https://github.com/davebarr/dnswalk): testeador de configuración dns en busca de inconsistencias.
- [fierce](https://github.com/mschwager/fierce): cuenta con muchas opciones y permite uso de diccionarios.
- [knockpy](https://github.com/guelfoweb/knock): enumera subdominios por diccionario, el autor recomienda configurar la API Key de Virustotal para obtener mejores resultados.

Estas herramientas estarán disponibles en Kali y Parrot, simplemente habrá que instalarlas con apt install.

# Fuerza bruta

Las técnicas de fuerza bruta en sentido estricto sería probar todas las posibles combinaciones, por ejemplo generar todos los posibles nombres dentro de un dominio. Esto sólo es posible para nombres de unas pocas letras (menos de 6)

Generalmente usaremos diccionarios, y las diversas herramientas los incluyen.

Para no hacer demasiado ruido, esto se suele hacer empleando diversos servidore dns-caché, si lo hacemos directamente contra el servidor autoritativo del dominio podemos ser detectados y bloqueados.

Si tenemos un servidor dns local, debemos detectar esta avalancha de consultas para detectar un posible ataque.

# Trasferencias de zona

Es el proceso por el cual los servidores secundarios copian el contenido del servidor DNS principal, puede ser de dos tipos:

- Transferencia completa (AXFR): copia completamente todo el archivo de la zona
- Transferencia parcial (IXFR): solo copia los cambios desde la última actualización.

Para intentar una trasferencia de zona usaremos:

```
dig axfr @<servidor>  <zona>
```

Para probarlo buscaremos el servidor NS de zonatransfer.me, servidor que nos permite hacer esta operación con fines educativos:

```
Profesor@LAPTOP-ICS5SKT2:~$ dig @8.8.8.8 zonetransfer.me ns +short
nsztm2.digi.ninja.
nsztm1.digi.ninja.
Profesor@LAPTOP-ICS5SKT2:~$ dig axfr @nsztm2.digi.ninja. zonetransfer.me

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> axfr @nsztm2.digi.ninja. zonetransfer.me
; (1 server found)
;; global options: +cmd
zonetransfer.me.        7200    IN      SOA     nsztm1.digi.ninja. robin.digi.ninja. 2019100801 172800 900 1209600 3600
zonetransfer.me.        301     IN      TXT     "google-site-verification=tyP28J7JAUHA9fw2sHXMgcCC0I6XBmmoVi04VlMewxA"
zonetransfer.me.        7200    IN      MX      0 ASPMX.L.GOOGLE.COM.
zonetransfer.me.        7200    IN      MX      10 ALT1.ASPMX.L.GOOGLE.COM.
zonetransfer.me.        7200    IN      MX      10 ALT2.ASPMX.L.GOOGLE.COM.
zonetransfer.me.        7200    IN      MX      20 ASPMX2.GOOGLEMAIL.COM.
zonetransfer.me.        7200    IN      MX      20 ASPMX3.GOOGLEMAIL.COM.
zonetransfer.me.        7200    IN      MX      20 ASPMX4.GOOGLEMAIL.COM.
zonetransfer.me.        7200    IN      MX      20 ASPMX5.GOOGLEMAIL.COM.
zonetransfer.me.        7200    IN      A       5.196.105.14
zonetransfer.me.        7200    IN      NS      nsztm1.digi.ninja.
zonetransfer.me.        7200    IN      NS      nsztm2.digi.ninja.
zonetransfer.me.        300     IN      HINFO   "Casio fx-700G" "Windows XP"
_acme-challenge.zonetransfer.me. 301 IN TXT     "2acOp15rSxBpyF6L7TqnAoW8aI0vqMU5kpXQW7q4egc"
_acme-challenge.zonetransfer.me. 301 IN TXT     "6Oa05hbUJ9xSsvYy7pApQvwCUSSGgxvrbdizjePEsZI"
```

Podemos ahora descubrir subdominios y hacer transferencias de zona a su vez.

# Certificados

[Ocultar](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/certificados.html# "Ocultar")

# Obtener dominios ocultos en los certificados

[Ocultar](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/certificados.html# "Ocultar")

Los certificados de servicios seguros, como https, contienen información que se puede aprovechar. En muchos casos sirven para sitios de diversos dominios y subdominios de la organización a investigar. Esta información es accesible de manera pública y hay sitios que recopilan estos certificados, incluso los ya caducados.

Herramientas que nos pueden servir para esta tarea son:

- [ct-exposer](https://github.com/chris408/ct-exposer): desarrollada en python

```processing
$ git clone https://github.com/chris408/ct-exposer.git
$ cd ct-exposer
$ pip3 install -r requirements.txt
$ chmod +x ct-exposer.py
$ ./ct-exposer.py -d iberdrola.com  
```

- certgraph: gráfica y disponible en Kali
- [https://crt.sh/:](https://crt.sh/:) sitio donde poder consultar on-line información sobre certificados
# Servidores DNS caché locales y Snooping

Si disponemos de un servidor DNS caché local, podemos comparar el TTL de una consulta DNS y compararla con el TTL de su servidor autoritativo, viendo la diferencia podemos saber si esa consulta se ha hecho y hace cuanto tiempo.

Con esta técnica llamada DNS caché Snooping se puede averiguar los sitios por los que los usuarios de una organización navegan.

En este [artículo](https://learn.microsoft.com/es-es/troubleshoot/windows-server/networking/dns-server-cache-snooping-attacks) de Microsoft podemos aprender más al respecto.

# Resolución inversa

La resolución inversa consiste en ver el nombre asociado a una determinada ip, para ello podemos usar los comando host y dig entre otros. Veamos un ejemplo:

```
profesor@LAPTOP-ICS5SKT2:~$ host -t PTR 108.157.109.2
2.109.157.108.in-addr.arpa domain name pointer server-108-157-109-2.mad56.r.cloudfront.net.
profesor@LAPTOP-ICS5SKT2:~$ dig -x 108.157.109.2

; <<>> DiG 9.18.28-0ubuntu0.22.04.1-Ubuntu <<>> -x 108.157.109.2
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 17920
;; flags: qr rd ad; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
;; WARNING: recursion requested but not available

;; QUESTION SECTION:
;2.109.157.108.in-addr.arpa.    IN      PTR

;; ANSWER SECTION:
2.109.157.108.in-addr.arpa. 0   IN      PTR     server-108-157-109-2.mad56.r.cloudfront.net.

;; Query time: 0 msec
;; SERVER: 192.168.128.1#53(192.168.128.1) (UDP)
;; WHEN: Thu Nov 28 22:15:13 CET 2024
;; MSG SIZE  rcvd: 127
```

# Herramientas

# Automatizando la tarea

## Sublist3r

](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/herramientas.html#exe-accordion-0-0)[

## Spiderfoot

](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/herramientas.html#exe-accordion-0-1)

  
Además de estas herramientas, se dispone de herramientas on-line:

- [https://www.domaintools.com/](https://www.domaintools.com/): de pago, ofrece servicios avanzados
- [https://robtex.com/:](https://robtex.com/:) recopila información de ip, dns y AS (Autonomous Systems) de fuentes abiertas
- [https://www.netcraft.com/:en](https://www.netcraft.com/:en) la sección de recursos tiene herramientas para búsquedas dns.
- [https://www.virustotal.com/gui/intelligence-overview](https://www.virustotal.com/gui/intelligence-overview): aunque su labor principal es la detección de malware, en la sección intelligence emplea google, facebook y una API para obtener información de todo tipo.
- [https://dnsdumpster.com/](https://dnsdumpster.com/) : permite obtener información relativa a un dominio y muestra en un mapa la relación entre los diversos equipos descubiertos.
# Anonimato

# ¿Es posible conseguir la privacidad absoluta?

Para preservar anonimato podemos usar la navegación de incógnito, pero esto sólo nos protege de otros usuarios del mismo equipo y poco más.

La navegación a través de Internet y su uso deja rastro. Con el objetivo de conseguir la privacidad absoluta surgen las redes anónimas:

- TOR (The Onion Router): la más conocida que además proporciona el navegador tor
- I2P (Invisible Internet Project)
- FreeNET

Aunque vamos a ver sólamente TOR en este [enlace](https://www.xataka.com/basics/como-entrar-deep-web-guia-2020-para-entrar-tor-zeronet-freenet-e-i2p) explica las tres comentadas y otra llamada ZeroNet.

# Darknet

# Redes ocultas

Dentro de internet tendremos:

- Surface web: indexable por buscadores y accesible públicamente
- Deep web: Es accesible pero no está indexada por los buscadores, pueden ser protegidos por login, captchas, contenidos dinámicos, ... por ejemplo nuestro correo, google drive, dropbox
- Darkweb: no indexada por buscadores y requiere clientes específicos. Maneja incluso IP ocultas. Dentro están las Darknets.

![](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/deep-web.jpg)

Esta imagen representa estos conceptos ([fuente](https://www.independent.co.ug/technology-how-dark-is-dark-web/))

# VPN

Una VPN (Virtual Private Network) permite ocultar la IP de origen, ofreciendo anonimato. Los servidores de VPN pertenecen a entidades privadas, por tanto no se puede confiar en ellos ciegamente. La más conocida es [ProtonVPN](https://protonvpn.com/es-es), de la empresa suiza Proton, que ofrece un servicio gratuíto de prueba.

Supuestamente no registran ip temporal del usuario pero no es del todo cierto, en este [enlace](https://techcrunch.com/2021/09/06/protonmail-logged-ip-address-of-french-activist-after-order-by-swiss-authorities/) se ve un caso donde a requierimiento judicial si proporcionaron este dato.

Tanto las redes anónimas como las VPN hacen la conexión más lenta, pero hay opciones de pago que mejoran el rendimiento.

Un acceso desde una red anónima puede ser detectado y bloqueado, en el caso de VPN es menos frecuente.

Alternativas a proton pueden ser:

- Tunnelbear:  [https://www.tunnelbear.com/](https://www.tunnelbear.com/)
- nord: https://nordvpn.com/es/

# TOR

[Ocultar](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/tor.html# "Ocultar")

[Ocultar](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/tor.html# "Ocultar")

En los años 90 surge el proyecto Onion Routing en le laboriatorio de Investigación Naval de los EEUU, en este proyecto es establecen varias capas de cifrado.

En 2004 se publicó el código y surge el [Tor Project](https://www.torproject.org/), una organización sin ánimo de lucro que dispone de miles de nodos (relays) operados por voluntarios.

La red Tor está descentralizada y para acceder a internet se establece un circuito a través de tres nodos aleatorios, uno de entrada (A), uno intermedio (B) y otro de salida (C), con un cifrado por capas entre los tres:

![](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/tor.png)

Se cifra por capas en orden inverso.

En este [enlace](https://support.torproject.org/https/) vemos cómo conseguir anominato mediante la combinación de la red TOR y https.

Para poder usar la red TOR con otras herramientas diferentes que el navegador tor necesitaremos usar proxychains. En este [enlace](https://www.redeszone.net/tutoriales/seguridad/proxychains-tor-linux-ocultar-identidad-internet/) tenemos cómo hacerlo en Kali.

Se pueden detectar los nodos de la red TOR, aquí tenemos una [lista](https://www.dan.me.uk/tornodes) que se puede usar en nuestro firewall.

# Técnicas y Herramientas

# El qué y el cómo

Existen multitud de herramientas para recopilar todo tipo de información, pero no debemos caer en el error de considerar la herramienta como un fin, sino como un medio.

Lo principal es entender cómo funcionan las cosas y luego seleccionar la herramienta adecuada. Y sobre todo, seguir un método que nos guíe en nuestra investigación.

En cuanto a las herramientas disponibles podemos consultar en:

- [OSINT Framework](https://osintframework.com/): Web interactiva con un catálogo muy ampio de herramientas y recursos organizados por categorías.
- [Ciberpatrulla OSINT](https://ciberpatrulla.com/): web donde hace una selección de herramientas interesantes.
- [OSINT.link](https://osint.link/): listado de recursos por categorías.
- [OSINT Techniques](https://inteltechniques.com/book1.html): Libro con más de 500 páginas sobre el tema. Tiene una sección de Resources con recursos accesibles
- [OSINT Handbook](https://i-intelligence.eu/resources/osint-toolkit): Documento muy amplio con más de 500 páginas sobre multitud de herramientas
- [Curso TCM](https://www.youtube.com/watch?v=qwA6MmbeGNo) sobre OSINT: En el canal de The Ciber Mentor hay un curso gratuíto de 5 horas sobre osint, con diversas técnicas y herramientas.
- Jason Haddix: tiene disponibles varios vídeos sobre su metodología de búsqueda de bugs (Bugs hunter's Metodology) y sobre la de análisis de aplicaciones (Application Analysis)

# Analizando sitios web

Dentro de los sitios web puede haber mucha información interesante, incluso en los comentarios del código. Vamos a ver algunas de estas técnicas.

- Descarga del un sitio web.

Para esta tarea es interesante dominar el comando wget, que permite incluso descargar un sitio entero. En este [enlace](https://www.linuxjournal.com/content/downloading-entire-web-site-wget) tenemos un ejemplo de descarga de un sitio completo, explicando todas las opciones empleadas.

- Versiones anteriores de un sitio web

Los sitios web cambian, evolucionan, e incluso desaparecen. Podemos acceder a veces al estado de un sitio web en el pasado, y acceder a información eliminada. Para ello emplearemos [The Wayback Machine](https://web.archive.org/). No solo guarda el contenido, también los archivos de descarga, permitiendo acceder a versiones antiguas de aplicaciones, juegos de videoconsolas antiguas, ... Se puede solicitar al que haga una copia del estado actual de u sitio.

Dispone de una API para comparar versiones de sitios, de manera que se pueden desarrollar scripst para analizar cambios. 

Un servicio similar es [archive.today](https://archive.ph/), pero hace copias bajo demanda, no de forma automática.

Si deseamos buscar en la caché del los buscadores podemos usar [cachedview.com](https://cachedview.com/), emplea los servicios de wayback machine para su tarea.

- Testigos on line

Un sitio puede variar a lo largo del tiempo, ¿como podemos verificar que algo estaba ahí en un momento dado?

Para validar y certificar contenidos de la web, se pueden emplear dos servicios

[

## eGarante

](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/reconocimiento_web.html#exe-accordion-0-0)[

## Save the Proof

](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/reconocimiento_web.html#exe-accordion-0-1)

# Buscando en información indexada

- **Buscadores web y dorks**

Existen diversos buscadores: google, yahoo!, Bing, Baidu, DuckDuckGo

Todos ellos se basan en recopilar en indexar lo que van encontrando los crawler (rastreadores) que emplean. En el caso de google, podemos consultar información al respecto en [www.google.com/bot.html](http://www.google.com/bot.html) 

Si no deseamos que los crawler indexen determinados contenidos de un sitio web, en el archivo robots.txt se lo podemos indicar. Esto a su vez puede servir de fuente de información para un atacante. Un ejemplo lo podemos tener aquí: [https://www.marca.com/robots.txt](https://www.marca.com/robots.txt) . Respetar esto es voluntario, aunque se suele hacer. Hay una forma de actuar llamada _security by obscurity_, que propone mantener ocultos los elementos que pueden comprometer la seguridad, no suele funcionar. 

Los google dorks o google hacking, son expresiones que podemos emplear como búsquedas más avanzadas. Permiten descubrir datos como credenciales, datos personales, patrones de formularios, ... Tenemos un amplísimo catálogo en la [google hacking database](https://www.exploit-db.com/google-hacking-database "ghdb") de exploit-db.

Algunos ejemplos pueden ser:

```processing
intext:"index of"".sql"
index.of.dcim
camera linksys inurl:main.cgi
```

- **Buscadores tecnológicos**

En vez de indexar contendidos, indexan servicios. Escanean la red buscando servidores con puertos activos, y almacenan los banners de los servicios, sería una base de datos de resultados de nmap.

Los más conocidos son:

1. [Shodan](https://www.shodan.io/): Si no te registras está my limitadas las búsquedas, ofrece búsquedas por CVE en sus cuentas empresariales. Se puede usar a través de API.
2. [Censys](https://censys.com): Similar al anterior, ofrece cuentas especiales para investigadores
3. [zoomeye](https://www.zoomeye.ai/): de origen chino, requiere reqistro y tiene límites de datos. Dispone de librería de python para su uso en herramientas propias.

Esto nos permite obtener información sin interactuar con el objetivo.

- **Búsqueda inversa de imágenes y vídeos**

Se trata de buscar dónde se ha publicado una determinada imagen o vídeo. se puede emplear para:

1. Comprobar uso adecuado de los derechos de autor: si disponemos de una imagen y no sabemos su origen para referenciar la fuente, si una imagen nuestra se ha publicado en otros sitios sin consentimiento, ... Para ello podemos usar [Berify](https://berify.com/).
2. Comprobar la veracidad de una imagen: hoy en día es muy frecuente encontrarse con bulos, que difunden imágenes que no se corresponden con el hecho o que están manipuladas. Esto permite detectar campañas de desinformación. En esta [guía](https://gijn.org/es/recurso/guia-avanzada-sobre-verificacion-de-contenido-de-video/) nos da consejos de cómo hacerlo.
3. Comprobar las publicaciones de un perfil en una red social: Buscar perfiles en redes sociales a partir de imágenes públicas de los mismos. Permite además detectar cuentas falsas que publican imágenes de otras personas, usurpando su personalidad.

Los buscadores disponen además de búsqueda de imágenes también. Las opciones disponibles pueden ser:

- Google: [https://images.google.com/](https://images.google.com/)
- Bing: el buscador de Microsoft también permite esta posibilidad
- Yandex: permite subir la imagen o mostrar el enlace a la misma.
- [Tineye](https://tineye.com/): tiene opciones de búsqueda avanzada de pago, que permite reconocimiento de imágenes a partir de la cámara del móvil o el uso de una API. Ofrece además plugins para diversos navegadores.
- Search by image: [Extensión](https://addons.mozilla.org/en-US/firefox/addon/search_by_image/) para firefox que permite búsqueda inversa de imágenes.

# Análisis de Archivos

# ¿Qué contiene realmente un archivo?

Las cosas no son siempre lo que parecen, o pueden ocultar algunos secretos. En análisis de archivos es fundamental para detectar amenazas, o explotar vulnerabilidades.

- **Identificación del formato**

El formato nos indica cual es su contenido.

Podemos ver la extensión, pero eso puede ser engañoso. Debemos tener en cuenta que la extensión en sistema Windows no se muestra, eso permite engaños, como el caso del famoso virus "I love you". Se enviaba un mensaje con el asunto Y LOVE YOU y un fichero adjunto LOVE-LETTER-FOR-YOU.txt.vbs. La extensión vbs no se mostraba, ya que windows la oculta, y se corresponde a un script de visual Basic. Al pulsar sobre el archivo, se descargaba y ejecutaba.

Posemos consultar los magic numbers para ver el formato interno del archivo, para ello emplearemos:

```processing
file <archivo>
```

Consultará los magic numbers al principio del archivo. Podemos ver también la información contenida mediante la herramienta _hexdump_.

```processing
hexdump -C <archivo>|head
```

Podemos consultar en este enlace todos los magic numbers para diferentes formatos: [https://en.wikipedia.org/wiki/List_of_file_signatures](https://en.wikipedia.org/wiki/List_of_file_signatures) 

- **Metadatos**

Junto al contenido, hay información adicional, como puede ser el autor, versión y herramienta de creación, fechas, ubicación, ... Esto son los metadatos.

Podemos averiguar por ejemplo, si una empresa usa una versióon vulnerable de alguna herramienta.

Para consultar metadatos podemos usar exiftool:

```processing
exiftool <archivo>
```

Podemos buscar archivos publicados en un determinado dominio empleando herramientas.

[- Metagoofil](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/anlisis_de_archivos.html#)

Permite descargar los archivos de un sitio web para posteriormente, analizarlos con otra herramienta. Podemos establecer pausas entre descargas, límites, tipos de archivos, ... Esta herramienta lo hace a través de Google, puede identificarnos como un bot y bloquearnos. Lo mejor es hacerlo a través de una VPN. Disponible en: [https://github.com/opsdisk/metagoofil](https://github.com/opsdisk/metagoofil) 

[-  Metafinder](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/anlisis_de_archivos.html#)

Es similar, pero permite emplear varios buscadores:Bing, Baidu. Disponible en: [https://github.com/Josue87/MetaFinder](https://github.com/Josue87/MetaFinder) 

[- Foca](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/anlisis_de_archivos.html#)

Herramienta que permite no solo descarga, también análisis, desarrollada por Chema Alonso y su equipo de Elevenpaths, Lleva un tiempo sin actualizar. Disponible en: [https://github.com/ElevenPaths/FOCA](https://github.com/ElevenPaths/FOCA) 

En este [artículo](https://outpost24.com/blog/metadata-hackers-best-friend/) nos explica cómo los metadatos pueden aportar mucha información sobre los objetivos.

- **Análisis de archivos de texto**

A veces debemos buscar en un archivo de texto. La herramienta que puede ayudarnos es _grep_. El formato de su uso es:

```processing
grep <patrón> <archivo>
```

También se puede encadenar con un pipe a la salida de otros comandos.

Las opciones más empleadas son:

- -i , --ignore-case. Se consideran iguales mayúsculas y minúsculas
- -r , --recursive. Busca en todos los archivos del directorio y en los subdirectorios de forma recursiva. Si lo combinamos con --include=*.php, busca sólo en estos archivos. 
- -e <patrón>, --regexp=patrón. Se emplea con expresiones regulares
- --color. Colorea las ocurrencias encontradas.

Es una herramienta que podemos emplear en análisis de código fuente. En este [artículo](https://secnhack.in/source-code-audit-with-grep-command/) nos lo explica.

- **Texto en archivos binarios**

A veces necesitamos buscar un texto en archivos binarios, donde las herramientas tienen menos éxito, por ejemplo en pdf o imágenes.

Podemos convertir en texto un pdf con la herramienta _pdftotext_ y luego aplicar grep.

```processing
$ pdftotext -layout archivo.pdf archivo.txt
```

Si el texto está en una imagen, debemos extraerlo empleando un OCR, las herramientas más empleadas son:

[- Tesseract](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/anlisis_de_archivos.html#)

Disponible en kali a través de sus repositorios, y también para windows. Dispone además de servicios on-line. El proyecto está en [https://github.com/tesseract-ocr/tesseract](https://github.com/tesseract-ocr/tesseract)   

[- EasyOCR](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/anlisis_de_archivos.html#)

Librería de python que se puede emplear en proyectos propios, disponible en https://github.com/JaidedAI/EasyOCR .Soporta múltiples idiomas y tiene una demo [on-line](https://www.jaided.ai/easyocr/). 

Podemos además extraer cadenas de texto de archivos binarios, incluso ejecutables:

```processing
$ strings hola.exe
```

- **Aclarar imágenes pixeladas**

A veces se pixela una imagen, o parte de ella, para ocultar detalles de la misma. Este proceso, a veces se puede revertir. En su lugar es mejor usar cajas opacas. 

Las herramientas disponibles dan buenos resultados para textos pixelados:

1. Depix: [https://github.com/spipm/Depixelization_poc](https://github.com/spipm/Depixelization_poc) 
2. DepixHMM: [https://github.com/JonasSchatz/DepixHMM](https://github.com/JonasSchatz/DepixHMM) 
3. Unredacter: [https://github.com/BishopFox/unredacter](https://github.com/BishopFox/unredacter) 

Para imágenes pixeladas, como rostros o paisajes, lo más efectivo es buscar el original mediante búsqueda inversa.

# Información personal

# Investigaciones

- **Emails**

Si disponemos de un e-mail, podemos rastrear a ver si se ha empleado en algún servicio para darse de alta, si aparece en alguna brecha de seguridad. ... Si metemos el mail diversos servicios, nos da un mensaje indicando que el mail ya está registrado, esto nos indica que esta persona es usuaria de este servicio.

Las herramientas que nos pueden ayudar son:

[-  Hunter](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/informacin_personal.html#)

Servicio web, que permite uso limitado a 25 resultados con registro gratuíto. Busca direcciones de correo de un determinado dominio. Disponible en [https://hunter.io/](https://hunter.io/) 

[- Infoga](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/informacin_personal.html#)

Emplea diversas fuentes: buscadores, shodan, ... e incluso información de brechas de seguridad como Have I been Pwned. Disponible en [https://github.com/Security-Tools-Alliance/Infoga](https://github.com/Security-Tools-Alliance/Infoga) 

[- IKY (I know you)](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/informacin_personal.html#)

Recopila información a partir de una dirección de correo. Se requieren API keys de diversos servicios para usarla, genera informes en formato json. Disponible en [https://github.com/kennbroorg/iKy](https://github.com/kennbroorg/iKy) y también en [https://kennbroorg.gitlab.io/ikyweb/](https://kennbroorg.gitlab.io/ikyweb/) 

- **Redes Sociales**

Para poder buscar en redes sociales, necesitaremos crear un perfil en las mismas. Este perfil "falso" es el que usaremos, pero no para interactuar con el objetivo, sólo para recabar información. Si creamos identidades falsas para hacer ingeniería social con ellas, no sería OSINT (ni legal)

Lo primero es averiguar dónde tiene cuenta nuestro objetivo, si disponemos de un nickname, podemos barrer varias empleando la herramienta [Sherlock](https://github.com/sherlock-project/sherlock)

Para usarlo en kali podemos instalarlo con apt:

```processing
$ sudo apt sherlock
```

Y buscaremos simplemente poniendo:

```processing
$ sherlock <username>
```

Si deseamos buscar información dentro de X (antiguo Twitter), hoy en día lo mejor es emplear la búsqueda avanzada dentro de la propia red. Nos va a permitir ver las publicaciones de una cuenta, las dirigidas a una cuenta, y las que mencionan una cuenta. En este [artículo](https://odint.net/twitter-osint/) los da consejos para ello.

Existen algunas herramientas que se pueden emplear:

[- Tinfoleak](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/informacin_personal.html#)

Permite buscar información en cuentas de twitter sin registro, el resultado se envía a tu correo electrónico: [https://tinfoleak.com/](https://tinfoleak.com/) 

[- Tafferugli](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/informacin_personal.html#)

Permite investigaciones sobre propaganda en twitter, abandonado hace cuatro años: [https://github.com/sowdust/tafferugli](https://github.com/sowdust/tafferugli) 

[- Twint](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/informacin_personal.html#)

Muy empleada en el pasado, al no requerir API Key, archivada en 2022: [https://github.com/twintproject/twint](https://github.com/twintproject/twint) 

Desde que Elon Musk adquiere Twitter, muchos usuarios abandonaron esta red y se pasaron a Mastodon y Threads, para hacer OSINT sobre estas redes debemos aprender sobre su uso, en este [artículo](https://www.secjuice.com/mastodon-osint-a-comprehensive-introduction/) se describe Matodon.

En el caso de Instagram, la herramienta disponible es Osintgram: [https://github.com/Datalux/Osintgram](https://github.com/Datalux/Osintgram) 

En esta herramienta podremos obtener información de cuentas públicas y de cuentas a las que se sigue. En el repositirio nos indica como emplear la herramienta, pero debemos disponer de una cuenta en Instagram para poder emplearla.

# Filtraciones

# Leaks

Puede ocurrir que información de interés se haya publicado como fruto de una filtración, este tipo de datos se denominan _leaks_, A veces las realizan hactivistas, pero en muchos casos son ciberdelincuentes, que al no cobrar la recompensa, publican los datos obtenidos de forma fraudulenta.

- Servicios para comprobar filtraciones.

[- Have I been pwned?](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/filtraciones.html#)

Servicio para comprobar si un correo, teléfono o contraseña forma parte de una filtración. Permite la descarga de 17 Gb de contraseñas comprometidas. Tiene una API gratuíta, pero con ciertas limitaciones de demanda. Se accede en [https://haveibeenpwned.com/](https://haveibeenpwned.com/) 

[- Dehashed](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/filtraciones.html#)

Ofrece búsquedas además de nombres de usuario, IP, ... Requiere registro para su uso y tiene servicios de pago. La url es: [https://dehashed.com/](https://dehashed.com/) 

[- GhostProject](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/filtraciones.html#)

Servicio completamente de pago. En enlace es: [https://ghostproject.fr/](https://ghostproject.fr/) 

- Sitios anónimos

Existen unos sitios, llamados paste, donde se pueden compartir pequeños trozos de código para copiar y pegar. El más conocido es [Pastebin](https://pastebin.com/)., pero hay otros como AnomPaste, PasteHTML y Pastie. Son fuente de filtraciones, podemos emplear el siguiente dork: _site:pastebin.com gmail.com_

La herramienta [pastenum](https://github.com/shadowbq/pastenum) nos permite automatizar búsquedas en estos sitios, pero está bastante abandonada.

- Fugas en repositorios de código fuente

En github y gitlab podemos buscar información relevante, como API Keys o contraseñas. A veces los desarrolladores, por error o descuido, dejan esta información en su código. Se pueden buscar mediante dorks y también mediante la herramienta [gitleaks](https://github.com/gitleaks/gitleaks), disponible en Kali, para los repositorios locales o descargados. Tanto github como gitlab permiten buscar este tipo de información y bloquearán el commit para evitar la fuga, pero ... a veces se cuelan estos datos.

Otras herramientas pueden ser [TruffleHog](https://github.com/trufflesecurity/trufflehog) , para repositorios on line, y [GitDump](https://github.com/Ebryx/GitDump) para clonar todos los repositorios de un sistema y posteriormente analizarlos.

- Herramientas de línea de comandos

Hay herramientas de línea de comandos que buscan en varios de los servicios comentados, pero requieren de API Key y configurarlos. Por ejemplo [H8Mail](https://github.com/khast3x/h8mail) o [WhatBreach](https://github.com/Ekultek/WhatBreach). A partir de un mail o de un nombre de usuario, realizan la búsqueda.

# Frameworks

# Todo en uno

Existen diversos frameworks que nos ofrecen gran cantidad de funciones integradas para este tipo de tareas de investigación, vamos a ver los principales:

[- OSR Framework](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/frameworks.html#)

Desarrollada en Python, tiene diversos módulos para diferentes búsquedas. Disponible en github y en kali a través de apt.

[- theHarvester](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/frameworks.html#)

Requiere de API key para varios de sus módulos, disponible en Kali igualmente.

[- Recon-ng](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/frameworks.html#)

Desarrollada en Python, almacena la información en una base de datos y genera informes. Disponible en Kali a través de apt, y en github. Ofrece tres aplicaciones: recon-ng, recon-web y recon-cli.

[- Foca](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/frameworks.html#)

Recopila y organiza información de metadatos de los ficheros de un sitio.Sólo disponible en Windows.

[- Maltego](https://aulavirtual33.educa.madrid.org/ies.elcanaveral.mostoles/pluginfile.php/167062/mod_exescorm/content/29/frameworks.html#)

Funciona con transformadas, está preinstalada el Kali en su versión community. Obtiene y organiza datos de personas e infraesructuras. Disponible un curso básico de uso en [youtube](https://www.youtube.com/watch?v=ILYxtP_JLdQ&list=PL7DhkxY3DMy17SBblDHSzU0j5rRJ36iQW).

Aunque todas ellas prometen mucho, la realidad dista mucho de las espectivas, cada vez es más frecuente disponer de herramientas de pago.

