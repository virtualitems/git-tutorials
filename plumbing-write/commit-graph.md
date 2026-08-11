---
title: "git commit-graph"
source: "https://git-scm.com/docs/git-commit-graph"
section: "plumbing-write"
---

# `git commit-graph`

## Ejemplo de partida

```bash
git commit-graph write --reachable
git commit-graph verify
```

Este caso usa `git commit-graph` para escribir y verificar el archivo que acelera recorridos de commits. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: escribir y verificar el archivo que acelera recorridos de commits.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git commit-graph verify [--object-dir <dir>] [--shallow] [--[no-]progress]
git commit-graph write [--object-dir <dir>] [--append]
			[--split[=<strategy>]] [--reachable | --stdin-packs | --stdin-commits]
			[--changed-paths] [--[no-]max-new-filters <n>] [--[no-]progress]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git commit-tree`](../plumbing-write/commit-tree.md)
- [`git checkout-index`](../plumbing-write/checkout-index.md)
- [`git hash-object`](../plumbing-write/hash-object.md)

## Fuente

- [git-commit-graph - Write and verify Git commit-graph files](https://git-scm.com/docs/git-commit-graph)
