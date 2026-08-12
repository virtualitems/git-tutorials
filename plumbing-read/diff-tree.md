---
title: "git diff-tree"
source: "https://git-scm.com/docs/git-diff-tree"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git diff-tree`

Este caso usa `git diff-tree` para comparar los blobs y modos de dos árboles.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git diff-tree --no-commit-id --name-status -r HEAD
```

La invocación `git diff-tree --no-commit-id --name-status -r HEAD` ejecuta esta operación: comparar los blobs y modos de dos árboles. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git diff-tree [--stdin] [-m] [-s] [-v] [--no-commit-id] [--pretty]
	      [-t] [-r] [-c | --cc] [--combined-all-paths] [--root] [--merge-base]
	      [<common-diff-options>] <tree-ish> [<tree-ish>] [<path>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git diff-tree [--stdin] [-m] [-s] [-v] [--no-commit-id] [--pretty]
              [-t] [-r] [-c | --cc] [--combined-all-paths] [--root] [--merge-base]
              [<common-diff-options>] <tree-ish> [<tree-ish>] [<path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git diff-tree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git diff-tree` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git diff-tree --stdin --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-m`

Activa m durante comparar los blobs y modos de dos árboles. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-tree -m --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-s`

Activa s durante comparar los blobs y modos de dos árboles. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-tree -s --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-v`

Activa v durante comparar los blobs y modos de dos árboles. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-tree -v --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--no-commit-id`

Desactiva el comportamiento `commit-id` para esta invocación.

```bash
git diff-tree --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--pretty`

Selecciona un formato para representar commits.

```bash
git diff-tree --pretty --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-t`

Activa t durante comparar los blobs y modos de dos árboles. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-tree -t --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-r`

Activa r durante comparar los blobs y modos de dos árboles. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `diff recursively`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree -r --no-commit-id --name-status HEAD
printf 'exit=%s\n' "$?"
```

### `-c`

Aplica una clave de configuración solo a esta invocación.

```bash
git diff-tree -c --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--cc`

Incluye cc en la salida o cambia cómo `git diff-tree` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show combined diff for merge commits removing uninteresting hunks`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree --cc --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--combined-all-paths`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git diff-tree --combined-all-paths --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--root`

Incluye root en la entrada, el resultado o el registro que construye `git diff-tree`. En Git 2.51.1, la ayuda corta expresa el contrato como `include the initial commit as diff against /dev/null`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree --root --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--merge-base`

Activa merge base durante comparar los blobs y modos de dos árboles. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git diff-tree --merge-base --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git diff-tree -z --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-p`

Incluye p en la salida o cambia cómo `git diff-tree` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output patch format.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree -p --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-u`

Selecciona la relación indicada por u; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `synonym for -p.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree -u --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--patch-with-raw`

Incluye parche with raw en la salida o cambia cómo `git diff-tree` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `output both a patch and the diff-raw format.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree --patch-with-raw --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--stat`

Resume cambios mediante conteos por ruta.

Esta forma se usa cuando `git diff-tree` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque estadísticas actúa sobre el estado que Git registró al iniciar la secuencia.

```bash
git diff-tree --stat --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--numstat`

Incluye numstat en la salida o cambia cómo `git diff-tree` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show numeric diffstat instead of patch.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree --numstat --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--patch-with-stat`

Antepone parche with estadísticas al valor que produce `git diff-tree`. En Git 2.51.1, la ayuda corta expresa el contrato como `output a patch and prepend its diffstat.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree --patch-with-stat --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--name-only`

Muestra nombres de ruta sin el contenido del diff.

```bash
git diff-tree --name-only --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--name-status`

Muestra nombres y estado de cada ruta.

```bash
git diff-tree --name-status --no-commit-id -r HEAD
printf 'exit=%s\n' "$?"
```

### `--full-index`

Incluye full índice en la salida o cambia cómo `git diff-tree` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show full object name on index lines.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree --full-index --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git diff-tree --abbrev=5 --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-R`

Lee R como parte de la entrada de `git diff-tree`. En Git 2.51.1, la ayuda corta expresa el contrato como `swap input file pairs.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git diff-tree` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git diff-tree -R --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-B`

Activa B durante comparar los blobs y modos de dos árboles. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `detect complete rewrites.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree -B --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-M`

Activa M durante comparar los blobs y modos de dos árboles. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `detect renames.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción selecciona el procedimiento que `git diff-tree` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git diff-tree -M --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-C`

Ejecuta Git como si se hubiera iniciado en el directorio indicado.

La opción selecciona el procedimiento que `git diff-tree` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git diff-tree -C --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--find-copies-harder`

Controla detección o búsqueda de relaciones entre entradas.

La opción cambia cómo `git diff-tree` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git diff-tree --find-copies-harder --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-l`

Limita comparar los blobs y modos de dos árboles al alcance identificado por l. En Git 2.51.1, la ayuda corta expresa el contrato como `limit rename attempts up to <n> paths.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree -l5 --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-O`

Activa O durante comparar los blobs y modos de dos árboles. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `reorder diffs according to the <file>.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git diff-tree` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git diff-tree -Orutas.txt --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-S`

Limita comparar los blobs y modos de dos árboles al alcance identificado por S. En Git 2.51.1, la ayuda corta expresa el contrato como `find filepair whose only one side contains the string.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree -Svalor --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--pickaxe-all`

Incluye elementos adicionales dentro del alcance indicado.

```bash
git diff-tree --pickaxe-all --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `-a`

Procesa a con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `--text treat all files as text.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree -a --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

### `--text`

Procesa texto con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `--text treat all files as text.`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git diff-tree --text --no-commit-id --name-status -r HEAD
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git for-each-ref`](../plumbing-read/for-each-ref.md)
- [`git diff-pairs`](../plumbing-read/diff-pairs.md)
- [`git for-each-repo`](../plumbing-read/for-each-repo.md)

## Fuente

- [git-diff-tree - Compares the content and mode of blobs found via two tree objects](https://git-scm.com/docs/git-diff-tree)
