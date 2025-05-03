# Basic
## Crear un Repositorio
Para crear un repositorio de cero:
```git init repo-name-here```

Para convertir un directorio existente en un repositorio git
```git init```

## Staging y Committing

1. Se crean y editan los archivos.
2. Se agregan al repositorio.
3. Se guardan los cambios en el repositorio.

Para agregar solo el archivo file-name:
```git add file-name```

Para agregar todos los archivos que no están en el repositorio.
```git add .```

Para guardar los cambios en el repositorio se hace commit:
```git commit -m "Mensaje describiendo el cambio"```

Para ver todos los commit hechos:
```git log```

```git log --since='2025-01-15' --until='2025-02-11'```

Para ver un solo commit:
```git show 1c9212```

Para ver los últimos n commits:
```git log -n 5```

Para ver los commits de un archivo especifico:
```git log archivo-a-revisar```

## Comparando Archivos
```git diff```

Por defecto compara la version actual y el ultimo commit.
```git diff file-name-to-compare```

Se pueden comparar dos commits por su código, el mas nuevo debe ir de segundo:
```git diff 34f23cb 65dbf2```

## Restaurando Archivos
Se puede restaurar a la version anterior, se restaura todo el commit:
```git revert```

Para restaurar un solo archivo se utiliza el checkout:
```git checkout HEAD~1 -- file-name-to-checkout```

Para excluir un archivo del staging area:
```git restore --staged file-to-exclude```
```git restore --stageg```