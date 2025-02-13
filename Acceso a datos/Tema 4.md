RA4: 10 preguntas
RA5: 5 preguntas Bases de datos XML en este examen       
Oracle
Neodatis - bbdd objetos
Teoría - siglas, características de BBDD objeto-relacionales y orientadas a objetos, herencia, multiplicidad, relaciones (tablas anidadas)

  
4.1. Introducción

**4.2. Bases de datos Objeto-Relacionales - Oracle** 
4.2.1 Características
4.2.2 Tipos de Objetos   
          Actividad 4.1
4.2.2.1 Métodos  
          Actividad 4.2
4.2.3 Tablas de objetos  
          Actividad 4.3
4.2.4 Tipos de colección
4.2.1 Varrays  
          Actividad 4.4
4.2. Tablas anidadas
4.2.5 Referencias
4.2.6 Herencia de tipos
4.2.7 [Ejemplo de modelo relacional y objeto relacional](https://aulavirtual33.educa.madrid.org/ies.sanjuandelacruz.pozuelodealarcon/mod/resource/view.php?id=86380 "Ejemplo de modelo relacional y objeto relacional")

```sql
CREATE OR REPLACE TYPE DIRECCION AS OBJECT
(
  CALLE  VARCHAR2(25),
  CIUDAD VARCHAR2(20),
  CODIGO_POST NUMBER(5),
  MEMBER PROCEDURE SET_CALLE(C VARCHAR2),
  MEMBER FUNCTION GET_CALLE RETURN VARCHAR2  
);
CREATE OR REPLACE TYPE PERSONA AS OBJECT
(
  CODIGO NUMBER,
  NOMBRE VARCHAR2(35),
  DIREC  DIRECCION,
  FECHA_NAC DATE
);
/
drop type persona force;
CREATE OR REPLACE TYPE PERSONA AS OBJECT
(
  CODIGO NUMBER,
  NOMBRE VARCHAR2(35),
  DIREC DIRECCION,
  FECHA_NAC DATE,
  MAP MEMBER FUNCTION POR_CODIGO RETURN NUMBER
);
/
CREATE OR REPLACE TYPE BODY PERSONA AS
  MAP MEMBER FUNCTION POR_CODIGO RETURN NUMBER IS
  BEGIN
    RETURN CODIGO;
  END;
END;
/

CREATE TABLE T_PERSONAS OF PERSONA ( CODIGO PRIMARY KEY );

desc t_personas;

INSERT INTO t_personas VALUES( 1, 'Juan Pérez', DIRECCION ('C/Los manantiales 5', 'GUADALAJARA', 19005), '18/12/1991' );
INSERT INTO T_PERSONAS (CODIGO, NOMBRE, DIREC, FECHA_NAC) VALUES ( 2, 'Julia Breña', DIRECCION ('C/Los espartales 25', 'GUADALAJARA', 19004), '18/12/1987' );
DECLARE 
    DIR DIRECCION := DIRECCION('C/Sevilla 20', 'GUADALAJARA', 19004); 
    PER PERSONA := PERSONA (5, 'MANUEL', DIR, '20/10/1987'); 
BEGIN 
    INSERT INTO T_PERSONAS VALUES (PER); --insertar 
    COMMIT; 
END; 
/
SELECT * FROM T_PERSONAS A WHERE A.DIREC.CIUDAD = 'GUADALAJARA';
SELECT CODIGO, A. DIREC FROM T_PERSONAS A;

CREATE OR REPLACE TYPE BODY DIRECCION AS
  --
  MEMBER PROCEDURE SET_CALLE(C VARCHAR2) IS
  BEGIN
    CALLE := C;
  END;
  --
  MEMBER FUNCTION GET_CALLE RETURN VARCHAR2 IS
  BEGIN
    RETURN CALLE;
  END;
END;
/
----USO DEL TIPO DIRECCION
DECLARE
  DIR DIRECCION := DIRECCION(NULL,NULL,NULL);
BEGIN
  DIR.SET_CALLE('La Mina, 3');
  DBMS_OUTPUT.PUT_LINE(DIR.GET_CALLE); 
  
  DIR := NEW DIRECCION ('C/Madrid 10','Toledo',45002);
  DBMS_OUTPUT.PUT_LINE(DIR.GET_CALLE); 
END;
/

SELECT NOMBRE, A. DIREC.GET_CALLE() FROM T_PERSONAS A;
UPDATE T_PERSONAS A 
    SET A. DIREC.CIUDAD = LOWER (A.DIREC.CIUDAD) 
WHERE A.DIREC.CIUDAD = 'GUADALAJARA';
DELETE T_PERSONAS A WHERE A.DIREC.CIUDAD = 'guadalajara';
DECLARE 
    CURSOR C1 IS SELECT * FROM T_PERSONAS; 
BEGIN 
    FOR I IN C1 LOOP 
        DBMS_OUTPUT.PUT_LINE(I.NOMBRE || ' - Calle: '|| I.DIREC.CALLE); 
    END LOOP; 
END; 
/
SET SERVEROUTPUT ON;

DECLARE 
    D DIRECCION:= DIRECCION ('C/Galiano 5', 'Guadalajara', 19004); 
BEGIN 
    UPDATE T_PERSONAS 
        SET DIREC = D WHERE NOMBRE =  'Juan Pérez'; 
    COMMIT; 
END; 
/

CREATE OR REPLACE TYPE RECTANGULO AS OBJECT
(
  BASE   NUMBER,
  ALTURA NUMBER,
  AREA   NUMBER,
  STATIC PROCEDURE PROC1 (ANCHO INTEGER, ALTO INTEGER),
  MEMBER PROCEDURE PROC2 (ANCHO INTEGER, ALTO INTEGER),
  CONSTRUCTOR FUNCTION RECTANGULO (BASE NUMBER, ALTURA NUMBER)
                       RETURN SELF AS RESULT
);
/  


CREATE TABLE TABLAREC (VALOR INTEGER);
/

CREATE OR REPLACE TYPE BODY RECTANGULO AS
-- 
  CONSTRUCTOR FUNCTION RECTANGULO (BASE NUMBER, ALTURA NUMBER)
                                   RETURN SELF AS RESULT IS  
  BEGIN
    SELF.BASE := BASE;
    SELF.ALTURA := ALTURA;
    SELF.AREA := BASE * ALTURA;
    RETURN;
  END;
--
  STATIC PROCEDURE PROC1 (ANCHO INTEGER, ALTO INTEGER) IS
  BEGIN
    INSERT INTO TABLAREC VALUES(ANCHO*ALTO);
    --ALTURA := ALTO; --ERROR NO SE PUEDE ACCEDER A LOS ATRIBUTOS DEL TIPO
    DBMS_OUTPUT.PUT_LINE('FILA INSERTADA');
    COMMIT;
  END;
--
MEMBER PROCEDURE PROC2 (ANCHO INTEGER, ALTO INTEGER) IS
  BEGIN    
    SELF.ALTURA := ALTO; --SE PUEDE ACCEDER A LOS ATRIBUTOS DEL TIPO
    SELF.BASE := ANCHO;
    AREA := ALTURA*BASE;
    INSERT INTO TABLAREC VALUES(AREA);
    DBMS_OUTPUT.PUT_LINE('FILA INSERTADA');
    COMMIT;
  END;
END;
/


--
DECLARE
  R1 RECTANGULO;
  R2 RECTANGULO;
  R3 RECTANGULO := RECTANGULO(NULL, NULL, NULL);
BEGIN
  R1 := NEW RECTANGULO(10, 20, 200);
  DBMS_OUTPUT.PUT_LINE('AREA R1: '||R1.AREA);

  R2 := NEW RECTANGULO(10,20);
  DBMS_OUTPUT.PUT_LINE('AREA R2: '||R2.AREA); 
 
  R3.BASE := 5;
  R3.ALTURA := 15;
  R3.AREA := R3.BASE * R3.ALTURA;
  DBMS_OUTPUT.PUT_LINE('AREA R3: '||R3.AREA);

  --USO DE LOS MÉTODOS DEL TIPO  RECTANGULO
  RECTANGULO.PROC1(10, 20);   --LLAMADA AL MÉTODO STATIC
  --RECTANGULO.PROC2(20, 30); --ERROR, LLAMADA AL MÉTODO MEMBER
  --R1.PROC1(5, 6);          --ERROR, LLAMADA AL MÉTODO STATIC 
  R1.PROC2(5, 10);           --LLAMADA AL MÉTODO MEMBER
END;
/
DECLARE 
    CURSOR C1 IS SELECT AREA FROM TABLAREC; 
    MAYOR NUMBER;
BEGIN 
    FOR I IN C1 LOOP 
        MAYOR :=  
    END LOOP; 
END; 
/
```

### Neodatis

**4.3 Bases de Datos orientadas a objetos (BDOO) -  Neodatis**  
4.3.1 Características de las Bases de Datos OO  
4.3.2 El estándar ODMG  
4.3.3 El lenguaje de consultas OQL  
4.4 Ejemplo de BDOO  
4.4.1 Consultas sencillas  
4.4.2 Consultas más complejas   
4.4.2.1 Crear una BD Neodatis a partir dle modelo relaiconal   
4.4.3 Modelo cliente/servidor de la base de datos
```java
    public static void main(String[] args) {  
        //creo la conexion  
        ODB odb = ODBFactory.open("Equipos.db");  
        E01_Paises pais1 = new E01_Paises(1, "Espana");  
        E01_Paises pais2 = new E01_Paises(2, "Mexico");  
		 // Creo los equipos  
		Jugadores j1= new Jugadores ("Mar�a", "voleibol", "Madrid", 14, pais1);  
		Jugadores j2= new Jugadores ("Miguel", "tenis", "Madrid", 15, pais1);  
		Jugadores j3= new Jugadores ("Mario", "baloncesto", "Guadalajara", 15, pais2);  
		Jugadores j4= new Jugadores ("Alicia", "tenis", "Madrid", 14, pais1);  
        // Inserto los objetos        
        OID oid1 = odb.store(j1);       
        odb.store(j2);       
        odb.store(j3);       
        odb.store(j4);       
        odb.store(pais1);       
        odb.store(pais2);  
        System.out.println(oid1);        
        OID oid2 = odb.getObjectId(j1);        
        System.out.println(oid2);  
        // sacar los datos de todos los jugadores        
        Objects<Jugadores> objects = odb.getObjects(Jugadores.class);  
        int i = 1;  
  
        System.out.println(objects.size() + " jugadores:");  
  
        while(objects.hasNext()){  
            Jugadores jug= objects.next();  
            System.out.println((i++) + "\t: " + jug.getNombre() + "*" +  
                    jug.getDeporte() + "*" + jug.getCiudad() + "*"
                    + jug.getEdad());  
        }  
        System.out.println("------------");  
  
      ///////CONSULTA 1//////////  
  
      IQuery query = new CriteriaQuery(Jugadores.class, Where.equal("deporte", "tenis"));  
      query.orderByDesc("edad");  
      i = 1;  
  
      Objects<Jugadores> objects1 = odb.getObjects(query);  
  
      System.out.println("Jugadores que juegan al tenis: ");  
  
      while(objects1.hasNext()){  
          Jugadores jug = objects1.next();  
  
          System.out.println((i++) + "\t: " + jug.getNombre() + "*" +  
                  jug.getDeporte() + "*" + jug.getCiudad() + "*" + jug.getEdad());  
      }  
      System.out.println("------------");  
  
        IQuery query2 = new CriteriaQuery (Jugadores.class,Where.equal("nombre", "Mar%3Fa"));  
        Objects<Jugadores> objetos = odb.getObjects (query2); 
        // Obtiene solo el primer objeto encontrado J        
        Jugadores jug = objetos.getFirst();        
        jug.setDeporte ("vóley-playa"); 
        // Cambia el deporte        
        odb.store (jug); // Actualiza el objeto        
        odb.commit(); // Valida los cambios */  
  
        //////CONSULTA 2 CON criterio///////  
  
        ICriterion criterio2 = new And().add(Where.equal("ciudad", "Madrid")).  
                add(Where.ge("edad",15));  
        query = new CriteriaQuery(Jugadores.class, criterio2);  
        Objects<Jugadores> objects2 = odb.getObjects(query);  
        mostrarDatos(objects2, "Jugadores que son de Madrid y tienen 15 a�os");  
  
        //////CONSULTA 3 CON jugadores que hay en un pais///////  
  
        String pais = "Mexico";  
  
        ICriterion criterio3 = new And().add(Where.equal("pais.nombrePais", pais));  
        query = new CriteriaQuery(Jugadores.class, criterio3);  
        Objects<Jugadores> jugadores = odb.getObjects(query);  
  
        mostrarDatos(jugadores, "Jugadores que son de " + pais);  
  
        ///////BORRAR UN PAIS///////  
  
       query = new CriteriaQuery(E01_Paises.class, Where.equal("nombrePais", "Espana"));  
       E01_Paises paisborrar = (E01_Paises) odb.getObjects(query).getFirst();  
       odb.delete(paisborrar);
        odb.close();  
    }  
  
    public static void mostrarDatos(Objects<Jugadores> objects, String mensaje) {  
        System.out.println(mensaje);  
        int i = 1;  
        while(objects.hasNext()){  
            Jugadores jug = objects.next();  
  
            System.out.println((i++) + "\t: " + jug.getNombre() + "*" +  
                    jug.getDeporte() + "*" + jug.getCiudad() + "*" + jug.getEdad()  
                    + "*" + jug.getPais().getNombrePais());  
        }  
        System.out.println("------------");  
    }  
}
```
