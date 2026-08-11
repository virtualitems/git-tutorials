---
title: "git prune-packed"
source: "https://git-scm.com/docs/git-prune-packed"
section: "plumbing-write"
---

# `git prune-packed`

## Ejemplo de partida

```bash
git prune-packed --dry-run
```

Este caso usa `git prune-packed` para eliminar objetos sueltos que ya existen dentro de packs. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: eliminar objetos sueltos que ya existen dentro de packs.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git prune-packed [-n | --dry-run] [-q | --quiet]
```

Los corchetes delimitan partes opcionales.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git read-tree`](../plumbing-write/read-tree.md)
- [`git pack-objects`](../plumbing-write/pack-objects.md)
- [`git symbolic-ref`](../plumbing-write/symbolic-ref.md)

## Fuente

- [git-prune-packed - Remove extra objects that are already in pack files](https://git-scm.com/docs/git-prune-packed)
