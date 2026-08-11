---
title: "git hash-object"
source: "https://git-scm.com/docs/git-hash-object"
section: "plumbing-write"
---

# `git hash-object`

## Ejemplo de partida

```bash
printf 'hola\n' | git hash-object --stdin
printf 'hola\n' | git hash-object -w --stdin
```

Este caso usa `git hash-object` para calcular el identificador de un objeto y guardarlo si se solicita. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: calcular el identificador de un objeto y guardarlo si se solicita.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git hash-object [-t <type>] [-w] [--path=<file> | --no-filters]
		[--stdin [--literally]] [--] <file>…
git hash-object [-t <type>] [-w] --stdin-paths [--no-filters]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git index-pack`](../plumbing-write/index-pack.md)
- [`git commit-tree`](../plumbing-write/commit-tree.md)
- [`git merge-file`](../plumbing-write/merge-file.md)

## Fuente

- [git-hash-object - Compute object ID and optionally create an object from a file](https://git-scm.com/docs/git-hash-object)
