---
title: "git merge-index"
source: "https://git-scm.com/docs/git-merge-index"
section: "plumbing-write"
---

# `git merge-index`

## Ejemplo de partida

```bash
git merge-index git-merge-one-file -a
```

Este caso usa `git merge-index` para ejecutar un programa de fusión para entradas sin resolver. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: ejecutar un programa de fusión para entradas sin resolver.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git merge-index [-o] [-q] <merge-program> (-a | ( [--] <file>…) )
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git mktag`](../plumbing-write/mktag.md)
- [`git merge-file`](../plumbing-write/merge-file.md)
- [`git mktree`](../plumbing-write/mktree.md)

## Fuente

- [git-merge-index - Run a merge for files needing merging](https://git-scm.com/docs/git-merge-index)
