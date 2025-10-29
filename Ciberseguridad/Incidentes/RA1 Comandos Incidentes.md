GPG o Gnu Privacy Guard es una herramienta para cifrado y firmas digitales que utiliza una serie de algoritmos como ElGamal, CAST5, 3DES, AES y Blowfish. La aplicación GPG genera un archivo de salida .gpg en el mismo directorio donde se ubique el archivo origen. El archivo de salida es binario.

- -c: la orden **-c (--symetric)**, cifra utilizando clave simétrica o privada; para ello nos solicita una contraseña o passphrase, que se emplea en el cifrado y descifrado (clave simétrica). Se genera un archivo binario con extensión .gpg.
- -a: añadiendo la opción **-a (--armor)** se guarda el documento cifrado con caracteres ASCII, en formato .asc. _**gpg -c -a fichero**_
- -d: esta es la orden para descifrar **(--decrypt)** el archivo cifrado.
- Por defecto, la herramienta utiliza CAST5 como algoritmo de cifrado simétrico. Si se quiere usar un determinado algoritmo de cifrado, se usa la opción **--cipher-algo**. Para ver los algoritmos disponibles ejecuta **gpg --version**.
- Existen 2 opciones para la generación de un par de claves: **--gen-key**  y **--full-generate-key**. En la primera de ellas básicamente solicita la identificación del propietario de las claves, con la segunda recoge otros datos antes de la creación de las claves.
- **gpg --list-keys**   o   **gpg -k**     para ver las claves públicas.
- **gpg --list-secret-keys**   o   **gpg -K**    para ver las claves privadas.
- Para publicar una clave pública en un servidor:   _gpg --send-keys --keyserver nombreServidor ClaveID_
- Para publicar una clave en el servidor por defecto (el de openpgp): _**gpg --send-keys ClaveID**_
- Para buscar una clave pública en el servidor:   _gpg --keyserver nombreServidor --search-keys ClaveID_
- Para buscar una clave pública en el servidor por defecto (el de openpgp): _**gpg --search-keys ClaveID**  
- Para descargar una clave pública:   _gpg --keyserver nombreServidor --recv-keys ClaveID_
- Para descargar una clave pública del servidor por defecto (el de openpgp): _**gpg --recv-keys ClaveID**  
- Para exportar la clave pública a un fichero:   _gpg --armor --output ficherodeclave --export ClaveID_
- Para exportar la clave privada a un fichero:   _gpg --armor --output ficherodeclave --export-secret-key ClaveID_
- Para importar una clave pública volcada en un fichero:   _gpg --import ficherodeclave_
- Para importar una clave privada volcada en un fichero: _gpg --allow-secret-key-import --import ficherodeclave_
- La orden para generar el certificado de revocación es:   _**gpg -o ficherorevocacion.asc --gen-revoke ClaveID**_
- Para importar a nuestra relación de claves (hacer efectiva la revocación): OJO, NO EJECUTAR MÁS QUE CUANDO SEA NECESARIO:   _gpg --import ficherorevocacion.asc_ 
- Para comunicar a los servidores de claves que nuestra clave ya no es válida:   _gpg --send-keys ClaveID_
- Para borrar claves privadas:  _gpg --delete-secret-key_ _ClaveID_
- Para borrar claves públicas:  **_gpg --delete-key ClaveID_**
- _gpg --output documentocifrado.gpg --encrypt --recipient ClaveID documentosincifrar_
- _gpg --output documentodescifrado --decrypt documentocifrado.gpg_

Los parámetros de _gpg_ para obtener la firma digital de documentos y realizar verificaciones son los siguientes:
- **--clear-sign**: se une la firma digital al contenido del archivo, el cual no se cifra (documento en claro). El resultado es un archivo ASCII.
- **-s (--sign)**: se une la firma digital al contenido del archivo, el cual se comprime y se cifra antes de ser firmado.
- **-b (--detach-sign)**: la firma se incluye en un archivo separado.El resultado es un archivo binario .sig.
- Para verificar la validez de las firmas digitales con _gpg_ se utiliza la opción **--_verify_**. Cuando se comprueba la firma en un archivo separado, se debe indicar también el archivo original.
- Para verificar la firma y extraer el documento se usa la opción -- **decrypt**.
- **-u (--local-user)**: para especificar el usuario firmante (saber qué clave del anillo debe usar para firmar).
- **-o (--output)**: para indicar el nombre del fichero destino.