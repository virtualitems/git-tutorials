---
title: "git ls-files"
source: "https://git-scm.com/docs/git-ls-files"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git ls-files`

Este caso usa `git ls-files` para enumerar entradas del índice y su relación con el área de trabajo.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git ls-files --stage
git ls-files --others --exclude-standard
```

La invocación `git ls-files --stage` ejecuta esta operación: enumerar entradas del índice y su relación con el área de trabajo. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git ls-files [-z] [-t] [-v] [-f]
		[-c|--cached] [-d|--deleted] [-o|--others] [-i|--ignored]
		[-s|--stage] [-u|--unmerged] [-k|--killed] [-m|--modified]
		[--resolve-undo]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git ls-files [<options>] [<file>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git ls-files -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git ls-files -z --stage
printf 'exit=%s\n' "$?"
```

### `-t`

Activa t durante enumerar entradas del índice y su relación con el área de trabajo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `identify the file status with tags`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-files -t --stage
printf 'exit=%s\n' "$?"
```

### `-v`

Define v para esta ejecución de `git ls-files`. En Git 2.51.1, la ayuda corta expresa el contrato como `use lowercase letters for 'assume unchanged' files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-files -v --stage
printf 'exit=%s\n' "$?"
```

### `-f`

Define f para esta ejecución de `git ls-files`. En Git 2.51.1, la ayuda corta expresa el contrato como `use lowercase letters for 'fsmonitor clean' files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git ls-files` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git ls-files -f --stage
printf 'exit=%s\n' "$?"
```

### `-c` y `--cached`

Usa el índice como origen o destino, sin tratar el área de trabajo de la misma forma.

#### Ejemplo con `--cached`

```bash
git ls-files --cached --stage
printf 'exit=%s\n' "$?"
```

### `-d` y `--deleted`

Incluye deleted en la salida o cambia cómo `git ls-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show deleted files in the output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--deleted`

```bash
git ls-files --deleted --stage
printf 'exit=%s\n' "$?"
```

### `-o` y `--others`

Incluye others en la salida o cambia cómo `git ls-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show other files in the output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--others`

```bash
git ls-files --others --stage
printf 'exit=%s\n' "$?"
```

### `-i` y `--ignored`

Incluye archivos ignorados en la vista solicitada. En Git 2.51.1, la ayuda corta expresa el contrato como `show ignored files in the output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--ignored`

```bash
git ls-files --ignored --stage
printf 'exit=%s\n' "$?"
```

### `-s` y `--stage`

Incluye stage en la salida o cambia cómo `git ls-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show staged contents' object name in the output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--stage`

```bash
git ls-files --stage
printf 'exit=%s\n' "$?"
```

### `-u` y `--unmerged`

Incluye unmerged en la salida o cambia cómo `git ls-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show unmerged files in the output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--unmerged`

```bash
git ls-files --unmerged --stage
printf 'exit=%s\n' "$?"
```

### `-k` y `--killed`

Incluye killed en la salida o cambia cómo `git ls-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show files on the filesystem that need to be removed`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--killed`

```bash
git ls-files --killed --stage
printf 'exit=%s\n' "$?"
```

### `-m` y `--modified`

Incluye modified en la salida o cambia cómo `git ls-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show modified files in the output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--modified`

```bash
git ls-files --modified --stage
printf 'exit=%s\n' "$?"
```

### `--resolve-undo`

Incluye resolución undo en la salida o cambia cómo `git ls-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show resolve-undo information`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-files --resolve-undo --stage
printf 'exit=%s\n' "$?"
```

### `--directory`

Añade el prefijo indicado a las rutas afectadas antes de procesarlas. En Git 2.51.1, la ayuda corta expresa el contrato como `show 'other' directories' names only`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-files --directory --stage
printf 'exit=%s\n' "$?"
```

### `--eol`

Incluye eol en la salida o cambia cómo `git ls-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show line endings of files`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-files --eol --stage
printf 'exit=%s\n' "$?"
```

### `--empty-directory`

Impide vacío directorio durante esta invocación de `git ls-files`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't show empty directories`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-files --empty-directory --stage
printf 'exit=%s\n' "$?"
```

### `-x` y `--exclude`

Excluye elementos que cumplan la condición indicada.

Esta forma se usa cuando `git ls-files` ya dejó una operación en curso. Revisa `git status` antes de ejecutarla porque excluir actúa sobre el estado que Git registró al iniciar la secuencia.

#### Ejemplo con `--exclude`

```bash
git ls-files --exclude=TODO --stage
printf 'exit=%s\n' "$?"
```

En esta forma, `TODO` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `-X` y `--exclude-from`

Excluye elementos que cumplan la condición indicada.

#### Ejemplo con `--exclude-from`

```bash
git ls-files --exclude-from=rutas.txt --stage
printf 'exit=%s\n' "$?"
```

En esta forma, `rutas.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa.

### `--exclude-per-directory`

Excluye elementos que cumplan la condición indicada.

```bash
git ls-files --exclude-per-directory=rutas.txt --stage
printf 'exit=%s\n' "$?"
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--exclude-standard`

Excluye elementos que cumplan la condición indicada.

```bash
git ls-files --exclude-standard --stage
printf 'exit=%s\n' "$?"
```

### `--full-name`

Incluye full nombre en la salida o cambia cómo `git ls-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `make the output relative to the project top directory`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-files --full-name --stage
printf 'exit=%s\n' "$?"
```

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git ls-files --recurse-submodules --stage
printf 'exit=%s\n' "$?"
```

### `--error-unmatch`

Procesa error unmatch con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `if any <file> is not in the index, treat this as an error`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git ls-files` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git ls-files --error-unmatch --stage
printf 'exit=%s\n' "$?"
```

### `--with-tree`

Activa with tree durante enumerar entradas del índice y su relación con el área de trabajo. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `pretend that paths removed since <tree-ish> are still present`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-files --with-tree=HEAD^{tree} --stage
printf 'exit=%s\n' "$?"
```

El ejemplo usa `HEAD^{tree}` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git ls-files --abbrev=5 --stage
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--debug`

Incluye debug en la salida o cambia cómo `git ls-files` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show debugging data`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-files --debug --stage
printf 'exit=%s\n' "$?"
```

### `--deduplicate`

Suprime deduplicate en la salida de esta invocación de `git ls-files`. En Git 2.51.1, la ayuda corta expresa el contrato como `suppress duplicate entries`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-files --deduplicate --stage
printf 'exit=%s\n' "$?"
```

### `--sparse`

Permite operar sobre entradas que quedan fuera de la selección sparse activa.

```bash
git ls-files --sparse --stage
printf 'exit=%s\n' "$?"
```

### `--format`

Define los campos y separadores de la salida.

```bash
git ls-files --format=oneline --stage
printf 'exit=%s\n' "$?"
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-empty-directory`

Desactiva para esta invocación el comportamiento que habilita `--empty-directory`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git ls-files --no-empty-directory --stage
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git ls-tree`](../plumbing-read/ls-tree.md)
- [`git get-tar-commit-id`](../plumbing-read/get-tar-commit-id.md)
- [`git merge-base`](../plumbing-read/merge-base.md)

## Fuente

- [git-ls-files - Show information about files in the index and the working tree](https://git-scm.com/docs/git-ls-files)
