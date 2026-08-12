---
title: "git archive"
source: "https://git-scm.com/docs/git-archive"
section: "administration"
status: "source-audited"
version: "2.55.0"
---

# `git archive`

Este caso usa `git archive` para crear un archivo tar o zip a partir de un árbol de Git.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Ejemplo mínimo

```bash
git archive --format=zip --output=entrega.zip HEAD
```

La invocación `git archive --format=zip --output=entrega.zip HEAD` ejecuta esta operación: crear un archivo tar o zip a partir de un árbol de Git. Después, los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Sintaxis y formas de invocación

```text
git archive [--format=<fmt>] [--list] [--prefix=<prefix>/] [<extra>]
	      [-o <file> | --output=<file>] [--worktree-attributes]
	      [--remote=<repo> [--exec=<git-upload-archive>]] <tree-ish>
	      [<path>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git archive [<options>] <tree-ish> [<path>...]
   or: git archive --list
   or: git archive --remote <repo> [--exec <cmd>] [<options>] <tree-ish> [<path>...]
   or: git archive --remote <repo> [--exec <cmd>] --list
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git archive -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `--format`

Define los campos y separadores de la salida.

```bash
git archive --format=valor --output=entrega.zip HEAD
git count-objects -vH
```

### `--list` y `-l`

Incluye información adicional en la salida.

#### Ejemplo con `--list`

```bash
git archive --list --format=zip --output=entrega.zip HEAD
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--prefix`

Antepone prefix al valor que produce `git archive`. En Git 2.51.1, la ayuda corta expresa el contrato como `prepend prefix to each pathname in the archive`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git archive --prefix=refs/heads/ --format=zip --output=entrega.zip HEAD
git count-objects -vH
```

El ejemplo usa `refs/heads/` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-o` y `--output`

Escribe el resultado en la ruta indicada.

#### Ejemplo con `--output`

```bash
git archive --output=rutas.txt --format=zip HEAD
git count-objects -vH
```

En esta forma, `rutas.txt` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--worktree-attributes`

Lee área de trabajo attributes como parte de la entrada de `git archive`. En Git 2.51.1, la ayuda corta expresa el contrato como `read .gitattributes in working directory`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git archive --worktree-attributes --format=zip --output=entrega.zip HEAD
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--remote`

Obtiene remote desde el origen indicado para esta invocación. En Git 2.51.1, la ayuda corta expresa el contrato como `retrieve the archive from remote repository <repo>`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git archive --remote=valor --format=zip --output=entrega.zip HEAD
git count-objects -vH
```

### `--exec`

Define exec con el valor que recibe la opción.

```bash
git archive --exec=status --format=zip --output=entrega.zip HEAD
git count-objects -vH
```

El ejemplo usa `status` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--add-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git archive` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git archive --add-file=rutas.txt --format=zip --output=entrega.zip HEAD
git count-objects -vH
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--add-virtual-file`

Selecciona un archivo de entrada o salida según la posición indicada en la sintaxis.

La opción cambia cómo `git archive` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git archive --add-virtual-file=archivo.txt --format=zip --output=entrega.zip HEAD
git count-objects -vH
```

El ejemplo usa `archivo.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git archive --verbose --format=zip --output=entrega.zip HEAD
git count-objects -vH
```

 La salida permite comprobar objetos sueltos, packs y espacio registrado.

### `--mtime`

Define mtime para esta ejecución de `git archive`. En Git 2.51.1, la ayuda corta expresa el contrato como `set modification time of archive entries`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git archive --mtime=2026-01-15T10:00:00Z --format=zip --output=entrega.zip HEAD
git count-objects -vH
```

El ejemplo usa `2026-01-15T10:00:00Z` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La salida permite comprobar objetos sueltos, packs y espacio registrado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git backfill`](../administration/backfill.md)
- [`git clean`](../administration/clean.md)

## Fuente

- [git-archive - Create an archive of files from a named tree](https://git-scm.com/docs/git-archive)
