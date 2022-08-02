### importar archivo sql a una bbdd desde consola
```sql
mysql -h localhost -u root dbe5fezlxyvlhg < dbe5fezlxyvlhg_table_wp_geo_options.sql
```

### psql importar a la bbdd tema7 la tabla Jaen
```sql
psql -d tema7 -U postgres -f  Jaen.sql
```

### importar datos a tabla nuevas_coordenadas desde fichero csv
```sql
\COPY nuevas_coordenadas (codbarrio, nombre, distrito, area) FROM C:\xampp\htdocs\ALPI\data\alpi_actualizacion\nuevas_coordenadas.csv' DELIMITER ';' CSV HEADER ENCODING 'UTF8',

## onectada a la BBDD: psql -U postgres -d PRUEBAS_ALPI

\COPY nuevas_coordenadas (id_general, texto_pregunta, posicion_h, posicion_v, x, y, actualizado) FROM 'C:\xampp\htdocs\ALPI\data\alpi_actualizacion\nuevas_coordenadas.csv' DELIMITER ';' CSV ENCODING 'UTF8';

```

### Crear estructura desde fichero  sql:
psql -U postgres PRUEBAS_ALPI < nuevas_coordenadas.sql


