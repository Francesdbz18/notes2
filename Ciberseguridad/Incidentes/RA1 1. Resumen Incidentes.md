## Introducción y Justificación

- Los sistemas informáticos son fundamentales en empresas; un fallo puede causar pérdidas económicas por interrupciones, pérdida de datos, o daños en la reputación.
- **La seguridad informática requiere inversión**, pero ayuda a evitar costes mayores, incluidas pérdidas intangibles como el tiempo de recuperación y la imagen de la empresa.
- Ningún sistema es 100% seguro; siempre debemos prepararnos para minimizar el daño cuando se produce un incidente.

## Clasificación de la Seguridad

### Seguridad Física

- Protege el hardware y cables frente a incendios, inundaciones, robos, apagones y desastres naturales.
- Mecanismos de defensa:
    - Mobiliario ignífugo, sistemas antiincendios, impermeabilización, cámaras y controles de acceso biométricos, uso de SAI para apagones, contacto con organismos estatales de meteorología y geografía.


### Seguridad Lógica

- Complementa la seguridad física, protegiendo software y datos frente a robos, virus, manipulaciones, y ataques de red.
- Medidas: cifrado de datos, contraseñas, sistemas biométricos, copias de seguridad, antivirus, firewalls, listas de control de acceso.


### Seguridad Activa

- Medidas preventivas: contraseñas, control de acceso, autenticación, encriptación, firmas digitales, sistemas con tolerancia a fallos.


### Seguridad Pasiva

- Minimiza daño tras incidentes: discos redundantes, SAI, copias de seguridad para restaurar datos.

## Definición de Ciberseguridad

- **Ciberseguridad**: herramientas, políticas, salvaguardas, formación, y tecnología para proteger activos y usuarios en el ciberespacio.
- Definiciones oficiales (ISO, ITU, CCN-CERT): preservación de la **Confidencialidad, Integridad y Disponibilidad (CID)** de la información.

## Tipos de Activos

- Activo de información: datos que merecen protección, sean tangibles o intangibles.
- Activo TIC: software o hardware en el entorno de negocio.

## Amenazas – Tipos de Malware

| Tipo de malware | Característica principal | Mecanismos de defensa |
| :-- | :-- | :-- |
| Adware | Publicidad no deseada | Evitar descargas dudosas, revisar instalaciones |
| Spyware | Robo de información | Usar antivirus, no conectar USB desconocidos |
| Gusanos | Autorreplicación en red | Actualización, antivirus, desactivar autoejecución |
| Troyano | Se disfrazan de software legítimo | Sistemas y antivirus actualizados, cuidado con webs fraudulentas |
| Ransomware | Bloqueo y/o cifrado de datos para pedir rescate | No abrir adjuntos dudosos, copias de seguridad |
| Botnets | Red de dispositivos infectados | Mantener dispositivos seguros y actualizados |
| Apps maliciosas | Uso indebido de permisos | Descargar sólo de tiendas oficiales, revisar permisos |

## Dimensiones y Principios de la Seguridad

### Confidencialidad

- Priva el acceso a la información a los no autorizados; implementado con cifrado (simétrico/asimétrico).
- Diferencia con privacidad: privacidad aplica solo a datos personales; confidencialidad a cualquier dato sensible.


### Integridad

- Garantiza que la información no ha sido modificada; se implementa con funciones hash (ejemplo: SHA-256).


### Disponibilidad

- La información debe estar accesible cuando se necesita; prevención ante DoS, ransomware, desastres.


### Autenticación

- Verifica identidad de usuarios/sistemas/procesos; factores: contraseñas, biometría, certificados digitales, tarjetas inteligentes.


### No repudio

- Imposibilita que una parte niegue haber realizado una acción; importancia de trazabilidad y firmas digitales.


### Control de acceso

- Gestiona autenticación, autorización y auditoría siguiendo principios de “necesidad de conocer” y “mínimo privilegio”.
- Separación de funciones para evitar fraude (ejemplo: compras y pagos separados).

## Criptografía

### Definición y objetivo

- Ciencia que estudia métodos para ocultar información, esencial para privacidad y protección de datos.


### Tipos

- **Simétrica**: misma clave para cifrar y descifrar (ejemplos: AES, DES). Ventaja: rapidez; desventajas: intercambio de claves y escalabilidad.
- **Asimétrica**: claves pública y privada distintas (ejemplos: RSA, Diffie-Hellman, DSA). Ventaja: intercambio seguro; desventaja: más lenta, claves largas.
- **Híbrida**: combina ambas; uso común en comunicaciones seguras (ejemplo: HTTPS, SSH).

### Algoritmo Diffie-Hellman

- Permite intercambio seguro de claves usando funciones matemáticas unidireccionales (logaritmos discretos).

### Funciones Hash

- Operaciones unidireccionales que producen resúmenes únicos de datos; algoritmos populares: MD5, SHA-256, SHA-512.

## Firma Digital

- Usa cifrado de clave privada sobre el hash del mensaje. Permite autenticación, integridad y no repudio de los datos.
- Ejemplo:
    - Celia firma un mensaje a David cifrando el hash con su clave privada. David verifica autenticidad descifrando con la clave pública y comparando el resumen hash.


## Certificados Digitales

- Documento que asocia clave pública con identidad. Contiene datos personales, validez, par de claves y firma de la Autoridad Certificadora.
- Se usa para autenticación y firma digital en trámites (ejemplo: FNMT, DNIe).
- Formatos: .pfx/.p12 (privada, exportación segura), .cer/.crt (pública, distribución general).

## DNI Electrónico

- Acredita identidad, permite firma digital con validez legal. Incorpora chip con certificados digitales y claves.
- Tipos:
    - DNIe (chip físico)
    - DNI 3.0 (NFC, móvil)
    - DNI 4.0 (app móvil, desde 2021)

## Infraestructura de Clave Pública (PKI)

- Modelo basado en terceras partes de confianza (Autoridades de Certificación).
- Facilita distribución y validación de certificados para autenticación y comunicaciones seguras.

