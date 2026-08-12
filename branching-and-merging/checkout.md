---
title: "git checkout"
source: "https://git-scm.com/docs/git-checkout"
section: "branching-and-merging"
status: "option-expanded"
---

# `git checkout`

Este caso usa `git checkout` para cambiar de rama o restaurar rutas desde otro estado. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Responsabilidad y efecto

git checkout consulta o cambia referencias, `HEAD`, worktrees y estados de integración. Recibe como entrada las ramas, commits o rutas que participan en la operación. La operación consiste en cambiar de rama o restaurar rutas desde otro estado.

Puede persistir el estado implicado por esta operación: cambiar de rama o restaurar rutas desde otro estado. Las opciones pueden limitar o ampliar ese efecto.

## Preparación

Los ejemplos que necesitan un repositorio parten del [laboratorio base de `git init`](../getting-and-creating-projects/init.md#laboratorio-base). La posición de opciones, revisiones y rutas sigue las [convenciones de la interfaz de Git](../guides/gitcli.md#convenciones-de-la-cli). Los nombres como `HEAD`, `main`, `HEAD~2` y `A..B` se explican en [revisiones y rangos](../guides/gitrevisions.md#revisiones-y-rangos). La selección de rutas se explica en [pathspecs y separación con `--`](../guides/gitcli.md#pathspecs). Antes de ejecutar una forma que escriba datos, registra `git status --short` y las referencias que puedan cambiar.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git checkout main
git checkout HEAD~1 -- README.md
```

La invocación `git checkout main` ejecuta esta operación: cambiar de rama o restaurar rutas desde otro estado. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes. Conserva stdout, stderr y el código de terminación cuando el ejemplo forme parte de un script.

## Sintaxis y formas de invocación

```text
git checkout [-q] [-f] [-m] [<branch>]
git checkout [-q] [-f] [-m] --detach [<branch>]
git checkout [-q] [-f] [-m] [--detach] <commit>
git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new-branch>] [<start-point>]
```

### Uso verificado con `git version 2.51.1`

```text
git checkout [<options>] <branch>
   or: git checkout [<options>] [<branch>] -- <file>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git checkout -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Flujos de uso

### Caso base

cambiar de rama o restaurar rutas desde otro estado. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Ejecuta el ejemplo mínimo y registra el estado antes y después.

### Alcance explícito

Aplicar git checkout a una referencia, rango o ruta identificada. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. Resuelve cada argumento antes de ejecutar y usa `--` para rutas.

### Validación

Comprobar el resultado de git checkout con una orden de lectura independiente. Usa el [ejemplo mínimo](#ejemplo-mínimo) como punto de partida. No uses la misma salida como única prueba del cambio.

## Opciones

Cada apartado usa una opción en una invocación concreta. Las opciones equivalentes comparten la explicación, pero cada alias tiene su propio ejemplo. Ejecuta una opción por vez antes de combinarlas.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.  La misma línea de ayuda también acepta `-q`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

#### Ejemplo con `-q`

```bash
git checkout -q main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--quiet`

```bash
git checkout --quiet main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.  La misma línea de ayuda también acepta `-f`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción controla omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o restaurar rutas desde otro estado puede retirar o reemplazar datos dentro del alcance seleccionado.

#### Ejemplo con `-f`

```bash
git checkout -f main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--force`

```bash
git checkout --force main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-m` y `--merge`

Ejecuta merge durante cambiar de rama o restaurar rutas desde otro estado. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a 3-way merge with the new branch`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-m`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-m`

```bash
git checkout -m main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--merge`

```bash
git checkout --merge main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--detach` y `-d`

Hace que `HEAD` apunte directamente a un commit.  La misma línea de ayuda también acepta `-d`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git checkout`, HEAD separado modifica la forma en que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `--detach`

```bash
git checkout --detach main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `-d`

```bash
git checkout -d main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-b`

Crea b como parte de cambiar de rama o restaurar rutas desde otro estado. En Git 2.51.1, la ayuda corta expresa el contrato como `create and checkout a new branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout -b main main
git status --short
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-B`

Restablece B como parte de cambiar de rama o restaurar rutas desde otro estado. En Git 2.51.1, la ayuda corta expresa el contrato como `create/reset and checkout a branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout -B main main
git status --short
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--orphan`

Crea o cambia a una rama sin padres en el historial existente. En Git 2.51.1, la ayuda corta expresa el contrato como `new unborn branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout --orphan=main main
git status --short
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-l`

Crea l como parte de cambiar de rama o restaurar rutas desde otro estado. En Git 2.51.1, la ayuda corta expresa el contrato como `create reflog for new branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout -l main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--guess`

Permite deducir una rama local a partir de una rama remota con el mismo nombre. En Git 2.51.1, la ayuda corta expresa el contrato como `second guess 'git checkout <no-such-branch>' (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout --guess main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--overlay`

Define overlay para esta ejecución de `git checkout`. En Git 2.51.1, la ayuda corta expresa el contrato como `use overlay mode (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git checkout`, overlay modifica la forma en que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git checkout --overlay main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git checkout --recurse-submodules=valor main
git status --short
```

El ejemplo usa `valor` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

La opción controla progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o restaurar rutas desde otro estado puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git checkout --progress main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--conflict`

Selecciona el estilo de marcadores que Git escribe al materializar un conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `conflict style (merge, diff3, or zdiff3)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

En `git checkout`, conflict modifica la forma en que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git checkout --conflict=short main
git status --short
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-t` y `--track`

Crea o ajusta la asociación de seguimiento solicitada.  La misma línea de ayuda también acepta `-t`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-t`

```bash
git checkout -t=valor main
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--track`

```bash
git checkout --track=valor main
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--overwrite-ignore`

Excluye elementos que cumplan la condición indicada.

La opción controla overwrite ignorar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o restaurar rutas desde otro estado puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git checkout --overwrite-ignore main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-other-worktrees`

Excluye elementos que cumplan la condición indicada.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout --ignore-other-worktrees main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-2` y `--ours`

Selecciona la versión de la etapa ours para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `checkout our version for unmerged files`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-2`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-2`

```bash
git checkout -2 main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--ours`

```bash
git checkout --ours main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-3` y `--theirs`

Selecciona la versión de la etapa theirs para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `checkout their version for unmerged files`. Conserva esa formulación al comparar el efecto entre versiones de Git. La misma línea de ayuda también acepta `-3`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

#### Ejemplo con `-3`

```bash
git checkout -3 main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--theirs`

```bash
git checkout --theirs main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-p` y `--patch`

Permite elegir hunks en vez de operar sobre el archivo completo.  La misma línea de ayuda también acepta `-p`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git checkout`, parche modifica la forma en que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-p`

```bash
git checkout -p main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--patch`

```bash
git checkout --patch main
git status --short
```

Esta forma no recibe un valor separado; los argumentos posteriores pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `-U` y `--unified`

Define cuántas líneas de contexto rodean cada hunk.  La misma línea de ayuda también acepta `-U`. Esas formas seleccionan el mismo comportamiento; cambia la escritura del argumento, no el efecto.

Estas escrituras son alias: seleccionan el mismo comportamiento. Se documentan juntas para no duplicar la regla, pero cada una conserva su propia invocación reproducible.

En `git checkout`, unified modifica la forma en que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

#### Ejemplo con `-U`

```bash
git checkout -U 5 main
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

#### Ejemplo con `--unified`

```bash
git checkout --unified=5 main
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

Ejecuta una sola alternativa cada vez. Si ejecutas varias consecutivamente, el primer comando puede cambiar el estado que observa el siguiente.

### `--inter-hunk-context`

Fusiona hunks cercanos cuando la distancia no supera el límite indicado.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git checkout --inter-hunk-context=5 main
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-skip-worktree-bits`

Excluye elementos que cumplan la condición indicada.

Esta forma se usa cuando `git checkout` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque ignorar omitir el elemento actual área de trabajo bits actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git checkout --ignore-skip-worktree-bits main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-from-file`

Lee pathspecs desde un archivo o desde stdin.

La opción cambia cómo `git checkout` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout --pathspec-from-file=rutas.txt main
git status --short
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-file-nul`

Interpreta los pathspecs de archivo como registros terminados en NUL.

La opción cambia cómo `git checkout` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout --pathspec-file-nul main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-detach`

Desactiva para esta invocación el comportamiento que habilita `--detach`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git checkout`, desactivar HEAD separado modifica la forma en que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git checkout --no-detach main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-orphan`

Desactiva para esta invocación el comportamiento que habilita `--orphan`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout --no-orphan main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-guess`

Desactiva para esta invocación el comportamiento que habilita `--guess`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout --no-guess main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-overlay`

Desactiva para esta invocación el comportamiento que habilita `--overlay`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git checkout`, desactivar overlay modifica la forma en que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git checkout --no-overlay main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-quiet`

Desactiva para esta invocación el comportamiento que habilita `--quiet`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia la representación o el canal del resultado. Úsala cuando una persona o un script necesite campos, separadores o cantidad de mensajes definidos. El contenido mostrado puede cambiar aunque el repositorio permanezca igual.

```bash
git checkout --no-quiet main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción añade, retira o consulta una comprobación previa. Ejecuta primero la forma que no escribe cuando exista y conserva el código de terminación como parte del resultado.

```bash
git checkout --no-recurse-submodules main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar progreso. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o restaurar rutas desde otro estado puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git checkout --no-progress main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-merge`

Desactiva para esta invocación el comportamiento que habilita `--merge`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout --no-merge main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-conflict`

Desactiva para esta invocación el comportamiento que habilita `--conflict`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git checkout`, desactivar conflict modifica la forma en que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git checkout --no-conflict main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-track`

Desactiva para esta invocación el comportamiento que habilita `--track`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout --no-track main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-force`

Desactiva para esta invocación el comportamiento que habilita `--force`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar omitir la protección. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o restaurar rutas desde otro estado puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git checkout --no-force main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-overwrite-ignore`

Desactiva para esta invocación el comportamiento que habilita `--overwrite-ignore`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción controla desactivar overwrite ignorar. Registra el estado de las referencias y conserva los cambios sin commit antes de usarla, porque cambiar de rama o restaurar rutas desde otro estado puede retirar o reemplazar datos dentro del alcance seleccionado.

```bash
git checkout --no-overwrite-ignore main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-other-worktrees`

Desactiva para esta invocación el comportamiento que habilita `--ignore-other-worktrees`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción limita o amplía el conjunto sobre el que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Comprueba la selección con una forma de lectura antes de combinarla con una opción que escriba estado.

```bash
git checkout --no-ignore-other-worktrees main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-patch`

Desactiva para esta invocación el comportamiento que habilita `--patch`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

En `git checkout`, desactivar parche modifica la forma en que se ejecuta cambiar de rama o restaurar rutas desde otro estado. Mantén iguales los demás argumentos para atribuir el cambio observado a esta opción.

```bash
git checkout --no-patch main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-ignore-skip-worktree-bits`

Desactiva para esta invocación el comportamiento que habilita `--ignore-skip-worktree-bits`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

Esta forma se usa cuando `git checkout` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque desactivar ignorar omitir el elemento actual área de trabajo bits actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git checkout --no-ignore-skip-worktree-bits main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-pathspec-from-file`

Desactiva para esta invocación el comportamiento que habilita `--pathspec-from-file`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git checkout` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout --no-pathspec-from-file main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-pathspec-file-nul`

Desactiva para esta invocación el comportamiento que habilita `--pathspec-file-nul`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git checkout` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git checkout --no-pathspec-file-nul main
git status --short
```

La opción no recibe un valor separado en la forma mostrada por la ayuda corta. Los argumentos que aparecen después pertenecen a `git checkout` o a otra opción. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Errores y diagnóstico

### La referencia es ambigua

Comprueba esta causa: Un nombre coincide con más de un objeto o una ruta. Usa `--` para separar rutas y una revisión completa para el objeto.

### El cambio de rama se rechaza

Comprueba esta causa: Hay modificaciones que serían sobrescritas. Confirma el estado y decide entre commit, stash o descarte.

### La integración se detiene

Comprueba esta causa: Dos cambios afectan la misma región o ruta. Resuelve, añade los archivos y usa la orden `--continue` o `--abort` que corresponda.

## Automatización y recuperación

Persistencia: Puede persistir el estado implicado por esta operación: cambiar de rama o restaurar rutas desde otro estado. Las opciones pueden limitar o ampliar ese efecto. Antes de una operación que mueva o elimine referencias, registra sus hashes con `git show-ref`. Antes de cambiar archivos, conserva `git diff` y `git diff --cached`. Para objetos y commits que dejaron de estar referenciados, consulta el reflog antes de ejecutar mantenimiento que pueda eliminarlos.

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

Añade una segunda ejecución con una entrada inválida. El ejercicio queda verificado cuando puedes explicar el código de terminación, el canal del diagnóstico y el estado que permaneció sin cambios.

## Páginas relacionadas

- [`git history`](../branching-and-merging/history.md)
- [`git branch`](../branching-and-merging/branch.md)
- [`git merge`](../branching-and-merging/merge.md)

## Fuente

- [git-checkout - Switch branches or restore working tree files](https://git-scm.com/docs/git-checkout)
