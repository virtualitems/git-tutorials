---
title: "git restore"
source: "https://git-scm.com/docs/git-restore"
section: "basic-snapshotting"
status: "source-audited"
version: "2.55.0"
---

# `git restore`

Este caso usa `git restore` para recuperar contenido de rutas en el índice o el área de trabajo.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Ejemplo mínimo

```bash
git restore --source=HEAD -- guia.txt
git restore --staged guia.txt
```

La invocación `git restore --source=HEAD -- guia.txt` ejecuta esta operación: recuperar contenido de rutas en el índice o el área de trabajo. Después, `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Sintaxis y formas de invocación

```text
git restore [<options>] [--source=<tree>] [--staged] [--worktree] [--] <pathspec>…
git restore [<options>] [--source=<tree>] [--staged] [--worktree] --pathspec-from-file=<file> [--pathspec-file-nul]
git restore (-p|--patch) [<options>] [--source=<tree>] [--staged] [--worktree] [--] [<pathspec>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git restore [<options>] [--source=<branch>] <file>...
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git restore -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--source` y `-s`

Activa source durante recuperar contenido de rutas en el índice o el área de trabajo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `which tree-ish to checkout from`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--source`

```bash
git restore --source=HEAD^{tree} -- guia.txt
git status --short
```

En esta forma, `HEAD^{tree}` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--staged` y `-S`

Selecciona el contenido preparado en el índice.

#### Ejemplo con `--staged`

```bash
git restore --staged --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--worktree` y `-W`

Selecciona o modifica el área de trabajo.

#### Ejemplo con `--worktree`

```bash
git restore --worktree --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--pathspec-from-file`

Lee pathspecs desde un archivo o desde stdin.

La opción cambia cómo `git restore` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git restore --pathspec-from-file=rutas.txt --source=HEAD -- guia.txt
git status --short
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--pathspec-file-nul`

Interpreta los pathspecs de archivo como registros terminados en NUL.

La opción cambia cómo `git restore` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git restore --pathspec-file-nul --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p` y `--patch`

Permite elegir hunks en vez de operar sobre el archivo completo.

#### Ejemplo con `--patch`

```bash
git restore --patch --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--ignore-unmerged`

Excluye elementos que cumplan la condición indicada.

```bash
git restore --ignore-unmerged --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--overlay`

Define overlay para esta ejecución de `git restore`. En Git 2.51.1, la ayuda corta expresa el contrato como `use overlay mode`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git restore --overlay --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git restore --quiet --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git restore --recurse-submodules --source=HEAD -- guia.txt
git status --short
```

### `--progress`

Muestra progreso aunque la salida no sea un terminal.

```bash
git restore --progress --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-m` y `--merge`

Ejecuta merge durante recuperar contenido de rutas en el índice o el área de trabajo. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a 3-way merge with the new branch`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--merge`

```bash
git restore --merge --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--conflict`

Selecciona el estilo de marcadores que Git escribe al materializar un conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `conflict style (merge, diff3, or zdiff3)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git restore --conflict=short --source=HEAD -- guia.txt
git status --short
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-2` y `--ours`

Selecciona la versión de la etapa ours para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `checkout our version for unmerged files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--ours`

```bash
git restore --ours --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-3` y `--theirs`

Selecciona la versión de la etapa theirs para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `checkout their version for unmerged files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--theirs`

```bash
git restore --theirs --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-U` y `--unified`

Define cuántas líneas de contexto rodean cada hunk.

#### Ejemplo con `--unified`

```bash
git restore --unified=5 --source=HEAD -- guia.txt
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--inter-hunk-context`

Fusiona hunks cercanos cuando la distancia no supera el límite indicado.

```bash
git restore --inter-hunk-context=5 --source=HEAD -- guia.txt
git status --short
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-skip-worktree-bits`

Excluye elementos que cumplan la condición indicada.

Esta forma se usa cuando `git restore` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque ignorar omitir el elemento actual área de trabajo bits actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git restore --ignore-skip-worktree-bits --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-overlay`

Desactiva para esta invocación el comportamiento que habilita `--overlay`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git restore --no-overlay --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse-submodules`

Desactiva para esta invocación el comportamiento que habilita `--recurse-submodules`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git restore --no-recurse-submodules --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-progress`

Desactiva para esta invocación el comportamiento que habilita `--progress`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git restore --no-progress --source=HEAD -- guia.txt
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git rm`](../basic-snapshotting/rm.md)
- [`git reset`](../basic-snapshotting/reset.md)
- [`git status`](../basic-snapshotting/status.md)

## Fuente

- [git-restore - Restore working tree files](https://git-scm.com/docs/git-restore)
