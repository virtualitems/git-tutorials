---
title: "git mktree"
source: "https://git-scm.com/docs/git-mktree"
section: "plumbing-write"
---

# `git mktree`

## Ejemplo de partida

```bash
git ls-tree HEAD | git mktree
```

Este caso usa `git mktree` para crear un objeto árbol a partir de una lista de entradas. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: crear un objeto árbol a partir de una lista de entradas.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git mktree [-z] [--missing] [--batch]
```

Los corchetes delimitan partes opcionales.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git multi-pack-index`](../plumbing-write/multi-pack-index.md)
- [`git mktag`](../plumbing-write/mktag.md)
- [`git pack-objects`](../plumbing-write/pack-objects.md)

## Fuente

- [git-mktree - Build a tree-object from ls-tree formatted text](https://git-scm.com/docs/git-mktree)
