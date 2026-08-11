---
title: "git read-tree"
source: "https://git-scm.com/docs/git-read-tree"
section: "plumbing-write"
---

# `git read-tree`

## Ejemplo de partida

```bash
git read-tree HEAD
git ls-files --stage
```

Este caso usa `git read-tree` para cargar información de árboles en el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: cargar información de árboles en el índice.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git read-tree [(-m [--trivial] [--aggressive] | --reset | --prefix=<prefix>)
		[-u | -i]] [--index-output=<file>] [--no-sparse-checkout]
		(--empty | <tree-ish1> [<tree-ish2> [<tree-ish3>]])
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git symbolic-ref`](../plumbing-write/symbolic-ref.md)
- [`git prune-packed`](../plumbing-write/prune-packed.md)
- [`git unpack-objects`](../plumbing-write/unpack-objects.md)

## Fuente

- [git-read-tree - Reads tree information into the index](https://git-scm.com/docs/git-read-tree)
