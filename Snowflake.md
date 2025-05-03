# Snowflake
Base de datos columnar, multinube, separa el procesamiento del almacenaje.

## SHOW DATABASES
Muestra un listado de las bases de datos.

## SHOW TABLES IN { DATABASE [ <db_name> ] }
Muestra las tablas en la base de datos de nombre <db_name>.

## SHOW TABLES [ LIKE ‘<pattern>’ ] IN { DATABASE [ <db_name> ] }
Muestra las tablas en la base de datos de nombre <db_name> donde el nombre la tabla sea like <pattern>.

## MERGE INTO <target_table> USING <source> ON <join_expr> { matchedClause | notMatchedClause } [ ... ]
Comando que permite hacer insert, update y delete en una tabla (target) a partir de una consulta (source).

## GROUP BY ALL
Cuando se quiere agrupar por todas las columnas que no están agregadas.

## NATURAL JOIN
Funciona similar al inner join pero no se especifican las columnas a igualar y en el resultado elimina las columnas repetidas, ademas si se utiliza alguna columna en común entre las dos tablas como condición en el where no hay que especificar a que tabla pertenece:

```sql
SELECT *
FROM table_name_1 AS t1
  NATURAL JOIN table_name_2 AS t2
```

## LATERAL JOIN
Se usa para unir una tabla con una consulta en el FROM.

## TOP N
Se utiliza para mostrar los N primeros resultados de una consulta.

## Query History
Se puede consultar el historial de ejecución de consultas:

```sql
SELECT query_text, start_time, end_time, execution_time
FROM snowflake.account_usage.query_history
WHERE query_text ILIKE '%table_name%';
```

## PARSE_JSON
Convierte un string json en un objeto json:
```sql
SELECT PARSE_JSON(
' -- enclosed in strings
  {
    "obj_id": 1,
    "obj_name": "name_object",
    "obj_age": 40
  }
' -- enclosed in strings
) AS info_json;
```

## OBJECT_CONSTRUCT
Convierte un arreglo de llave, valor en un objeto json:
```sql
SELECT PARSE_JSON(
    "obj_id": 1,
    "obj_name": "name_object",
    "obj_age": 40
) AS info_json;
```

## Querying JSON Data
```sql
SELECT info_json:obj_id,
  info_json:obj_name,
  info_json:obj_age
FROM info_json_data;
```