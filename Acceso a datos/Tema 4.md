obj dir, obj persona
tabla personas
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