---
title: "git symbolic-ref"
source: "https://git-scm.com/docs/git-symbolic-ref"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git symbolic-ref`

Este caso usa `git symbolic-ref` para leer o cambiar una referencia simbólica.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git symbolic-ref HEAD
git symbolic-ref refs/heads/actual
```

La invocación `git symbolic-ref HEAD` ejecuta esta operación: leer o cambiar una referencia simbólica. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git symbolic-ref [-m <reason>] <name> <ref>
git symbolic-ref [-q] [--short] [--no-recurse] <name>
git symbolic-ref --delete [-q] <name>
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git symbolic-ref [-m <reason>] <name> <ref>
   or: git symbolic-ref [-q] [--short] [--no-recurse] <name>
   or: git symbolic-ref --delete [-q] <name>
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git symbolic-ref -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-m`

Actualiza m como parte de leer o cambiar una referencia simbólica. En Git 2.51.1, la ayuda corta expresa el contrato como `reason of the update`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git symbolic-ref -m valor HEAD
git fsck --no-progress
```

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git symbolic-ref --quiet HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `--short`

Incluye short en la salida o cambia cómo `git symbolic-ref` la representa. En Git 2.51.1, la ayuda corta expresa el contrato como `shorten ref output`. Conserva esa formulación al comparar el efecto entre versiones de Git.

```bash
git symbolic-ref --short HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--no-recurse`

Desactiva el comportamiento `recurse` para esta invocación.

```bash
git symbolic-ref --no-recurse HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `--delete` y `-d`

Elimina el elemento seleccionado.

#### Ejemplo con `--delete`

```bash
git symbolic-ref --delete HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `--recurse`

Extiende la operación de forma recursiva al ámbito documentado.

```bash
git symbolic-ref --recurse HEAD
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git unpack-objects`](../plumbing-write/unpack-objects.md)
- [`git read-tree`](../plumbing-write/read-tree.md)
- [`git update-index`](../plumbing-write/update-index.md)

## Fuente

- [git-symbolic-ref - Read, modify and delete symbolic refs](https://git-scm.com/docs/git-symbolic-ref)
