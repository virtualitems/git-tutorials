---
title: "git checkout-index"
source: "https://git-scm.com/docs/git-checkout-index"
section: "plumbing-write"
---

# `git checkout-index`

## Ejemplo de partida

```bash
mkdir exportado
git checkout-index --all --prefix=exportado/
```

Este caso usa `git checkout-index` para copiar archivos del índice al área de trabajo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: copiar archivos del índice al área de trabajo.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git checkout-index [-u] [-q] [-a] [-f] [-n] [--prefix=<string>]
		   [--stage=<number>|all]
		   [--temp]
		   [--ignore-skip-worktree-bits]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git commit-graph`](../plumbing-write/commit-graph.md)
- [`git commit-tree`](../plumbing-write/commit-tree.md)

## Fuente

- [git-checkout-index - Copy files from the index to the working tree](https://git-scm.com/docs/git-checkout-index)
