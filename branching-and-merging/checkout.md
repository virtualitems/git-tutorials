---
title: "git checkout"
source: "https://git-scm.com/docs/git-checkout"
section: "branching-and-merging"
status: "source-audited"
version: "2.55.0"
---

# `git checkout`

Este caso usa `git checkout` para cambiar de rama o restaurar rutas desde otro estado.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Ejemplo mínimo

```bash
git checkout main
git checkout HEAD~1 -- README.md
```

La invocación `git checkout main` ejecuta esta operación: cambiar de rama o restaurar rutas desde otro estado. Después, `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Sintaxis y formas de invocación

```text
git checkout [-q] [-f] [-m] [<branch>]
git checkout [-q] [-f] [-m] --detach [<branch>]
git checkout [-q] [-f] [-m] [--detach] <commit>
git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new-branch>] [<start-point>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git checkout [<options>] <branch>
   or: git checkout [<options>] [<branch>] -- <file>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git checkout -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git checkout --quiet main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-f` y `--force`

Omite una protección concreta; úsala solo después de verificar el estado objetivo.

#### Ejemplo con `--force`

```bash
git checkout --force main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-m` y `--merge`

Ejecuta merge durante cambiar de rama o restaurar rutas desde otro estado. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a 3-way merge with the new branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--merge`

```bash
git checkout --merge main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--detach` y `-d`

Hace que `HEAD` apunte directamente a un commit.

#### Ejemplo con `--detach`

```bash
git checkout --detach main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-b`

Crea b como parte de cambiar de rama o restaurar rutas desde otro estado. En Git 2.51.1, la ayuda corta expresa el contrato como `create and checkout a new branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git checkout -b main main
git status --short
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-B`

Restablece B como parte de cambiar de rama o restaurar rutas desde otro estado. En Git 2.51.1, la ayuda corta expresa el contrato como `create/reset and checkout a branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git checkout -B main main
git status --short
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--orphan`

Crea o cambia a una rama sin padres en el historial existente. En Git 2.51.1, la ayuda corta expresa el contrato como `new unborn branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git checkout --orphan=main main
git status --short
```

El ejemplo usa `main` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-l`

Crea l como parte de cambiar de rama o restaurar rutas desde otro estado. En Git 2.51.1, la ayuda corta expresa el contrato como `create reflog for new branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git checkout -l main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--guess`

Permite deducir una rama local a partir de una rama remota con el mismo nombre. En Git 2.51.1, la ayuda corta expresa el contrato como `second guess 'git checkout <no-such-branch>' (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git checkout --guess main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--overlay`

Define overlay para esta ejecución de `git checkout`. En Git 2.51.1, la ayuda corta expresa el contrato como `use overlay mode (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git checkout --overlay main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git checkout --recurse-submodules main
git status --short
```

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git checkout --progress main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--conflict`

Selecciona el estilo de marcadores que Git escribe al materializar un conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `conflict style (merge, diff3, or zdiff3)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git checkout --conflict=short main
git status --short
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-t` y `--track`

Crea o ajusta la asociación de seguimiento solicitada.

#### Ejemplo con `--track`

```bash
git checkout --track=valor main
git status --short
```

En esta forma, `valor` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--overwrite-ignore`

Excluye elementos que cumplan la condición indicada.

```bash
git checkout --overwrite-ignore main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-other-worktrees`

Excluye elementos que cumplan la condición indicada.

```bash
git checkout --ignore-other-worktrees main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-2` y `--ours`

Selecciona la versión de la etapa ours para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `checkout our version for unmerged files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--ours`

```bash
git checkout --ours main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-3` y `--theirs`

Selecciona la versión de la etapa theirs para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `checkout their version for unmerged files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--theirs`

```bash
git checkout --theirs main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-p` y `--patch`

Permite elegir hunks en vez de operar sobre el archivo completo.

#### Ejemplo con `--patch`

```bash
git checkout --patch main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-U` y `--unified`

Define cuántas líneas de contexto rodean cada hunk.

#### Ejemplo con `--unified`

```bash
git checkout --unified=5 main
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--inter-hunk-context`

Fusiona hunks cercanos cuando la distancia no supera el límite indicado.

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

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

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

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-guess`

Desactiva para esta invocación el comportamiento que habilita `--guess`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git checkout --no-guess main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-overlay`

Desactiva para esta invocación el comportamiento que habilita `--overlay`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git checkout --no-overlay main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git checkout --no-recurse-submodules main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git checkout --no-progress main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-track`

Desactiva para esta invocación el comportamiento que habilita `--track`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git checkout --no-track main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-overwrite-ignore`

Desactiva para esta invocación el comportamiento que habilita `--overwrite-ignore`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git checkout --no-overwrite-ignore main
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git history`](../branching-and-merging/history.md)
- [`git branch`](../branching-and-merging/branch.md)
- [`git merge`](../branching-and-merging/merge.md)

## Fuente

- [git-checkout - Switch branches or restore working tree files](https://git-scm.com/docs/git-checkout)
