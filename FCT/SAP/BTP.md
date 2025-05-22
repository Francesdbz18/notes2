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
  
DATA: lv_idoc_number TYPE edi_docnum,  
      ls_edidc       TYPE edidc,  
      lt_edidd       TYPE STANDARD TABLE OF edidd,  
      ls_edidd       TYPE edidd,  
      lt_edidc       TYPE STANDARD TABLE OF edidc.  
  
DATA: ls_mara TYPE mara,  
      lt_makt TYPE TABLE OF makt,  
      ls_makt TYPE makt.  
  
CLEAR ls_edidc.  
ls_edidc-mestyp  = 'MATMAS'.  
ls_edidc-doctyp = 'MATMAS07'.  
ls_edidc-rcvprn  = p_logsys.  
ls_edidc-rcvprt  = 'LS'.  
ls_edidc-sndprn  = sy-sysid.  
ls_edidc-sndprt  = 'LS'.  
  
APPEND ls_edidc TO lt_edidc.  
  
DATA: lv_segnum        TYPE i VALUE 1,  
      lv_matmas_segnum TYPE i,  
      lv_maram_segnum  TYPE i.  
  
CLEAR ls_edidd.  
ls_edidd-segnam = 'E1MATMAS'.  
ls_edidd-segnum = lv_segnum.  
APPEND ls_edidd TO lt_edidd.  
  
lv_matmas_segnum = lv_segnum.  
ADD 1 TO lv_segnum.  
  
CLEAR ls_edidd.  
ls_edidd-segnam  = 'E1MARAM'.  
ls_edidd-segnum  = lv_segnum.  
ls_edidd-psgnum = lv_matmas_segnum.  
  
ls_edidd-sdata+0(018) = ls_mara-matnr.  
ls_edidd-sdata+18(004) = ls_mara-mtart.  
ls_edidd-sdata+22(001) = ls_mara-mbrsh.  
ls_edidd-sdata+23(009) = ls_mara-matkl.  
  
APPEND ls_edidd TO lt_edidd.  
  
lv_maram_segnum = lv_segnum.  
ADD 1 TO lv_segnum.  
  
  
SELECT * INTO TABLE lt_makt  
  FROM makt  
  WHERE matnr = ls_mara-matnr.  
LOOP AT lt_makt INTO ls_makt.  
  CLEAR ls_edidd.  
  ls_edidd-segnam  = 'E1MAKTM'.  
  ls_edidd-segnum  = lv_segnum.  
  ls_edidd-psgnum = lv_maram_segnum.  
  
  ls_edidd-sdata+0(018)  = ls_makt-matnr.  
  ls_edidd-sdata+18(002) = ls_makt-spras.  
  ls_edidd-sdata+20(040) = ls_makt-maktx.  
  
  APPEND ls_edidd TO lt_edidd.  
  ADD 1 TO lv_segnum.  
ENDLOOP.  
  
  
  
CALL FUNCTION 'MASTER_IDOC_DISTRIBUTE'  
  EXPORTING  
    master_idoc_control        = ls_edidc  
  TABLES  
    communication_idoc_control = lt_edidc  
    master_idoc_data           = lt_edidd  
  EXCEPTIONS  
    OTHERS                     = 1.
```