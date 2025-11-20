# Guía de Estudio: Hacking Ético - Tema 1

## Conceptos fundamentales

### Definición de Hacking Ético

El **hacking ético** es el uso de habilidades y técnicas avanzadas para sobrepasar los límites de un sistema informático en cuanto a confidencialidad, integridad y disponibilidad, con la finalidad de encontrar debilidades para mitigarlas. El término proviene de la palabra "hack", que significa una solución rápida e ingeniosa para un problema. Es importante destacar que <mark style="background: #FFB8EBA6;">el hacking ético siempre se realiza con autorización expresa y dentro del marco legal.</mark>

### Principios de la Seguridad Informática (CIA+)

Los cinco principios fundamentales de la seguridad son:

| Principio            | Descripción                                                                               |
| -------------------- | ----------------------------------------------------------------------------------------- |
| **Confidencialidad** | Garantizar que la información es accesible únicamente a personas autorizadas              |
| **Integridad**       | Asegurar la veracidad de los datos previniendo cambios no autorizados                     |
| **Disponibilidad**   | Garantizar que los sistemas son accesibles cuando son requeridos por usuarios autorizados |
| **Autenticación**    | Garantizar la identidad del creador de un contenido mediante factores de autenticación    |
| **No repudio**       | El emisor no puede negar el envío de información, ni el receptor negar su recepción       |

## Clasificación de hackers

### Tipos según sus Intenciones

Los hackers se clasifican según sus motivaciones y métodos:

| Tipo                            | Descripción                          | Características                                                                                                           |
| ------------------------------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| **White Hat** (Sombrero Blanco) | Hackers éticos profesionales         | Actúan con <mark style="background: #FFB8EBA6;">permisos legales</mark>, mejoran la seguridad, notifican vulnerabilidades |
| **Black Hat** (Sombrero Negro)  | Ciberdelincuentes                    | Cometen delitos, realizan fraudes, extorsiones y robos para beneficio propio                                              |
| **Grey Hat** (Sombrero Gris)    | Entre los dos anteriores             | Incluye hacktivistas como Anonymous, no siempre cumplen la ley                                                            |
| **Script Kiddies/Newbies**      | Personas sin conocimientos avanzados | Usan herramientas de otros, pueden causar daños importantes sin comprenderlos                                             |

### Tipos de Intrusos según motivaciones

Clasificación adicional de intrusos por sus objetivos:

- **Cracker**: Buscan <mark style="background: #FFB8EBA6;">hacer daño</mark> y obtener beneficio económico
- **Phreaker**: Buscan conexión a Internet sin pagar (actualmente en desuso)
- **Spammer**: Generadores de correo basura
- **Lammer**: Script kiddie que actúa sin conocimientos
- **Insider**: Personal interno que actúa contra su propia empresa
- **Hacktivista**: Motivado por notoriedad y reivindicaciones
- **State-sponsored Hacker**: Actúa respaldado por un gobierno (espionaje estatal)

## Marco Legal Español

### Código penal

El **Código penal español** establece penas específicas para delitos informáticos:

**Artículo 197bis.1**: Prisión de 6 meses a 2 años por acceder sin autorización a sistemas de información vulnerando medidas de seguridad.

**Artículo 197bis.2**: Prisión de 3 meses a 2 años o multa de 3 a 12 meses por interceptar transmisiones no públicas de datos sin autorización.

**Artículo 197ter**: Prisión de 6 meses a 2 años o multa de 3 a 18 meses por producir, adquirir o facilitar programas informáticos o contraseñas para cometer delitos informáticos.

## Malware y amenazas

### Tipos de malware

Clasificación según su comportamiento:

| Tipo | Función |
|------|---------|
| **Exploit** | Aprovecha vulnerabilidades del software (incluye payload) |
| **Virus** | Se acopla a programas legítimos y se replica |
| **Ransomware** | Encripta información y exige rescate en criptomonedas |
| **Spyware** | Recopila actividad y datos del usuario |
| **Adware** | Genera publicidad no deseada |
| **Troyano** | Deja puerta de entrada al atacante |
| **Rootkit** | Proporciona acceso y control remoto total desapercibido |
| **Keylogger** | Captura pulsaciones de teclado para obtener credenciales |
| **Gusano** | Se autopropaga por redes sin intervención |
| **Bacteria** | Se replica repetidamente para saturar memoria |
| **Bomba lógica** | Permanece oculta hasta que se dispara bajo ciertas condiciones |
| **Cryptojacking** | Usa CPU del sistema para minar criptomonedas |

### Ejemplos históricos de Malware

Casos relevantes que marcaron la historia:

- **Melissa (1999)**: Infectó 4 millones de equipos en 3 días mediante correo electrónico
- **I Love You (2000)**: Infectó 40 millones de equipos en 6 horas usando Visual Basic
- **Stuxnet (2010)**: Infectaba controladores industriales (PLC) usando vulnerabilidades zero-day
- **WannaCry (2017)**: Ransomware que infectó 200,000 equipos explotando la vulnerabilidad EternalBlue de Windows

## Vulnerabilidades

### Definición y tipos

Una **vulnerabilidad** es un fallo de diseño, configuración o programación que altera el comportamiento normal del sistema y permite accesos o acciones no previstas.

### Causas principales

- **Errores de programación**: Pueden ser no intencionados o backdoors deliberados
- **Librerías de terceros vulnerables**: Ejemplo: Log4Shell (CVE-2021-44228) en log4j
- **Frameworks con fallos**: Ejemplo: Spring4Shell (CVE-2022-22965)
- **Módulos del SO**: Permiten escalar privilegios
- **Mal uso de criptografía**: Ejemplo: Zerologon (CVE-2020-1472)
- **Vulnerabilidades hardware**: Aprovechan ejecución especulativa o fallos en memoria DDR DRAM

### Sistema de codificación CVE

El sistema **CVE** (Common Vulnerabilities and Exposures) utiliza el formato:

$$
\text{CVE-yyyy-XXXXX}
$$

Donde:
- <mark style="background: #D2B3FFA6;">**yyyy**: Año de descubrimiento</mark>
- <mark style="background: #BBFABBA6;">**XXXXX**: Número asignado</mark>

### Métrica CVSS

El sistema **CVSS** (Common Vulnerability Scoring System) clasifica la gravedad:

| Rango      | Gravedad |
| ---------- | -------- |
| 1.0 - 3.9  | Baja     |
| 4.0 - 6.9  | Media    |
| 7.0 - 8.9  | Alta     |
| 9.0 - 10.0 | Crítica  |

Existen además **métricas temporales** (gravedad según el momento) y **métricas de entorno** (dependen del sistema) que ajustan la puntuación base.

### Catálogos relacionados

MITRE mantiene catálogos complementarios:

- **<mark style="background: #FFB8EBA6;">CWE</mark>** (Common Weakness Enumeration): Clasificación de tipos de vulnerabilidades con lista de las 25 más comunes
- **<mark style="background: #FFB8EBA6;">CAPEC</mark>** (Common Attack Pattern Enumerations and Classifications): Recopilación de métodos y patrones de ataque más empleados

## Pentesting (Test de Intrusión)

### Definición

Un **pentest** es una <mark style="background: #FFB8EBA6;">acción intrusiva autorizada</mark> contra un sistema para mejorar su seguridad, siempre con el permiso explícito de la organización y generalmente con cláusula de confidencialidad.

### Tipos de auditorías

**Según el conocimiento**:

| Tipo            | Descripción                                           |
| --------------- | ----------------------------------------------------- |
| **Caja negra**  | Conocimiento similar al de un atacante externo        |
| **Caja blanca** | Conocimiento total, incluye revisión de código fuente |
| **Caja gris**   | Conocimiento parcial con algunos permisos limitados   |

**Según la posición**:

- **Perimetral**: Sin vía de entrada, hay que encontrarla
- **Interna**: Acceso como empleado con escasos privilegios
- **Interna con privilegios**: Acceso a configuraciones, código y políticas de seguridad

**Según el alcance**:

- Auditorías web
- Auditorías de aplicaciones móviles
- Auditorías wireless y VoIP
- Pruebas de stress DoS/DDoS

### Contrato previo

Antes de iniciar un pentest se debe establecer un contrato que incluya [1]:

- **Alcance**: Sistemas que se van a auditar
- **Ventanas de actuación**: Rango temporal permitido
- **Técnicas**: Ingeniería social, DoS, DDoS, exploits, etc.
- **Autorización expresa**: Permiso explícito documentado
- **Entregables**: Informes y documentación acordada

### Fases del Pentest

El proceso de pentesting consta de cinco fases:

1. **Footprinting (reconocimiento pasivo)**: Fase no intrusiva, se recaba información de fuentes públicas usando técnicas OSINT
2. **Fingerprinting (reconocimiento activo)**: Se interactúa directamente con el objetivo mediante análisis de puertos y detección de vulnerabilidades
3. **Explotación**: Se diseña y aplica un vector de ataque usando exploits para comprometer el objetivo
4. **Postexplotación**: Se consolida el compromiso, se escalan privilegios y se realiza pivoting hacia otras máquinas
5. **Documentación**: Se elaboran informes técnicos y ejecutivos con los resultados

### Metodologías principales

**PTES** (Penetration Testing Execution Standard): Establece 7 fases e incluye guía técnica con herramientas útiles [1].

**OSSTMM** (Open Source Security Testing Methodology Manual): Metodología de acceso libre, versión actual de 2010, con certificación STAR y 5 canales de seguridad (humana, física, inalámbrica, telecomunicaciones, redes de datos) [1].

**OWASP** (Open Web Application Security Project): Ofrece tres guías especializadas [1]:
- WSTG: Para aplicaciones web
- MASTG: Para aplicaciones móviles
- FSTM: Para firmware IoT

### Informes finales

Se generan dos tipos de informes:

**Informe técnico**:
- Dirigido a personal de programación o sistemas
- Incluye metodología, herramientas y estándares utilizados
- Soluciones genéricas a problemas detectados
- Vulnerabilidades ordenadas por riesgo o naturaleza
- Indicación de posibles falsos positivos

**Informe ejecutivo**:
- Resumen sin detalles técnicos
- Estado de seguridad de los sistemas
- Resultados obtenidos
- Formato PowerPoint para presentación al cliente

## Equipos de seguridad

Las organizaciones dividen sus equipos de seguridad por colores:

| Equipo          | Función                                                                      |
| --------------- | ---------------------------------------------------------------------------- |
| **Red team**    | Seguridad ofensiva, hacking ético                                            |
| **Blue team**   | Seguridad defensiva, respuesta ante incidentes, análisis forense, bastionado |
| **Yellow team** | Desarrollo seguro de aplicaciones                                            |

## Recursos de formación

### Plataformas CTF (Capture The Flag)

Los CTF son ejercicios de entrenamiento donde se busca obtener una "flag" (código) [1]:

**Tipos de CTF**:
- **Retos (Challenges)**: Crypto, Stego, Web, Forensics, Reversing, Pwn, Hardware
- **Máquinas (Boxes)**: Explotación completa de sistemas
- **Redes (Networks/Labs)**: Simulación de red empresarial con pivoting

**Plataformas principales** [1]:
- **Atenea** (CCN-CERT): Plataforma española con academia integrada
- **Academia Hacker** (INCIBE): Talleres y competiciones para nuevos talentos
- **Una al Mes** (Hispasec): Reto mensual
- **PicoCTF** (Carnegie Mellon): Recursos de aprendizaje y retos desde 2019
- **CTF Time**: Publicación de eventos y retos pasados
- **HackTheBox**: Máquinas con ranking y HTB Academy para certificación
- **TryHackMe**: Laboratorios (rooms) con contenido gratuito y premium
- **VulnHub**: Repositorio con más de 700 máquinas vulnerables
- **HackMyVM**: Repositorio de máquinas vulnerables
- **Proving Grounds** (OffSec): Versión gratuita (Play) y de pago (Practice)

### Certificaciones Profesionales

Principales certificaciones del sector [1]:

| Certificación | Organización       | Nivel             | Características                          |
| ------------- | ------------------ | ----------------- | ---------------------------------------- |
| **CEH**       | EC-Council         | Básico-Intermedio | Bajo contenido práctico, mejorado en v12 |
| **Pentest+**  | CompTIA            | Intermedio        | Cubre todas las fases                    |
| **eJPT**      | eLearnSecurity     | Básico            | Para principiantes                       |
| **eCPPT**     | eLearnSecurity     | Avanzado          | Nivel profesional                        |
| **HTB CPTS**  | Hack The Box       | Intermedio        | Especialista en pentesting               |
| **PNPT**      | TCM Security       | Intermedio        | Creada por The Cyber Mentor              |
| **OSCP**      | Offensive Security | Avanzado          | La más prestigiosa y compleja            |

### Plataformas Bug Bounty

Programas de recompensas por reporte de vulnerabilidades:

- **Bugcrowd**: Programas de principales empresas
- **HackerOne**: Una de las plataformas más importantes
- **Intigriti**: Plataforma de ámbito europeo
- **Immunefi**: Especializada en protección de activos digitales y criptomonedas

## Herramientas

### Distros para hacking

**Kali Linux**: La principal distribución, ofrece múltiples formatos (VM, ISO, ARM, Cloud).

**Alternativas**:
- **ParrotOS**: Distribución completa alternativa
- **BlackArch**: Basada en Arch Linux
- **CommandoVM**: Convierte Windows en distribución de seguridad ofensiva

## Red Tor

dffdf

---

## Preguntas de Repaso

1. ¿Cuáles son los cinco principios de la seguridad informática?
2. ¿Qué diferencia existe entre White Hat, Black Hat y Grey Hat?
3. ¿Qué penas establece el Código Penal español para acceso no autorizado a sistemas?
4. ¿Cuál es el formato del sistema CVE?
5. ¿Qué rangos de puntuación CVSS corresponden a vulnerabilidades críticas?
6. ¿Cuáles son las cinco fases de un pentest?
7. ¿Qué diferencia hay entre auditoría de caja negra, blanca y gris?
8. ¿Qué elementos debe incluir el contrato previo a un pentest?
9. ¿Qué es OSINT y en qué fase se utiliza?
10. ¿Qué diferencia hay entre Red Team y Blue Team?
11. ¿Qué es un exploit y qué es un payload?
12. ¿Qué es ransomware y cómo opera?
13. ¿Qué fue Stuxnet y qué lo hizo especial?
14. ¿Qué es un Script Kiddie?
15. ¿Qué catálogos mantiene MITRE además de CVE?
16. ¿Qué tipos de CTF existen?
17. ¿Cuál es la certificación más prestigiosa en hacking ético?
18. ¿Qué metodología de pentesting ofrece certificación STAR?
19. ¿Qué diferencia hay entre footprinting y fingerprinting?
20. ¿Qué es pivoting en la fase de postexplotación?

---

## Glosario de Términos Clave

- **CVE**: Common Vulnerabilities and Exposures
- **CVSS**: Common Vulnerability Scoring System
- **CWE**: Common Weakness Enumeration
- **CAPEC**: Common Attack Pattern Enumerations and Classifications
- **OSINT**: Open Source Intelligence
- **CTF**: Capture The Flag
- **Pentest**: Penetration Testing (Test de Intrusión)
- **Exploit**: Código que aprovecha una vulnerabilidad
- **Payload**: Acción maliciosa que ejecuta un exploit
- **Zero-day**: Vulnerabilidad desconocida sin parche disponible
- **Pivoting**: Usar una máquina comprometida para acceder a otras
- **Escalación de privilegios**: Obtener permisos superiores en un sistema
- **Bug Bounty**: Programa de recompensas por vulnerabilidades
- **Footprinting**: Reconocimiento pasivo sin interacción directa
- **Fingerprinting**: Reconocimiento activo con interacción directa
- **Backdoor**: Puerta trasera dejada intencionalmente
- **Rootkit**: Herramienta de acceso y control remoto oculto
- **Ransomware**: Malware que encripta datos y exige rescate
- **Phishing**: Suplantación de identidad por correo electrónico


Referencias:
[1] HackingEtico_Tema1.docx