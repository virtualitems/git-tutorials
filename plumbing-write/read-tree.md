---
title: "git read-tree"
source: "https://git-scm.com/docs/git-read-tree"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git read-tree`

Este caso usa `git read-tree` para cargar información de árboles en el índice.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git read-tree HEAD
git ls-files --stage
```

La invocación `git read-tree HEAD` ejecuta esta operación: cargar información de árboles en el índice. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git read-tree [(-m [--trivial] [--aggressive] | --reset | --prefix=<prefix>)
		[-u | -i]] [--index-output=<file>] [--no-sparse-checkout]
		(--empty | <tree-ish1> [<tree-ish2> [<tree-ish3>]])
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git read-tree [(-m [--trivial] [--aggressive] | --reset | --prefix=<prefix>)
                     [-u | -i]] [--index-output=<file>] [--no-sparse-checkout]
                     (--empty | <tree-ish1> [<tree-ish2> [<tree-ish3>]])
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git read-tree -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-m`

Ejecuta m durante cargar información de árboles en el índice. En Git 2.51.1, la ayuda corta expresa el contrato como `perform a merge in addition to a read`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git read-tree -m HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--trivial`

Activa trivial durante cargar información de árboles en el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `3-way merge if no file level merging required`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git read-tree` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git read-tree --trivial HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--aggressive`

Activa aggressive durante cargar información de árboles en el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `3-way merge in presence of adds and removes`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git read-tree --aggressive HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--reset`

Restablece restablecer como parte de cargar información de árboles en el índice. En Git 2.51.1, la ayuda corta expresa el contrato como `same as -m, but discard unmerged entries`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git read-tree --reset HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--prefix`

Lee prefix como parte de la entrada de `git read-tree`. En Git 2.51.1, la ayuda corta expresa el contrato como `read the tree into the index under <subdirectory>/`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git read-tree --prefix=valor HEAD
git fsck --no-progress
```

### `-u`

Actualiza u como parte de cargar información de árboles en el índice. En Git 2.51.1, la ayuda corta expresa el contrato como `update working tree with merge result`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git read-tree -u HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-i`

Impide i durante esta invocación de `git read-tree`. En Git 2.51.1, la ayuda corta expresa el contrato como `don't check the working tree after merging`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git read-tree -i HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--index-output`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

```bash
git read-tree --index-output=rutas.txt HEAD
git fsck --no-progress
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-sparse-checkout`

Desactiva el comportamiento `sparse-checkout` para esta invocación.

```bash
git read-tree --no-sparse-checkout HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--empty`

Limita cargar información de árboles en el índice al alcance identificado por vacío. En Git 2.51.1, la ayuda corta expresa el contrato como `only empty the index`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git read-tree --empty HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git read-tree --verbose HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `--exclude-per-directory`

Excluye elementos que cumplan la condición indicada.

```bash
git read-tree --exclude-per-directory=valor HEAD
git fsck --no-progress
```

### `-n` y `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

#### Ejemplo con `--dry-run`

```bash
git read-tree --dry-run HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `--sparse-checkout`

Selecciona la relación indicada por sparse checkout; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-sparse-checkout`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git read-tree --sparse-checkout HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--debug-unpack`

Activa debug unpack durante cargar información de árboles en el índice. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `debug unpack-trees`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git read-tree --debug-unpack HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--recurse-submodules`

Propaga la operación a submódulos dentro del alcance.

```bash
git read-tree --recurse-submodules=valor HEAD
git fsck --no-progress
```

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git read-tree --quiet HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

## Páginas relacionadas

- [`git symbolic-ref`](../plumbing-write/symbolic-ref.md)
- [`git prune-packed`](../plumbing-write/prune-packed.md)
- [`git unpack-objects`](../plumbing-write/unpack-objects.md)

## Fuente

- [git-read-tree - Reads tree information into the index](https://git-scm.com/docs/git-read-tree)
