---
title: "git multi-pack-index"
source: "https://git-scm.com/docs/git-multi-pack-index"
section: "plumbing-write"
---

# `git multi-pack-index`

## Ejemplo de partida

```bash
git multi-pack-index write
git multi-pack-index verify
```

Este caso usa `git multi-pack-index` para administrar un índice que cubre varios archivos pack. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: administrar un índice que cubre varios archivos pack.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git multi-pack-index [<options>] write [--preferred-pack=<pack>]
		         [--[no-]bitmap] [--[no-]incremental] [--[no-]stdin-packs]
		         [--refs-snapshot=<path>] [--[no-]write-chain-file]
			 [--base=<checksum>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git pack-objects`](../plumbing-write/pack-objects.md)
- [`git mktree`](../plumbing-write/mktree.md)
- [`git prune-packed`](../plumbing-write/prune-packed.md)

## Fuente

- [git-multi-pack-index - Write and verify multi-pack-indexes](https://git-scm.com/docs/git-multi-pack-index)
