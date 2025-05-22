SAP IDocs

Ejercicio: Programa que genere y envíe un IDOC de tipo MATMAS07.
ZENVIA_MAT_IDOC_FF
En la pantalla de selección se debe introducir el material y el sistema lógico.

hint: para crear un idoc no es necesario rellenar todos los segmentos

material: fgpc01
e1maram 
e1maktm
```
*&---------------------------------------------------------------------*  
*& Report ZENVIA_MAT_IDOC_FF  
*&---------------------------------------------------------------------*  
*&  
*&---------------------------------------------------------------------*  
REPORT zenvia_mat_idoc_ff.

PARAMETERS:  
  p_matnr  TYPE matnr OBLIGATORY,  
  p_logsys TYPE logsys OBLIGATORY.  
  
DATA: ls_edidc       TYPE edidc,  
      lt_edidd       TYPE STANDARD TABLE OF edidd,  
      ls_edidd       TYPE edidd,  
      lt_edidc       TYPE STANDARD TABLE OF edidc.  
  
CLEAR ls_edidc.  
ls_edidc-mestyp  = 'MATMAS'.  
ls_edidc-idoctp  = 'MATMAS07'.  
ls_edidc-rcvprn  = p_logsys.  
ls_edidc-rcvprt  = 'LS'.  
ls_edidc-sndprn  = sy-sysid.  
ls_edidc-sndprt  = 'LS'.  
ls_edidc-serial  = sy-datum && sy-uzeit.  
APPEND ls_edidc TO lt_edidc.  
  
CLEAR ls_edidd.  
ls_edidd-segnam  = 'E1MARAM'.  
ls_edidd-sdata = p_matnr.  
APPEND ls_edidd TO lt_edidd.  
  
CLEAR ls_edidd.  
ls_edidd-segnam  = 'E1MAKTM'.  
ls_edidd-sdata  = p_matnr.  
APPEND ls_edidd TO lt_edidd.  
  
CALL FUNCTION 'MASTER_IDOC_DISTRIBUTE'  
  EXPORTING  
    master_idoc_control        = ls_edidc  
  TABLES  
    communication_idoc_control = lt_edidc  
    master_idoc_data           = lt_edidd  
  EXCEPTIONS  
    OTHERS                     = 1.  
  
COMMIT WORK.
```