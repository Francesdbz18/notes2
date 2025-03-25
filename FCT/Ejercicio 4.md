```ABAP
*&---------------------------------------------------------------------*  
*& Report ZEJERCICIO_4_FF  
*&---------------------------------------------------------------------*  
*&  
*&---------------------------------------------------------------------*  
REPORT ZEJERCICIO_4_FF.  
  
DATA: oref   TYPE REF TO cx_root,  
      text type string.  
  
  TRY.  
    DATA(div2) = 1 / 0.  
    CATCH cx_sy_arithmetic_error INTO oref.  
      text = oref->get_text( ).  
  ENDTRY.  
***EXTRAIDO DE help.sap.com  
  
  write: text.  
  
*using the WRITE TO statement  
*****************************  
  data: gd_date(10).  "field to store output date  
  
* Converts SAP date from 20020901 to 01.09.2002  
  write: sy-datum to gd_date dd/mm/yyyy.  
    write: gd_date.  
  
* Converts SAP date from 20020901 to 01.09.02  
  write: sy-datum to gd_date dd/mm/yy.  
  write: gd_date.  
* Converts SAP date from 20020901 to 09.01.02  
  write: sy-datum to gd_date mm/dd/yy.  
  write: gd_date.  
* Converts SAP date from 20020901 to 020901  
  write: sy-datum to gd_date yymmdd.  
  write: gd_date.  
  
  NEW-LINE.  
  
* Using basic data manipulation techniques  
************************************  
  
* Converts SAP date from 20010901(YYYYMMDD) to 01092001(DDMMYYYY)  
  gd_date(2)    = sy-datum+6(2).  
  gd_date+2(2) = sy-datum+4(2).  
  gd_date+4(4) = sy-datum(4).  
  
*....  
* taking this technique bit further you can produce any output you want  
************************************  
   data: gd_outputdate type string,  
                gd_day(2),   "field to store day 'DD'  
                gd_month(2), "field to store month 'MM'  
                gd_year(4).  "field to store year 'YYYY'  
  
* split date into 3 fields to store 'DD', 'MM' and 'YYYY'  
  gd_day(2)   = sy-datum+6(2).  
  gd_month(2) = sy-datum+4(2).  
  gd_year(4)  = sy-datum(4).  
  
*Now use the CONCATENATE statement or it's newer method to format the date as you want  
*Note you could also at this point create new variables to represent MMM i.e. APR, JAN, FEB etc  
  
*dd/mm/yyyy  
concatenate gd_day gd_month gd_year into gd_outputdate separated by '/'.  
write gd_outputdate.  
*dd.mm.yyyy  
concatenate gd_day gd_month gd_year into gd_outputdate separated by '.'.  
write gd_outputdate.  
*mm--dd--yyyy  
concatenate gd_month gd_day gd_year into gd_outputdate separated by '--'.  
write gd_outputdate.  
*mm-dd-yyyy using new method  
gd_outputdate = |{ gd_month }| && |-| && |{ gd_day }| && |-| && |{ gd_year }|.  
write gd_outputdate.  
  
*mmyyyy using new method  
gd_outputdate = |{ gd_month }| && |{ gd_year }|.  
  
write gd_outputdate.  
  
* Using Function modules  
************************  
  
* Converts date from 20010901 to 01SEP2001  
  gd_date   = sy-datum.  
  CALL FUNCTION 'CONVERSION_EXIT_IDATE_OUTPUT'  
    EXPORTING  
      input         = gd_date  
    IMPORTING  
      OUTPUT        = gd_date.  
  
 write gd_date.  
  
*** EXTRAIDO DE se80.co.uk
```
