### Sequence 
```psql
CREATE SEQUENCE IF NOT EXISTS sequence_name
  START WITH (SELECT MAX(column_name) FROM table_name)
  INCREMENT BY 1;
SELECT column_name, column_default
FROM information_schema.columns
WHERE table_name = 'table_name'
AND column_default LIKE 'nextval%';
```

### restaurar .backup

En primer lugar debe existir una base de datos con el mismo nombre de la que se va a restaurar y comprobar que tenga permisos el usuario -U con el que se está haciendo la conexión.

```psql
psql --single-transaction -U postgres -p 5433 basalan < c:\basalan.backup
```

Hasta hace unos días me funcionaba ahora lo he tenido con hacer con pg_restore

```psql
pg_restore -U postgres -p 5433 -d basalan c:\basalan.backup
```

### Operador :: (signo de dos puntos doble)
https://learn.microsoft.com/es-es/azure/databricks/sql/language-manual/functions/coloncolonsign

Convierte el valor expr al tipo de datos de destino type.

```sql
expr :: type
```

### importar archivo .sql externo a una base de datos mysql en local

- Abrir consola de windows.

- Posicionarnos en carpeta: C:\xampp\mysql\bin

```sh
cd C:\xampp\mysql\bin
mysql -h localhost -u root dbe5fezlxyvlhg < C:\Users\evara\Downloads\dbe5fezlxyvlhg(3).sql

```

Para que no de errores de importación por el tamaño del paquete modificar el archivo my.ini (desde xammpp) y buscar:

```sql
[mysqld]
max_allowed_packet=100M
```

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

##Conectada a la BBDD: psql -U postgres -d PRUEBAS_ALPI

\COPY nuevas_coordenadas (id_general, texto_pregunta, posicion_h, posicion_v, x, y, actualizado) FROM 'C:\xampp\htdocs\ALPI\data\alpi_actualizacion\nuevas_coordenadas.csv' DELIMITER ';' CSV ENCODING 'UTF8';

```

### Crear estructura desde fichero  sql:

```sql
psql -U postgres PRUEBAS_ALPI < nuevas_coordenadas.sql
```

### osm to pgrouting desde consola
```sql
osm2pgrouting --file lugones --dbname daniel --username postgres --password postgres --conf mapconfig.xml --clean

```

### Copiar sql a bbdd existente
psql -U postgres -f dump_respuestas_15_12.sql ALPI
