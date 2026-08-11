---
title: "git update-index"
source: "https://git-scm.com/docs/git-update-index"
section: "plumbing-write"
---

# `git update-index`

## Ejemplo de partida

```bash
git update-index --assume-unchanged config.local
git ls-files -v config.local
```

Este caso usa `git update-index` para modificar directamente entradas y bits del índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: modificar directamente entradas y bits del índice.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git update-index
	     [--add] [--remove | --force-remove] [--replace]
	     [--refresh] [-q] [--unmerged] [--ignore-missing]
	     [(--cacheinfo <mode>,<object>,<file>)…]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git update-ref`](../plumbing-write/update-ref.md)
- [`git unpack-objects`](../plumbing-write/unpack-objects.md)
- [`git write-tree`](../plumbing-write/write-tree.md)

## Fuente

- [git-update-index - Register file contents in the working tree to the index](https://git-scm.com/docs/git-update-index)
