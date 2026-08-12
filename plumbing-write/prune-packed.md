---
title: "git prune-packed"
source: "https://git-scm.com/docs/git-prune-packed"
section: "plumbing-write"
status: "source-audited"
version: "2.55.0"
---

# `git prune-packed`

Este caso usa `git prune-packed` para eliminar objetos sueltos que ya existen dentro de packs.

## Preparación

Usa el [laboratorio base](../getting-and-creating-projects/init.md#laboratorio-base) para las operaciones que necesitan un repositorio. Consulta las [convenciones de la CLI](../guides/gitcli.md) antes de combinar opciones, revisiones y rutas.

## Cómo funciona

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Ejemplo mínimo

```bash
git prune-packed --dry-run
```

La invocación `git prune-packed --dry-run` ejecuta esta operación: eliminar objetos sueltos que ya existen dentro de packs. Después, `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Sintaxis y formas de invocación

```text
git prune-packed [-n | --dry-run] [-q | --quiet]
```

### Ayuda corta de la instalación de prueba (`git 2.51.1`)

```text
git prune-packed [-n | --dry-run] [-q | --quiet]
```

Los corchetes indican elementos opcionales; `<valor>` exige sustitución; los puntos suspensivos permiten repetición; `|` separa formas excluyentes. Usa `git prune-packed -h` para consultar la sintaxis que corresponde a la instalación donde ejecutarás la orden.

## Opciones

Las [convenciones de la CLI](../guides/gitcli.md) explican alias, valores, negación, opciones interactivas y códigos de terminación. Cada apartado muestra el comportamiento específico de esta orden.

### `-n` y `--dry-run`

Calcula el alcance y muestra lo que ocurriría sin aplicar el cambio.

#### Ejemplo con `--dry-run`

```bash
git prune-packed --dry-run
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

### `-q` y `--quiet`

Reduce mensajes que no representan errores.

#### Ejemplo con `--quiet`

```bash
git prune-packed --quiet --dry-run
git fsck --no-progress
```

 La comprobación detecta objetos o enlaces que no cumplen el formato esperado.

## Páginas relacionadas

- [`git read-tree`](../plumbing-write/read-tree.md)
- [`git pack-objects`](../plumbing-write/pack-objects.md)
- [`git symbolic-ref`](../plumbing-write/symbolic-ref.md)

## Fuente

- [git-prune-packed - Remove extra objects that are already in pack files](https://git-scm.com/docs/git-prune-packed)
