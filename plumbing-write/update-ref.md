---
title: "git update-ref"
source: "https://git-scm.com/docs/git-update-ref"
section: "plumbing-write"
---

# `git update-ref`

## Ejemplo de partida

```bash
git update-ref refs/heads/prueba HEAD
git show-ref --verify refs/heads/prueba
```

Este caso usa `git update-ref` para actualizar referencias con comprobaciones de valor anterior. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: actualizar referencias con comprobaciones de valor anterior.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git update-ref [-m <reason>] [--no-deref] -d <ref> [<old-oid>]
git update-ref [-m <reason>] [--no-deref] [--create-reflog] <ref> <new-oid> [<old-oid>]
git update-ref [-m <reason>] [--no-deref] --stdin [-z] [--batch-updates]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Condición que debes comprobar

Actualizar una referencia cambia qué commit alcanza su nombre. Pasa el valor anterior cuando necesites detectar escrituras concurrentes.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git write-tree`](../plumbing-write/write-tree.md)
- [`git update-index`](../plumbing-write/update-index.md)
- [`git unpack-objects`](../plumbing-write/unpack-objects.md)

## Fuente

- [git-update-ref - Update the object name stored in a ref safely](https://git-scm.com/docs/git-update-ref)
