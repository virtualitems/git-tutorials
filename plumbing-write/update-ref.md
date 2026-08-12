---
title: "git update-ref"
source: "https://git-scm.com/docs/git-update-ref"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git update-ref`

Este caso usa `git update-ref` para actualizar referencias con comprobaciones de valor anterior.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git update-ref refs/heads/prueba HEAD
git show-ref --verify refs/heads/prueba
```

La invocación `git update-ref refs/heads/prueba HEAD` ejecuta esta operación: actualizar referencias con comprobaciones de valor anterior. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git update-ref [-m <reason>] [--no-deref] -d <ref> [<old-oid>]
git update-ref [-m <reason>] [--no-deref] [--create-reflog] <ref> <new-oid> [<old-oid>]
git update-ref [-m <reason>] [--no-deref] --stdin [-z] [--batch-updates]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git update-ref [<options>] -d <refname> [<old-oid>]
   or: git update-ref [<options>]    <refname> <new-oid> [<old-oid>]
   or: git update-ref [<options>] --stdin [-z] [--batch-updates]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git update-ref -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-m`

Actualiza m como parte de actualizar referencias con comprobaciones de valor anterior. En Git 2.51.1, la ayuda corta expresa el contrato como `reason of the update`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-ref -m valor refs/heads/prueba HEAD
git fsck --no-progress
```

### `--no-deref`

Desactiva el comportamiento `deref` para esta invocación.

```bash
git update-ref --no-deref refs/heads/prueba HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-d`

Retira d del alcance que procesa `git update-ref`. En Git 2.51.1, la ayuda corta expresa el contrato como `delete the reference`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-ref -d refs/heads/prueba HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--create-reflog`

Permite crear o escribir el elemento seleccionado.

```bash
git update-ref --create-reflog refs/heads/prueba HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--stdin`

Lee registros o nombres desde la entrada estándar.

La opción cambia cómo `git update-ref` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-ref --stdin refs/heads/prueba HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-z`

Termina registros con NUL para evitar división por espacios o saltos de línea.

La opción cambia cómo `git update-ref` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

```bash
git update-ref -z refs/heads/prueba HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--batch-updates` y `-0`

Activa batch updates durante actualizar referencias con comprobaciones de valor anterior. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración. En Git 2.51.1, la ayuda corta expresa el contrato como `batch reference updates`. Conserva esa formulación al comparar el efecto entre versiones de Git.

La opción cambia cómo `git update-ref` recibe datos. Define el separador, la codificación y la ruta de entrada antes de ejecutarla. Los nombres con espacios o saltos de línea requieren una interfaz terminada en NUL cuando el comando la ofrece.

#### Ejemplo con `--batch-updates`

```bash
git update-ref --batch-updates refs/heads/prueba HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `--deref`

Selecciona la relación indicada por deref; la ayuda de Git la define respecto de otra forma equivalente u opuesta. En Git 2.51.1, la ayuda corta expresa el contrato como `opposite of --no-deref`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git update-ref --deref refs/heads/prueba HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git write-tree`](../plumbing-write/write-tree.md)
- [`git update-index`](../plumbing-write/update-index.md)
- [`git unpack-objects`](../plumbing-write/unpack-objects.md)

## Fuente

- [git-update-ref - Update the object name stored in a ref safely](https://git-scm.com/docs/git-update-ref)
