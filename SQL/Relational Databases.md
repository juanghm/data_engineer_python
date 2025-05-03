# Relational Databases

## Ver Objetos de un Schema
Para listar las tablas de un schema se puede utilizar al consulta:

```sql
SELECT *
FROM information_schema.tables
WHERE table_schema = 'schema_name';
```

Para listar las vistas de un schema se puede utilizar al consulta:
```sql
SELECT *
FROM information_schema.views
WHERE table_schema = 'schema_name';
```

Para listar las columnas de una o varias tablas se puede utilizar al consulta:
```sql
SELECT *
FROM information_schema.columns
WHERE table_schema = 'schema_name'
    AND table_name = 'table_name;
```

Para listar las llaves foráneas se puede utilizar al consulta:
```sql
SELECT constraint_name, table_name, constraint_type
FROM information_schema.table_constraints
WHERE constraint_type = 'FOREIGN KEY';
```

Cambiar Tipo de Datos de una Columna
Al cambiar el tipo de dato de una columna es posible que se necesario una transformación de los datos, así:
```sql
ALTER TABLE table_name
ALTER COLUMN column_name
TYPE new_type
USING CAST(column_name AS new_type);

ALTER TABLE table_name
ALTER COLUMN column_name
TYPE new_type
USING SUBSTRING(column_name FROM 1 TO 10);
```

## Vistas

- Se puede hacer insert en una vista SOLO si esta proviene de una consulta a UNA sola tabla.
- Es una MALA práctica hacer inserts sobre una vista.
- Si se quiere modificar una vista, modificando su consulta, esta nueva consulta debe traer los mismos campos, en el mismo orden y de los mismos tipos de datos que la consulta anterior. Se pueden agregar nuevas columnas al FINAL.

## Tablas Temporales
- Se pueden crear tablas temporales que solo estarán disponibles durante la sesión actual.
```sql
CREATE TEMP TABLE temp_table_name (
    column_name1 data_type,
    column_name2 data_type,
    ...
);
```

```sql
CREATE TEMP TABLE temp_table_name AS
    SELECT column_name1, column_name2, ...
```

## Analizar Tablas
Para analizar una tabla y actualizar las estadísticas de la misma:
```sql
ANALYZE table_name;
```

Explicar la ejecucion de consultas.
```sql
EXPLAIN
```

## Extensiones
Para consultar que extensiones están disponibles para instalarse:
```sql
SELECT name FROM pg_available_extensions;
```

Para consultar que extensiones se tienen instaladas se puede utilizar:
```sql
SELECT extname FROM pg_extension;
```

## Good Practices

- Alinear las palabras claves SELECT, FROM, WHERE, GROUP BY
- Indentar la consulta.
- Comentar las consultas. Al inicio de la consulta un comentario entre /* y */, también se puede comentar una linea de la consulta usando --
- Se recomienda reducir al máximo las sub-consultas, solo usarlas en caso de ser necesaria.
- Usar CTE, se ejecuta una sola vez y se guarda en memoria.