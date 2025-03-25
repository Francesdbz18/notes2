```ABAP
*&---------------------------------------------------------------------*  
*& Report ZEJERCICIOSCREEN_FF  
*&---------------------------------------------------------------------*  
*&  
*&---------------------------------------------------------------------*  
REPORT ZEJERCICIOSCREEN_FF.  
  
TYPES: BEGIN OF producto,  
         id     TYPE c LENGTH 5,  
         name   TYPE c LENGTH 15,  
         uprice TYPE p DECIMALS 2,  
         cantidad type i,  
       END OF producto,  
       BEGIN OF pedido,  
         id         TYPE c LENGTH 10,  
         date       TYPE d,  
         time       TYPE t,  
         producto1  TYPE producto,  
         producto2  TYPE producto,  
         producto3  TYPE producto,  
         producto4  TYPE producto,  
         producto5  TYPE producto,  
         totalprice TYPE p DECIMALS 2,  
       END OF pedido.  
  
PARAMETERS: p_id TYPE string,  
            p_name TYPE string,  
            p_uprice TYPE p DECIMALS 2,  
            p_cant type i.  
PARAMETERS: p_id2 TYPE string,  
            p_name2 TYPE string,  
            p_upric2 TYPE p DECIMALS 2,  
            p_cant2 type i.  
PARAMETERS: p_id3 TYPE string,  
            p_name3 TYPE string,  
            p_upric3 TYPE p DECIMALS 2,  
            p_cant3 type i.  
PARAMETERS: p_id4 TYPE string,  
            p_name4 TYPE string,  
            p_upric4 TYPE p DECIMALS 2,  
            p_cant4 type i.  
PARAMETERS: p_id5 TYPE string,  
            p_name5 TYPE string,  
            p_upric5 TYPE p DECIMALS 2,  
            p_cant5 type i.  
  
DATA:  
  product1 TYPE producto,  
  product2 TYPE producto,  
  product3 TYPE producto,  
  product4 TYPE producto,  
  product5 TYPE producto.  
  
product1-id = p_id.  
product1-name = p_name.  
product1-uprice = p_uprice.  
product1-cantidad = p_cant.  
product2-id = p_id2.  
product2-name = p_name2.  
product2-uprice = p_upric2.  
product2-cantidad = p_cant2.  
product3-id = p_id3.  
product3-name = p_name3.  
product3-uprice = p_upric3.  
product3-cantidad = p_cant3.  
product4-id = p_id4.  
product4-name = p_name4.  
product4-uprice = p_upric4.  
product4-cantidad = p_cant4.  
product5-id = p_id5.  
product5-name = p_name5.  
product5-uprice = p_upric5.  
product5-cantidad = p_cant5.  
  
DATA: pedido1 TYPE pedido.  
  
pedido1-id = 'aaaaaaaaaaaaaaa'.  
pedido1-date = sy-datum.  
pedido1-time = cl_demo_date_time=>get_user_time( ).  
pedido1-producto1 = product1.  
pedido1-producto2 = product2.  
pedido1-producto3 = product3.  
pedido1-producto4 = product4.  
pedido1-producto5 = product5.  
pedido1-totalprice = ( pedido1-producto1-uprice * pedido1-producto1-cantidad ) + ( pedido1-producto2-uprice * pedido1-producto2-cantidad ) + ( pedido1-producto3-uprice * pedido1-producto3-cantidad ) + ( pedido1-producto4-uprice *  
pedido1-producto4-cantidad ) + ( pedido1-producto5-uprice * pedido1-producto5-cantidad ).  
  
write: 'PEDIDO 1'.  
NEW-LINE.  
  
WRITE: 'ID: ', pedido1-id.  
NEW-LINE.  
WRITE: 'Fecha: ',pedido1-date.  
NEW-LINE.  
WRITE: 'Hora: ', pedido1-time.  
NEW-LINE.  
write: 'PRODUCTO 1'.  
NEW-LINE.  
WRITE: pedido1-producto1-id.  
NEW-LINE.  
WRITE: pedido1-producto1-name.  
NEW-LINE.  
WRITE: pedido1-producto1-uprice.  
NEW-LINE.  
WRITE: pedido1-producto1-cantidad.  
NEW-LINE.  
write: 'PRODUCTO 2'.  
NEW-LINE.  
WRITE: pedido1-producto2-id.  
NEW-LINE.  
WRITE: pedido1-producto2-name.  
NEW-LINE.  
WRITE: pedido1-producto2-uprice.  
NEW-LINE.  
WRITE: pedido1-producto2-cantidad.  
NEW-LINE.  
write: 'PRODUCTO 3'.  
NEW-LINE.  
WRITE: pedido1-producto3-id.  
NEW-LINE.  
WRITE: pedido1-producto3-name.  
NEW-LINE.  
WRITE: pedido1-producto3-uprice.  
NEW-LINE.  
WRITE: pedido1-producto3-cantidad.  
NEW-LINE.  
write: 'PRODUCTO 4'.  
NEW-LINE.  
WRITE: pedido1-producto4-id.  
NEW-LINE.  
WRITE: pedido1-producto4-name.  
NEW-LINE.  
WRITE: pedido1-producto4-uprice.  
NEW-LINE.  
WRITE: pedido1-producto4-cantidad.  
NEW-LINE.  
write: 'PRODUCTO 5'.  
NEW-LINE.  
WRITE: pedido1-producto5-id.  
NEW-LINE.  
WRITE: pedido1-producto5-name.  
NEW-LINE.  
WRITE: pedido1-producto5-uprice.  
NEW-LINE.  
WRITE: pedido1-producto5-cantidad.  
NEW-LINE.  
WRITE: 'Precio total: ', pedido1-totalprice.
```
