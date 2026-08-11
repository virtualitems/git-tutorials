---
title: "git symbolic-ref"
source: "https://git-scm.com/docs/git-symbolic-ref"
section: "plumbing-write"
---

# `git symbolic-ref`

## Ejemplo de partida

```bash
git symbolic-ref HEAD
git symbolic-ref refs/heads/actual
```

Este caso usa `git symbolic-ref` para leer o cambiar una referencia simbólica. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: leer o cambiar una referencia simbólica.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git symbolic-ref [-m <reason>] <name> <ref>
git symbolic-ref [-q] [--short] [--no-recurse] <name>
git symbolic-ref --delete [-q] <name>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git unpack-objects`](../plumbing-write/unpack-objects.md)
- [`git read-tree`](../plumbing-write/read-tree.md)
- [`git update-index`](../plumbing-write/update-index.md)

## Fuente

- [git-symbolic-ref - Read, modify and delete symbolic refs](https://git-scm.com/docs/git-symbolic-ref)
