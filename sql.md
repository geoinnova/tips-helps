### importar archivo sql a una bbdd desde consola
```sql
mysql -h localhost -u root dbe5fezlxyvlhg < dbe5fezlxyvlhg_table_wp_geo_options.sql
```




psql -d tema7 -U postgres -f  mdt_Jaen.sql

\COPY nuevas_coordenadas (codbarrio, nombre, distrito, area) FROM C:\xampp\htdocs\ALPI\data\alpi_actualizacion\nuevas_coordenadas.csv' DELIMITER ';' CSV HEADER ENCODING 'UTF8',



Crear estructura desde fichero  sql:
psql -U postgres PRUEBAS_ALPI < nuevas_coordenadas.sql


Conectada a la BBDD: psql -U postgres -d PRUEBAS_ALPI
\COPY nuevas_coordenadas (id_general, posicion_h, posicion_v, x, y) FROM 'nuevas_coordenadas.csv' DELIMITER ';' CSV ENCODING 'UTF8'; 

\COPY nuevas_coordenadas (id_general, posicion_h, posicion_v, x, y) FROM 'C:\xampp\htdocs\ALPI\_DATOS Y EXPLICACIONES\ACTUALIZACION ENTREGADA\datos_nuevas_coordenadas.csv' DELIMITER ';' CSV ENCODING 'UTF8';


\COPY nuevas_coordenadas (id_general, texto_pregunta, posicion_h, posicion_v, x, y, actualizado) FROM 'C:\xampp\htdocs\ALPI\data\alpi_actualizacion\nuevas_coordenadas.csv' DELIMITER ';' CSV ENCODING 'UTF8';
