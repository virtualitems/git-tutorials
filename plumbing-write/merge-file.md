---
title: "git merge-file"
source: "https://git-scm.com/docs/git-merge-file"
section: "plumbing-write"
---

# `git merge-file`

## Ejemplo de partida

```bash
git merge-file actual.txt base.txt otra.txt
```

Este caso usa `git merge-file` para fusionar tres versiones de un archivo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: fusionar tres versiones de un archivo.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git merge-file [-L <current-name> [-L <base-name> [-L <other-name>]]]
	[--ours|--theirs|--union] [-p|--stdout] [-q|--quiet] [--marker-size=<n>]
	[--[no-]diff3] [--object-id] <current> <base> <other>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git merge-index`](../plumbing-write/merge-index.md)
- [`git index-pack`](../plumbing-write/index-pack.md)
- [`git mktag`](../plumbing-write/mktag.md)

## Fuente

- [git-merge-file - Run a three-way file merge](https://git-scm.com/docs/git-merge-file)
