---
title: "git cat-file"
source: "https://git-scm.com/docs/git-cat-file"
section: "plumbing-read"
status: "source-audited"
version: "2.55.0"
---

# `git cat-file`

Este caso usa `git cat-file` para consultar el tipo, tamaño o contenido de objetos.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Ejemplo mínimo

```bash
git cat-file -t HEAD
git cat-file -p HEAD^{tree}
```

La invocación `git cat-file -t HEAD` ejecuta esta operación: consultar el tipo, tamaño o contenido de objetos. Después, la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Sintaxis y formas de invocación

```text
git cat-file <type> <object>
git cat-file (-e | -p | -t | -s) <object>
git cat-file (--textconv | --filters)
	     [<rev>:<path|tree-ish> | --path=<path|tree-ish> <rev>]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git cat-file <type> <object>
   or: git cat-file (-e | -p | -t | -s) <object>
   or: git cat-file (--textconv | --filters)
                    [<rev>:<path|tree-ish> | --path=<path|tree-ish> <rev>]
   or: git cat-file (--batch | --batch-check | --batch-command) [--batch-all-objects]
                    [--buffer] [--follow-symlinks] [--unordered]
                    [--textconv | --filters] [-Z]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git cat-file -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-e`

Comprueba e antes de aceptar el resultado de `git cat-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `check if <object> exists`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file -e -t HEAD
printf 'exit=%s\n' "$?"
```

### `-p`

Incluye p en la salida o cambia cómo `git cat-file` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `pretty-print <object> content`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file -p -t HEAD
printf 'exit=%s\n' "$?"
```

### `-t`

Define t con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `show object type (one of 'blob', 'tree', 'commit', 'tag', ...)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file -t HEAD
printf 'exit=%s\n' "$?"
```

### `-s`

Incluye s en la salida o cambia cómo `git cat-file` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show object size`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file -s -t HEAD
printf 'exit=%s\n' "$?"
```

### `--textconv`

Ejecuta textconv durante consultar el tipo, tamaño o contenido de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `run textconv on object's content`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file --textconv -t HEAD
printf 'exit=%s\n' "$?"
```

### `--filters`

Ejecuta filters durante consultar el tipo, tamaño o contenido de objetos. En Git 2.51.1, la ayuda corta expresa el contrato como `run filters on object's content`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file --filters -t HEAD
printf 'exit=%s\n' "$?"
```

### `--path`

Define ruta para esta ejecución de `git cat-file`.

```bash
git cat-file --path=valor -t HEAD
printf 'exit=%s\n' "$?"
```

### `--batch`

Incluye batch en la salida o cambia cómo `git cat-file` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show full <object> or <rev> contents`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file --batch=oneline -t HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--batch-check`

Valida el dato o estado antes de producir el resultado.

```bash
git cat-file --batch-check=oneline -t HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--batch-command`

Lee batch command como parte de la entrada de `git cat-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `read commands from stdin`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file --batch-command=oneline -t HEAD
printf 'exit=%s\n' "$?"
```

El ejemplo usa `oneline` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El código de terminación distingue una ejecución aceptada de un error y, en algunos comandos de consulta, de una respuesta negativa. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--batch-all-objects`

Selecciona la representación o tratamiento de identificadores de objeto.

```bash
git cat-file --batch-all-objects -t HEAD
printf 'exit=%s\n' "$?"
```

### `--buffer`

Incluye buffer en la salida o cambia cómo `git cat-file` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `buffer --batch output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file --buffer -t HEAD
printf 'exit=%s\n' "$?"
```

### `--follow-symlinks`

Activa seguir renombres symlinks durante consultar el tipo, tamaño o contenido de objetos. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `follow in-tree symlinks`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file --follow-symlinks -t HEAD
printf 'exit=%s\n' "$?"
```

### `--unordered`

Impide unordered durante esta invocación de `git cat-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `do not order objects before emitting them`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file --unordered -t HEAD
printf 'exit=%s\n' "$?"
```

### `-Z`

Lee Z como parte de la entrada de `git cat-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `stdin and stdout is NUL-terminated`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git cat-file` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git cat-file -Z -t HEAD
printf 'exit=%s\n' "$?"
```

### `--use-mailmap`

Define use mailmap para esta ejecución de `git cat-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `use mail map file`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git cat-file` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git cat-file --use-mailmap -t HEAD
printf 'exit=%s\n' "$?"
```

### `--mailmap`

Define mailmap para esta ejecución de `git cat-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `alias of --use-mailmap`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file --mailmap -t HEAD
printf 'exit=%s\n' "$?"
```

### `--filter`

Limita los objetos transferidos mediante una especificación de filtro de clon parcial. En Git 2.51.1, la ayuda corta expresa el contrato como `object filtering`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git cat-file --filter=valor -t HEAD
printf 'exit=%s\n' "$?"
```

## Páginas relacionadas

- [`git cherry`](../plumbing-read/cherry.md)
- [`git diff-files`](../plumbing-read/diff-files.md)

## Fuente

- [git-cat-file - Provide contents or details of repository objects](https://git-scm.com/docs/git-cat-file)
