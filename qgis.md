## Cargar shapefile

Datos de prueba de Natural earth: https://www.naturalearthdata.com/downloads/10m-cultural-vectors/

Interface gráfica: carpeta PostGIS > postGIS shapefile.

View connection details .. postgres, 415263, database: laque sea a conectar (T6_shapefile) >Add File > Loalizar archivo formato shapefile (.shp)

Importante: 
Indicar su sistema de referencia de coordenadas mediante su código: SRID 4326 en nuestro caso. En OPTIONS, indicar más opciones. > Import

Comprobarlo: ir a T6_shapefile y en la tabla countries pulsar sobre el ojo

ACCESO DESDE QGIS- Varias opciones:
- Conectar a la BBDD.: Capa > Añadir Capa > Añadir Capas de PostGIS
- Icono superior izquierdo: Abrir administrador de fuentes de datos
- Ver > Barra de Herramientas > Administrar Capas ... Dentro de la barra de herramientas > Icono Elefante (Administrar capas PostGIS) > PostgreSQL > Nueva conexión:
Servicio: nada
Anfitrión: IP o localhost
Pestaña básica: usuario y pass de la bbdd

Mostrar Panel Capas === > Ver > Panel Capas

SEGUIR MINUTO 7 Tema 8 Acceso desde QGIS
