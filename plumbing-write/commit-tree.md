---
title: "git commit-tree"
source: "https://git-scm.com/docs/git-commit-tree"
section: "plumbing-write"
---

# `git commit-tree`

## Ejemplo de partida

```bash
arbol=$(git write-tree)
commit=$(printf '%s\n' 'Commit de práctica' | git commit-tree "$arbol" -p HEAD)
printf '%s\n' "$commit"
```

Este caso usa `git commit-tree` para crear un objeto commit a partir de un árbol y sus padres. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: crear un objeto commit a partir de un árbol y sus padres.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git commit-tree <tree> [(-p <parent>)…]
git commit-tree [(-p <parent>)…] [-S[<keyid>]] [(-m <message>)…]
		  [(-F <file>)…] <tree>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git hash-object`](../plumbing-write/hash-object.md)
- [`git commit-graph`](../plumbing-write/commit-graph.md)
- [`git index-pack`](../plumbing-write/index-pack.md)

## Fuente

- [git-commit-tree - Create a new commit object](https://git-scm.com/docs/git-commit-tree)
