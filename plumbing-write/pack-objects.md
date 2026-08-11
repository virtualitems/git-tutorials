---
title: "git pack-objects"
source: "https://git-scm.com/docs/git-pack-objects"
section: "plumbing-write"
---

# `git pack-objects`

## Ejemplo de partida

```bash
mkdir -p packs
git rev-list --objects --all | git pack-objects packs/pack
```

Este caso usa `git pack-objects` para crear un archivo pack a partir de objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: crear un archivo pack a partir de objetos.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git pack-objects [-q | --progress | --all-progress] [--all-progress-implied]
		   [--no-reuse-delta] [--delta-base-offset] [--non-empty]
		   [--local] [--incremental] [--window=<n>] [--depth=<n>]
		   [--revs [--unpacked | --all]] [--keep-pack=<pack-name>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git prune-packed`](../plumbing-write/prune-packed.md)
- [`git multi-pack-index`](../plumbing-write/multi-pack-index.md)
- [`git read-tree`](../plumbing-write/read-tree.md)

## Fuente

- [git-pack-objects - Create a packed archive of objects](https://git-scm.com/docs/git-pack-objects)
