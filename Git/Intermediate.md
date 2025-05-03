# Intermediate

## Branches

Ver todas las ramas:
```git branch```

Crear un branch:
```git branch new-branch-name```

Moverse a una rama:
```git switch new-branch-name```

Crear una nueva rama y moverse a ella:
```git switch -c new-branch-name```

Comparar dos ramas:
```git diff branch-1 branch-2```

Re-nombrar una rama:
```git branch -m current_name new_name```

Eliminar una rama (que ya fue merge a master o main):
```git branch -d branch-name-to-delete```

Eliminar una rama que no ha sido merged:
```git branch -D branch-name-to-delete```

Hacer merge de dos ramas:
```git merge other-branch```

## Remotes

Para ver los remotes configurados:
```git remote -v```

Para agregar otro remoto
```git remote add name-remote url-remote```

Fetch los cambios de una rama remota:
```git fetch original main```

Bajar los cambios:
```git merge origin```

Pulling de un remote, equivalente a fetch y merge:
```git pull origin```

Enviar los cambios de la rama main al repositorio remoto origin:
```git push origin main```