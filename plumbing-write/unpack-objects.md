---
title: "git unpack-objects"
source: "https://git-scm.com/docs/git-unpack-objects"
section: "plumbing-write"
---

# `git unpack-objects`

## Ejemplo de partida

```bash
git unpack-objects < paquete.pack
```

Este caso usa `git unpack-objects` para extraer objetos de un flujo pack. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: extraer objetos de un flujo pack.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git unpack-objects [-n] [-q] [-r] [--strict]
```

Los corchetes delimitan partes opcionales.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git update-index`](../plumbing-write/update-index.md)
- [`git symbolic-ref`](../plumbing-write/symbolic-ref.md)
- [`git update-ref`](../plumbing-write/update-ref.md)

## Fuente

- [git-unpack-objects - Unpack objects from a packed archive](https://git-scm.com/docs/git-unpack-objects)
