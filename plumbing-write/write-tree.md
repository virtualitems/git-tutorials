---
title: "git write-tree"
source: "https://git-scm.com/docs/git-write-tree"
section: "plumbing-write"
---

# `git write-tree`

## Ejemplo de partida

```bash
git add README.md
arbol=$(git write-tree)
git cat-file -t "$arbol"
```

Este caso usa `git write-tree` para crear un objeto árbol a partir del índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: crear un objeto árbol a partir del índice.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git write-tree [--missing-ok] [--prefix=<prefix>/]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git update-ref`](../plumbing-write/update-ref.md)
- [`git update-index`](../plumbing-write/update-index.md)

## Fuente

- [git-write-tree - Create a tree object from the current index](https://git-scm.com/docs/git-write-tree)
