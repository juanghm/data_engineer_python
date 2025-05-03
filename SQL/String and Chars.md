# String and Chars

### Contatenation ||
- Se puede utilizar el comando doble || para concatenar varias cadenas.
- También se puede usar el comando CONCAT(string_1, string_2, ….)
  
### REPLACE(column_name, string_original, string_new)
Reemplaza el string_original por el string_new en la columna column name.

### INITCAP()
Convierte el texto en title case.

### POSITION(char IN column)
Retorna un entero que indica la posición del caracter en la cadena.

### STRPOS(column, char)
Retorna un entero que indica la posición del caracter en la cadena.

### LEFT(column, n)
retorna los n primeros caracteres de la cadena en la columna.

### RIGHT(column, n)
retorna los n últimos caracteres de la cadena en la columna.

### SUBSTRING(column, init_index, n)
Extrae la cadena de la columna que inicia en el init_index y tiene de longitud n.

### SUBSTRING(column FROM init_index FOR POSITION(char IN column))
Extrae la cadena de la columna que inicia en init_index y termina en la posición que esta el char

### TRIM(leading | trailing | both) [chars] FROM string
Todos los parámetros son opcionales.

### LPAD(string, n, char)
Agrega chars (si no se pasa se agregan espacios) a la izquierda del string hasta completar la longitud n de la cadena.

### Full Text Search
Hace una búsqueda del texto en cualquier posición sin importar el case.
```sql
SELECT *
FROM table
WHERE to_tsvector(title) @@ to_tsquery('cia');
```
Busca la palabra ‘cia’ en el campo title sin importar la posición ni si esta en mayúscula o minúscula.
