---
title: "git index-pack"
source: "https://git-scm.com/docs/git-index-pack"
section: "plumbing-write"
---

# `git index-pack`

## Ejemplo de partida

```bash
git index-pack paquete.pack
```

Este caso usa `git index-pack` para crear un índice para un pack y comprobar sus objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: crear un índice para un pack y comprobar sus objetos.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git index-pack [-v] [-o <index-file>] [--[no-]rev-index] <pack-file>
git index-pack --stdin [--fix-thin] [--keep] [-v] [-o <index-file>]
		  [--[no-]rev-index] [<pack-file>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git merge-file`](../plumbing-write/merge-file.md)
- [`git hash-object`](../plumbing-write/hash-object.md)
- [`git merge-index`](../plumbing-write/merge-index.md)

## Fuente

- [git-index-pack - Build pack index file for an existing packed archive](https://git-scm.com/docs/git-index-pack)
