# Dates

### AGE(date_1, date_2)
Calcula la diferencia entre dos fechas retornando el intervalo.
```sql
SELECT AGE(date_field)
```

### EXTRACT(field FROM source)
Se puede extraer una parte de la fecha, mes, año, etc.
```sql
SELECT EXTRACT(quarter FROM NOW()) AS quarter;
```

### DATE_PART(‘field’, source)
Similar a la función extract, obtiene la parte de la fecha que se indica.
```sql
SELECT DATE_PART('quarter', NOW()) AS quarter;
```

### DATE_TRUNC(‘field’, source)
Trunca la fecha por el campo que se le especifique.
```sql
SELECT DATE_TRUNC('month', NOW()) AS quarter; -- obtiene la año-mes-01 00:00:00
```

### TO_DATE(texto_fecha, formato)
Permite convertir un string en tipo DATE.
```sql
SELECT TO_DATE('12-04-2025', 'DD-MM-YYYY') AS fecha_convertida
```

### MAKE_DATE
Permite crear una fecha a partir de 3 valores, año, mes y dia:
```sql
SELECT MAKE_DATE(EXTRACT(YEAR FROM CURRENT_DATE)::INT, 4, 1)-- 2025-04-01
```