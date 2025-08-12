# Merge
## Fast-forward merge
Cuando se hace un merge de una rama a otra, si la rama de destino no tiene commits nuevos desde que se creó la rama de origen, Git puede hacer un "fast-forward" y simplemente mover el puntero de la rama de destino al último commit de la rama de origen. Esto es más eficiente y mantiene el historial lineal.
```bash
  git merge --ff-only <branch>
```
- Es ideal para mantener un historial limpio y lineal.
- Se usa cuando se quiere hacer merge de una rama que ha tenido una vida corta.
- NO se recomienda cuando se quiera preservar el historial de merges.
- NO se recomienda cuando es un feature muy grande o complejo.

## Merge recursivo
Cuando se hace un merge de dos ramas que han tenido commits diferentes desde que se separaron, Git utiliza un algoritmo de merge recursivo. Este algoritmo encuentra el ancestro común más reciente de ambas ramas y crea un nuevo commit de merge que combina los cambios de ambas ramas.
```bash
  git merge <branch>
```
- Es ideal para combinar ramas que han tenido desarrollos paralelos.
- Se usa cuando se quiere preservar el historial de merges.
- Se recomienda para merges de características grandes o complejas.

## Squash merge
Un "squash merge" combina todos los commits de una rama en un solo commit antes de hacer el merge en la rama de destino. Esto es útil para mantener un historial limpio y evitar un gran número de commits intermedios que pueden no ser relevantes para el historial del proyecto.
```bash
  git merge --squash <branch>
```
- Es ideal para combinar ramas de características que tienen muchos commits intermedios.
- Se usa cuando se quiere simplificar el historial de commits.
- NO se recomienda para ramas que tienen un historial de commits importante que se quiere preservar.

## Octopus merge
Un "octopus merge" es un tipo de merge que permite combinar más de dos ramas en un solo commit. Es útil cuando se quiere combinar múltiples ramas de características en una sola rama de destino.
```bash
  git merge -s octopus <branch1> <branch2> <branch3>
```
- Es ideal para combinar múltiples ramas de características en una sola rama de destino.
- Se usa cuando se quiere hacer un merge de varias ramas al mismo tiempo.
- NO se recomienda para merges complejos, ya que puede ser difícil resolver conflictos en múltiples ramas.
- NO se recomienda para merges que involucren ramas con un historial de commits complejo.

# Rebase
El rebase es una alternativa al merge que permite reescribir el historial de commits de una rama. En lugar de crear un nuevo commit de merge, el rebase mueve los commits de la rama de origen a la rama de destino, aplicando los cambios uno por uno. Esto resulta en un historial más limpio y lineal, pero puede ser peligroso si no se usa correctamente, ya que reescribe el historial de commits.
```bash
    git rebase <branch>
```
- Es ideal para mantener un historial limpio y lineal.
- Se usa cuando se quiere aplicar los cambios de una rama a otra sin crear un commit de merge.
- NO se recomienda para ramas que ya han sido compartidas con otros, ya que reescribir el historial puede causar problemas de sincronización.
- Se recomienda para ramas de características que aún no han sido compartidas o que se están desarrollando de manera aislada.
- Se debe tener cuidado al hacer rebase en ramas que tienen un historial de commits complejo, ya que puede ser difícil resolver conflictos.

# Cherry-pick
El cherry-pick es una operación que permite aplicar un commit específico de una rama a otra. Esto es útil cuando se quiere aplicar un cambio específico sin hacer un merge completo de la rama.
```bash
    git cherry-pick <commit>
    # or
    git cherry-pick <commit_1_hash> <commit_2_hash> ...
```
- Es ideal para aplicar cambios específicos de una rama a otra.
- Se usa cuando se quiere aplicar un commit específico sin hacer un merge completo de la rama.
- Se recomienda para aplicar correcciones de errores o cambios específicos que se han hecho en una rama de características.
- NO se recomienda para aplicar múltiples commits, ya que puede ser difícil resolver conflictos si los commits están relacionados entre sí.
- Se debe tener cuidado al hacer cherry-pick en ramas que tienen un historial de commits complejo, ya que puede ser difícil resolver conflictos.

# Bisect
El bisect es una herramienta de Git que permite encontrar el commit que introdujo un error en el código. Utiliza una búsqueda binaria para identificar el commit problemático, lo que hace que sea mucho más eficiente que revisar manualmente cada commit.
```bash
    git bisect start
    git bisect bad <commit> # Marca el commit problemático
    git bisect good <commit> # Marca un commit que se sabe que es bueno
    # Git comenzará a hacer checkout de commits intermedios para que puedas probar si el error está presente o no
    # Una vez que encuentres el commit problemático, usa:
    git bisect reset # Para volver al estado original
```
- Es ideal para encontrar el commit que introdujo un error en el código.
- Se usa cuando se quiere identificar rápidamente el commit que causó un problema.
- Se recomienda para proyectos grandes con muchos commits, ya que hace que la búsqueda sea mucho más eficiente.
- NO se recomienda para proyectos pequeños o con pocos commits, ya que puede ser innecesario.
- Se debe tener cuidado al usar bisect en ramas que tienen un historial de commits complejo, ya que puede ser difícil resolver conflictos si el commit problemático está relacionado con otros commits.

# Filter-repo
El filter-repo es una herramienta avanzada de Git que permite reescribir el historial de commits de un repositorio. Es útil para eliminar archivos grandes, sensibles o innecesarios del historial, así como para cambiar la estructura del repositorio.
```bash
  git filter-repo --path <file_or_directory> --invert-paths
```
- Es ideal para limpiar el historial de commits de un repositorio.
- Se usa cuando se quiere eliminar archivos grandes, sensibles o innecesarios del historial.
- Se recomienda para proyectos que han acumulado archivos innecesarios o sensibles en su historial.
- NO se recomienda para proyectos pequeños o con pocos commits, ya que puede ser innecesario.
- Se debe tener cuidado al usar filter-repo, ya que reescribir el historial puede causar problemas de sincronización si el repositorio ha sido compartido con otros.

# Reflog
El reflog es una herramienta de Git que permite ver el historial de referencias de un repositorio. Muestra un registro de todas las operaciones que han modificado las referencias, como commits, merges, rebases, etc. Es útil para recuperar commits perdidos o para entender cómo ha cambiado el historial del repositorio.
```bash
  git reflog
  git checkout <hash> # Para recuperar un commit perdido
  git checkout -b <branch-name> # Para crear una nueva rama desde un commit perdido
```
- Es ideal para ver el historial de referencias de un repositorio.
- Se usa cuando se quiere entender cómo ha cambiado el historial del repositorio o recuperar commits perdidos.
- Se recomienda para proyectos grandes con muchos commits, ya que hace que sea más fácil rastrear cambios en el historial.
- NO se recomienda para proyectos pequeños o con pocos commits, ya que puede ser innecesario.

# Reset
El reset es una operación de Git que permite deshacer commits y mover el puntero de la rama a un commit anterior. Hay tres tipos de reset: soft, mixed y hard.
```bash
  git reset --soft <commit> # Mueve el puntero de la rama al commit especificado, pero mantiene los cambios en el área de preparación (staging area).
  git reset --mixed <commit> # Mueve el puntero de la rama al commit especificado y deshace los cambios en el área de preparación, pero mantiene los cambios en el directorio de trabajo.
  git reset --hard <commit> # Mueve el puntero de la rama al commit especificado y deshace todos los cambios en el área de preparación y en el directorio de trabajo.
```
- Es ideal para deshacer commits y mover el puntero de la rama a un commit anterior.
- Se usa cuando se quiere deshacer cambios recientes en una rama.
- Se recomienda para proyectos grandes con muchos commits, ya que hace que sea más fácil deshacer cambios recientes.
- NO se recomienda para proyectos pequeños o con pocos commits, ya que puede ser innecesario.
