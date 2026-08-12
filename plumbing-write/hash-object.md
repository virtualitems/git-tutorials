---
title: "git hash-object"
source: "https://git-scm.com/docs/git-hash-object"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git hash-object`

Este caso usa `git hash-object` para calcular el identificador de un objeto y guardarlo si se solicita.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
printf 'hola\n' | git hash-object --stdin
printf 'hola\n' | git hash-object -w --stdin
```

La invocación `git hash-object` ejecuta esta operación: calcular el identificador de un objeto y guardarlo si se solicita. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git hash-object [-t <type>] [-w] [--path=<file> | --no-filters]
		[--stdin [--literally]] [--] <file>…
git hash-object [-t <type>] [-w] --stdin-paths [--no-filters]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git hash-object [-t <type>] [-w] [--path=<file> | --no-filters]
                       [--stdin [--literally]] [--] <file>...
   or: git hash-object [-t <type>] [-w] --stdin-paths [--no-filters]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git hash-object -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-t`

Define t con el valor que recibe la opción. En Git 2.51.1, la ayuda corta expresa el contrato como `object type`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git hash-object -t commit
git fsck --no-progress
```

El ejemplo usa `commit` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-w`

Escribe o registra w como parte de calcular el identificador de un objeto y guardarlo si se solicita. En Git 2.51.1, la ayuda corta expresa el contrato como `write the object into the object database`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git hash-object -w
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--path`

Procesa ruta con la regla indicada por esta opción. En Git 2.51.1, la ayuda corta expresa el contrato como `process file as it were from this path`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git hash-object` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git hash-object --path=rutas.txt
git fsck --no-progress
```

El ejemplo usa `rutas.txt` como valor. Sustitúyelo por un valor del tipo que muestra la sintaxis de tu versión. Un valor numérico conserva su unidad y un nombre de referencia debe resolver antes de ejecutar la orden. La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-filters`

Desactiva el comportamiento `filters` para esta invocación.

```bash
git hash-object --no-filters
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git hash-object` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git hash-object --stdin
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--literally`

Crea literally como parte de calcular el identificador de un objeto y guardarlo si se solicita. En Git 2.51.1, la ayuda corta expresa el contrato como `just hash any random garbage to create corrupt objects for debugging Git`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git hash-object --literally
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin-paths`

Lee entrada estándar paths como parte de la entrada de `git hash-object`. En Git 2.51.1, la ayuda corta expresa el contrato como `read file names from stdin`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git hash-object` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git hash-object --stdin-paths
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--filters`

Selecciona la relación indicada por filters; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-filters`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git hash-object --filters
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git index-pack`](../plumbing-write/index-pack.md)
- [`git commit-tree`](../plumbing-write/commit-tree.md)
- [`git merge-file`](../plumbing-write/merge-file.md)

## Fuente

- [git-hash-object - Compute object ID and optionally create an object from a file](https://git-scm.com/docs/git-hash-object)
