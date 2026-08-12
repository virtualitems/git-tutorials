---
title: "git status"
source: "https://git-scm.com/docs/git-status"
section: "basic-snapshotting"
status: "source-audited"
version: "2.55.0"
---

# `git status`

Este caso usa `git status` para comparar el área de trabajo y el índice con el commit actual.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Ejemplo mínimo

```bash
git status --short --branch
```

La invocación `git status --short --branch` ejecuta esta operación: comparar el área de trabajo y el índice con el commit actual. Después, `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Sintaxis y formas de invocación

```text
git status [<options>] [--] [<pathspec>…]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git status [<options>] [--] [<pathspec>...]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git status -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-v` y `--verbose`

Aumenta el detalle enviado a la salida.

#### Ejemplo con `--verbose`

```bash
git status --verbose --short --branch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-s` y `--short`

Incluye short en la salida o cambia cómo `git status` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show status concisely`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--short`

```bash
git status --short --branch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-b` y `--branch`

Selecciona o modifica referencias dentro del alcance de la orden.

#### Ejemplo con `--branch`

```bash
git status --branch --short
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--show-stash`

Incluye información adicional en la salida.

```bash
git status --show-stash --short --branch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ahead-behind`

Calcula cuántos commits separan una rama de su upstream. En Git 2.51.1, la ayuda corta expresa el contrato como `compute full ahead/behind values`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git status --ahead-behind --short --branch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--porcelain`

Produce un contrato de salida destinado a scripts.

```bash
git status --porcelain=valor --short --branch
git status --short
```

### `--long`

Incluye long en la salida o cambia cómo `git status` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `show status in long format (default)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git status --long --short --branch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z` y `--null`

Usa NUL como terminador para conservar cualquier byte válido de un nombre.

#### Ejemplo con `--null`

```bash
git status --null --short --branch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `-u` y `--untracked-files`

Define cuánto detalle muestra Git sobre archivos que todavía no están en el índice. En Git 2.51.1, la ayuda corta expresa el contrato como `show untracked files, optional modes: all, normal, no. (Default: all)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--untracked-files`

```bash
git status --untracked-files=all --short --branch
git status --short
```

En esta forma, `all` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--ignored`

Incluye archivos ignorados en la vista solicitada. En Git 2.51.1, la ayuda corta expresa el contrato como `show ignored files, optional modes: traditional, matching, no. (Default: traditional)`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git status --ignored=all --short --branch
git status --short
```

El ejemplo usa `all` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ignore-submodules`

Excluye elementos que cumplan la condición indicada.

```bash
git status --ignore-submodules=always --short --branch
git status --short
```

El ejemplo usa `always` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--column`

Incluye column en la salida o cambia cómo `git status` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `list untracked files in columns`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git status` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git status --column=short --short --branch
git status --short
```

El ejemplo usa `short` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-renames`

Desactiva el comportamiento `renames` para esta invocación.

La opción selecciona el procedimiento que `git status` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git status --no-renames --short --branch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--renames`

Controla detección o búsqueda de relaciones entre entradas.

La opción selecciona el procedimiento que `git status` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git status --renames --short --branch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-M` y `--find-renames`

Controla detección o búsqueda de relaciones entre entradas.

#### Ejemplo con `--find-renames`

```bash
git status --find-renames=5 --short --branch
git status --short
```

En esta forma, `5` es un valor de ejemplo. Sustitúyelo por un valor que cumpla el tipo y el alcance indicados por la sintaxis. El estado muestra si cambió el área de trabajo, el índice o la operación en curso.

### `--no-ahead-behind`

Desactiva para esta invocación el comportamiento que habilita `--ahead-behind`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

```bash
git status --no-ahead-behind --short --branch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-column`

Desactiva para esta invocación el comportamiento que habilita `--column`. Mantén iguales los demás argumentos y compara el resultado con la forma positiva para comprobar la diferencia.

La opción cambia cómo `git status` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git status --no-column --short --branch
git status --short
```

El estado muestra si cambió el área de trabajo, el índice o la operación en curso. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git rm`](../basic-snapshotting/rm.md)
- [`git restore`](../basic-snapshotting/restore.md)

## Fuente

- [git-status - Show the working tree status](https://git-scm.com/docs/git-status)
