```abap
REPORT ztablas_12_ff.

TYPES: BEGIN OF ty_frecuencia,
         valor      TYPE i,
         frecuencia TYPE i,
       END OF ty_frecuencia.

DATA: lt_numeros    TYPE STANDARD TABLE OF i,
      lt_frecuencia TYPE STANDARD TABLE OF ty_frecuencia,
      lv_numero     TYPE i,
      lv_frecuencia TYPE ty_frecuencia.

APPEND 10 TO lt_numeros.
APPEND 20 TO lt_numeros.
APPEND 20 TO lt_numeros.
APPEND 30 TO lt_numeros.
APPEND 30 TO lt_numeros.
APPEND 30 TO lt_numeros.
APPEND 40 TO lt_numeros.
APPEND 10 TO lt_numeros.

LOOP AT lt_numeros INTO lv_numero.
  lv_frecuencia-valor = lv_numero.
  lv_frecuencia-frecuencia = 1.
  COLLECT lv_frecuencia INTO lt_frecuencia.
ENDLOOP.

SORT lt_frecuencia BY valor.
DELETE ADJACENT DUPLICATES FROM lt_frecuencia COMPARING valor.

LOOP AT lt_frecuencia INTO lv_frecuencia.
  WRITE: / 'Número:', lv_frecuencia-valor, ' Frecuencia:', lv_frecuencia-frecuencia.
ENDLOOP.

```