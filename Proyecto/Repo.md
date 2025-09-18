[Francesdbz18/f1-webapp](https://github.com/Francesdbz18/f1-webapp)

Este es el repositorio con el código de la aplicación. Incluye instrucciones para poder ejecutarla en local.

Por ahora, permite: 
-  Seleccionar un año y una sesión específica (carrera, clasificación, etc.)
    
- Ver la lista de pilotos participantes
    
- Acceder al detalle de cada piloto, con su información y estadísticas de vueltas (gráfico incluido)
    
- Ver imágenes y colores del equipo, además de otros datos relevantes

Al ser una aplicación web con React y TypeScript, el frontend se encuentra organizado en componentes y con archivos TypeScript JSX, mientras que el backend usa Python con FastAPI para consumir los datos de OpenF1 y pasarlos al frontend.