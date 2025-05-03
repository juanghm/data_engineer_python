# ROLLUP & CUBE

### ROLLUP
Es una sub-clausula del GROUP BY, que genera una columna extra para agregaciones a nivel de grupo.


producto    |  region    |  total_ventas
------------|------------|---------------
Camiseta    |  Norte     |  100
Camiseta    |  Sur       |  150
Pantalón    |  Norte     |  200
Pantalón    |  Sur       |  300

```sql
SELECT producto, region, SUM(total_ventas) AS total
FROM ventas
GROUP BY ROLLUP (producto, region);
```

producto    |  region    |  total | desc
------------|------------|--------|------
Camiseta    |  Norte     |  100   | 
Camiseta    |  Sur       |  150   | 
Camiseta    |  NULL      |  250   | -- Subtotal por producto "Camiseta"
Pantalón    |  Norte     |  200   | 
Pantalón    |  Sur       |  300   | 
Pantalón    |  NULL      |  500   | -- Subtotal por producto "Pantalón"
NULL        |  NULL      |  750   | -- Total general

- Agrupa primero por producto y region.
- Luego genera subtotales por cada producto (cuando region es NULL).
- Finalmente, genera un total general para todas las filas (cuando ambas columnas son NULL).


### CUBE
Funciona de manera similar a ROLLUP pero no es jerárquico, es decir, genera todos los totales por agrupación.

producto    |  region    |  total_ventas
------------|------------|---------------
Camiseta    |  Norte     |  100
Camiseta    |  Sur       |  150
Pantalón    |  Norte     |  200
Pantalón    |  Sur       |  300

```sql
SELECT producto, region, SUM(total_ventas) AS total
FROM ventas
GROUP BY CUBE (producto, region);
```

producto    |  region    |  total | desc
------------|------------|--------|--
Camiseta    |  Norte     |  100.  |
Camiseta    |  Sur       |  150.  |
Camiseta    |  NULL      |  250   |-- Subtotal por producto "Camiseta"
Pantalón    |  Norte     |  200.  |
Pantalón    |  Sur       |  300.  |
Pantalón    |  NULL      |  500   |-- Subtotal por producto "Pantalón"
NULL        |  Norte     |  300   |-- Subtotal por región "Norte"
NULL        |  Sur       |  450   |-- Subtotal por región "Sur"
NULL        |  NULL      |  750   |-- Total general

- Genera un subtotal para cada combinación de columnas:
- Subtotales por producto.
- Subtotales por región.
- Total general para todas las filas.
- Incluye combinaciones de columnas con NULL cuando no se aplica una agrupación específica.