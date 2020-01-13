```sql
CREATE DATABASE gisdb;
\connect gisdb;
-- Enable PostGIS (includes raster)
CREATE EXTENSION postgis;
-- Enable Topology
CREATE EXTENSION postgis_topology;
-- Enable PostGIS Advanced 3D
-- and other geoprocessing algorithms
CREATE EXTENSION postgis_sfcgal;
-- fuzzy matching needed for Tiger
CREATE EXTENSION fuzzystrmatch;
-- rule based standardizer
CREATE EXTENSION address_standardizer;
-- example rule data set
CREATE EXTENSION address_standardizer_data_us;
-- Enable US Tiger Geocoder
CREATE EXTENSION postgis_tiger_geocoder;
-- routing functionality
CREATE EXTENSION pgrouting;
-- spatial foreign data wrappers
CREATE EXTENSION ogr_fdw;

-- LIDAR support
CREATE EXTENSION pointcloud;
-- LIDAR Point cloud patches to geometry type cases
CREATE EXTENSION pointcloud_postgis;
```


Crear una tabla

```sql

-- ejemplo
CREATE TABLE spatial_table (id integer, name varchar, geom geometry);


CREATE TABLE canchitas (id integer, name varchar, geom geometry);

```

Guardar datos de prueba

```sql

INSERT INTO spatial_table VALUES
  (1, 'point', 'POINT(30 10)'),
  (2, 'line', 'LINESTRING(30 10, 10 30, 40 40)'),
  (3, 'polygon-simple',
      'POLYGON((30 10, 40 40, 20 40, 10 20, 30 10))'),
  (4, 'polygon-hole', 
      'POLYGON((35 10, 45 45, 15 40, 10 20, 35 10),(20 30, 35 35, 30 20, 20 30))');


INSERT INTO spatial_table VALUES
  (5, 'multipoint', 'MULTIPOINT(10 40, 40 30, 20 20, 30 10)'),
  (6, 'multilinestring', 'MULTILINESTRING((10 10, 20 20, 10 40), (40 40, 30 30, 40 20, 30 10))'),
  (7, 'multipolygon', 
      'MULTIPOLYGON(((40 40, 20 45, 45 30, 40 40)), ((20 35, 10 30, 10 10, 30 5, 45 20, 20 35), (30 20, 20 15, 20 25, 30 20)))'),
  (8, 'geometrycollection', 'GEOMETRYCOLLECTION(POINT(4 6), LINESTRING(4 6,7 10))');


INSERT INTO spatial_table VALUES
  (9, 'point', ST_GeomFromText('POINT(-123.12 49.28)', 4326)),
  (10, 'point', ST_GeomFromText('POINT(491272.2 5458589.7)', 26910));


-- canchas de la UNAP

INSERT INTO spatial_table VALUES
  (11, 'point', ST_GeomFromText('POINT(-15.82544 -70.01511)', 4326));

```

<img src="2020-01-13 07_25_45-Window.png">

[fuente](http://strimas.com/spatial/r-postgis-2/)