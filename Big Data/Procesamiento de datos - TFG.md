F1-webapp: beber datos de la API 
API -> Nifi -> Kafka -> Nifi -> Python (Flask)
¿Qué datos voy a procesar? ¿Cómo?

1. API
¿Datos de pilotos?
Algo que pueda dividirse en 2.

2. Nifi
Consumir API y dividir los datos, enviarlos como mensajes a Kafka en dos topics.

3. Kafka
Consumir los mensajes y transmitirlos de nuevo. Los topics deben tener dos particiones y un factor de replicación de dos.

4. Nifi
Procesar los datos para unificar su formato. Almacenar como JSON.

5. Python (Flask)
Aplicación web simple que muestre los datos. 
JSON -> Python (Pandas DataFrame) -> Matplotlib
