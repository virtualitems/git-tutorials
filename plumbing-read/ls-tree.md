---
title: "git ls-tree"
source: "https://git-scm.com/docs/git-ls-tree"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git ls-tree`

Este caso usa `git ls-tree` para enumerar el contenido de un objeto árbol.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git ls-tree -r --name-only HEAD
```

La invocación `git ls-tree -r --name-only HEAD` ejecuta esta operación: enumerar el contenido de un objeto árbol. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git ls-tree [-d] [-r] [-t] [-l] [-z]
	    [--name-only] [--name-status] [--object-only] [--full-name] [--full-tree] [--abbrev[=<n>]] [--format=<format>]
	    <tree-ish> [<path>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git ls-tree [<options>] <tree-ish> [<path>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git ls-tree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-d`

Limita enumerar el contenido de un objeto árbol al alcance identificado por d. En Git 2.51.1, la ayuda corta expresa el contrato como `only show trees`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-tree -d -r --name-only HEAD
printf 'exit=%s\n' "$?"
```

### `-r`

Activa r durante enumerar el contenido de un objeto árbol. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `recurse into subtrees`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-tree -r --name-only HEAD
printf 'exit=%s\n' "$?"
```

### `-t`

Incluye t en la salida o cambia cómo `git ls-tree` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show trees when recursing`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-tree -t -r --name-only HEAD
printf 'exit=%s\n' "$?"
```

### `-l` y `--long`

Incluye long en la entrada, el resultado o el registro que construye `git ls-tree`. En Git 2.51.1, la ayuda corta expresa el contrato como `include object size`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--long`

```bash
git ls-tree --long -r --name-only HEAD
printf 'exit=%s\n' "$?"
```

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

```bash
git ls-tree -z -r --name-only HEAD
printf 'exit=%s\n' "$?"
```

### `--name-only`

Muestra nombres de ruta sin el contenido del diff.

```bash
git ls-tree --name-only -r HEAD
printf 'exit=%s\n' "$?"
```

### `--name-status`

Muestra nombres y estado de cada ruta.

```bash
git ls-tree --name-status -r --name-only HEAD
printf 'exit=%s\n' "$?"
```

### `--object-only`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git ls-tree --object-only -r --name-only HEAD
printf 'exit=%s\n' "$?"
```

### `--full-name`

Define full nombre para esta ejecución de `git ls-tree`. En Git 2.51.1, la ayuda corta expresa el contrato como `use full path names`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-tree --full-name -r --name-only HEAD
printf 'exit=%s\n' "$?"
```

### `--full-tree`

Incluye full tree en la salida o cambia cómo `git ls-tree` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `list entire tree; not just current directory (implies --full-name)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git ls-tree --full-tree -r --name-only HEAD
printf 'exit=%s\n' "$?"
```

### `--abbrev`

Reduce la representación visible del identificador sin cambiar el objeto.

```bash
git ls-tree --abbrev=5 -r --name-only HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--format`

Define los campos y separadores de la salida.

```bash
git ls-tree --format=oneline -r --name-only HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git merge-base`](../plumbing-read/merge-base.md)
- [`git ls-files`](../plumbing-read/ls-files.md)
- [`git name-rev`](../plumbing-read/name-rev.md)

## Fuente

- [git-ls-tree - List the contents of a tree object](https://git-scm.com/docs/git-ls-tree)
