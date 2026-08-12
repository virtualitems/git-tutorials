---
title: "git merge-file"
source: "https://git-scm.com/docs/git-merge-file"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git merge-file`

Este caso usa `git merge-file` para fusionar tres versiones de un archivo.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git merge-file actual.txt base.txt otra.txt
```

La invocación `git merge-file actual.txt base.txt otra.txt` ejecuta esta operación: fusionar tres versiones de un archivo. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git merge-file [-L <current-name> [-L <base-name> [-L <other-name>]]]
	[--ours|--theirs|--union] [-p|--stdout] [-q|--quiet] [--marker-size=<n>]
	[--[no-]diff3] [--object-id] <current> <base> <other>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git merge-file [<options>] [-L <name1> [-L <orig> [-L <name2>]]] <file1> <orig-file> <file2>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git merge-file -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-L`

Define L para esta ejecución de `git merge-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `set labels for file1/orig-file/file2`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git merge-file` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git merge-file -L tema actual.txt base.txt otra.txt
git fsck --no-progress
```

El ejemplo usa `tema` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--ours`

Selecciona la versión de la etapa ours para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use our version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-file --ours actual.txt base.txt otra.txt
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--theirs`

Selecciona la versión de la etapa theirs para las rutas en conflicto. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use their version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-file --theirs actual.txt base.txt otra.txt
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--union`

Define union para esta ejecución de `git merge-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use a union version`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-file --union actual.txt base.txt otra.txt
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-p` y `--stdout`

Incluye salida estándar en la salida o cambia cómo `git merge-file` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `send results to standard output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

#### Ejemplo con `--stdout`

```bash
git merge-file --stdout actual.txt base.txt otra.txt
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git merge-file --quiet actual.txt base.txt otra.txt
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `--marker-size`

Define marker size para esta ejecución de `git merge-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `for conflicts, use this marker size`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-file --marker-size=5 actual.txt base.txt otra.txt
git fsck --no-progress
```

El ejemplo usa `5` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--diff3`

Define diff3 para esta ejecución de `git merge-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `use a diff3 based merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-file --diff3 actual.txt base.txt otra.txt
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--object-id`

Selecciona la representación o tratamiento de identificadores de objeto.

La opción cambia cómo `git merge-file` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git merge-file --object-id actual.txt base.txt otra.txt
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--zdiff3`

Define zdiff3 para esta ejecución de `git merge-file`. En Git 2.51.1, la ayuda corta expresa el contrato como `use a zealous diff3 based merge`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git merge-file --zdiff3 actual.txt base.txt otra.txt
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--diff-algorithm`

Selecciona el algoritmo o estrategia que procesa la entrada.

La opción selecciona el procedimiento que `git merge-file` aplica a la misma entrada. Mantén constantes las revisiones, rutas y archivos cuando compares el resultado con otra estrategia.

```bash
git merge-file --diff-algorithm=sha256 actual.txt base.txt otra.txt
git fsck --no-progress
```

El ejemplo usa `sha256` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git merge-index`](../plumbing-write/merge-index.md)
- [`git index-pack`](../plumbing-write/index-pack.md)
- [`git mktag`](../plumbing-write/mktag.md)

## Fuente

- [git-merge-file - Run a three-way file merge](https://git-scm.com/docs/git-merge-file)
