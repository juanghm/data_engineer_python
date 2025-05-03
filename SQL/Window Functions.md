# Window Functions

Funcionan similar a una sub-consulta en el select usando la palabra OVER().

- Se ejecutan después de ejecutar la consulta principal (antes de ORDER BY).
- Utiliza la información traída por la consulta NO los datos en la db.
- Funciona en la mayoría de motores de bd.
```sql
SELECT id,
  goals,
 (SELECT AVG(goals) FROM matches) AS overall_avg
FROM matches;

-- Es lo mismo que:

SELECT id,
  goals,
  AVG(goals) OVER() AS overall_avg
FROM matches;
```

El OVER() sin ningún campo dentro de los paréntesis es equivalente a toda la consulta, es decir el promedio de todos los datos.

### ROW_NUMBER()
Se utiliza para agregar una columna con un numero consecutivo correspondiente a cada fila. Siempre asigna valores únicos a cada fila sin importar los valores de los campos.
```sql
SELECT field_1, 
  field_2, 
  ROW_NUMBER() OVER() AS row_no 
FROM table_name
```

### RANK()
Se puede usar para hacer un ranking. Asigna el mismo numero a las filas que tengan los mismos valores, si asigna el mismo numero a varias filas se salta el siguiente numero de ranking:
```sql
SELECT id,
  goals,
  RANK() OVER(ORDER BY goals) AS goals_rank -- Por defecto clasifica de menor->mayor.
FROM matches; 
```

### DENSE_RANK()
Se puede usar para hacer un ranking. Asigna el mismo numero a las filas que tengan los mismos valores, si asigna el mismo numero a varias filas NO se salta el siguiente numero de ranking:
```sql
SELECT id,
  goals,
  DENSE_RANK() OVER(ORDER BY goals) AS goals_rank -- Por defecto clasifica de menor->mayor.
FROM matches; 
```

### ORDER BY
Al agregar la cláusula ORDER BY la función ventana ordena antes de aplicar la función, si se ordena en orden DESC por fecha por ejemplo, el ROW_NUMBER() iniciara en la fecha mas reciente e ira avanzando.

### LAG(column, n)
Selecciona el n-avo valor anterior de la columna especificada, se utiliza para comparar un valor con el n-avo anterior.
```sql
SELECT year, champion,
  LAG(champion, 1) OVER(ORDER BY year ASC) AS last_champion
FROM matches;
```

### LEAD(column, n)
Selecciona el n-avo valor siguiente de la columna especificada, se utiliza para comparar un valor con el n-avo siguiente.
```sql
SELECT year, champion,
  LEAD(champion, 1) OVER(ORDER BY year ASC) AS next_champion
FROM matches;
```

### FIRST_VALUE(column)
Devuelve el primer valor de la tabla o partición.

### LAST_VALUE(column)
Devuelve el ultimo valor de la tabla o partición. Por defecto el ultimo valor es la fila actual, a menos que se indique un rango con UNBOUNDED FOLLOWING.


### OVER and PARTITION BY
Se realiza el calculo sobre la partición “GROUP BY” del campo, así:
```sql
SELECT AVG(home) OVER(PARTITION BY season)
```

Promedio de goles para cada season.

Como particiona los datos las funciones de ventana se aplican sobre cada partición, es decir, ROW_NUMBER se aplicara para cada partición y se resetea para cada partición siguiente.

### Sliding Windows (Frame)
Realiza cálculos relativos a cada fila.
```sql
ROWS BETWEEN <start> AND <finish>
```
Los valores de start y finish pueden ser:

- UNBOUNDED PRECEDING – Todas las filas anteriores a la fila actual.
- n PRECEDING – n filas anteriores a la fila actual.
- CURRENT ROW – solo la fila actual.
- n FOLLOWING – n filas después de a la fila actual.
- UNBOUNDED FOLLOWING – Todas las filas siguientes a la fila actual.
```sql
SELECT date,
  home_goal,
  away_goal,
  SUM(home_goal)
    OVER(ORDER BY date
    ROWS BETWEEN 1 PRECEDING
    AND CURRENT ROW) AS last2
FROM matches
```
Esta sentencia presenta el resultado de sumar el acumulado de home_goal cada dos filas.

## Paging

### NTILE(n)
Divide los datos de la consulta en n paginas.
```sql
SELECT date,
  home_team,
  away_team,
  NTILE(10) OVER() as Page
FROM matches;
```
Divide los datos en 10 paginas.
