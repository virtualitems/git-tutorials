---
title: "git merge-index"
source: "https://git-scm.com/docs/git-merge-index"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git merge-index`

Este caso usa `git merge-index` para ejecutar un programa de fusión para entradas sin resolver.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git merge-index git-merge-one-file -a
```

La invocación `git merge-index git-merge-one-file -a` ejecuta esta operación: ejecutar un programa de fusión para entradas sin resolver. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git merge-index [-o] [-q] <merge-program> (-a | ( [--] <file>…) )
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git merge-index [-o] [-q] <merge-program> (-a | [--] [<filename>...])
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git merge-index -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-o`

Activa o durante ejecutar un programa de fusión para entradas sin resolver. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git merge-index -o git-merge-one-file -a
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-q`

Activa q durante ejecutar un programa de fusión para entradas sin resolver. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git merge-index -q git-merge-one-file -a
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

### `-a`

Activa a durante ejecutar un programa de fusión para entradas sin resolver. La opción afecta esta invocación y no cambia la configuración de otras órdenes salvo que la propia función escriba esa configuración.

```bash
git merge-index -a git-merge-one-file
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado. Ejecuta la comprobación inmediatamente después para que ningún comando intermedio cambie el estado que estás observando.

## Páginas relacionadas

- [`git mktag`](../plumbing-write/mktag.md)
- [`git merge-file`](../plumbing-write/merge-file.md)
- [`git mktree`](../plumbing-write/mktree.md)

## Fuente

- [git-merge-index - Run a merge for files needing merging](https://git-scm.com/docs/git-merge-index)
