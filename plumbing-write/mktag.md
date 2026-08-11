---
title: "git mktag"
source: "https://git-scm.com/docs/git-mktag"
section: "plumbing-write"
---

# `git mktag`

## Ejemplo de partida

```bash
git cat-file tag v1.0 > etiqueta.txt
git mktag < etiqueta.txt
```

Este caso usa `git mktag` para validar y crear un objeto de etiqueta anotada. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: identificadores, entradas del índice o referencias validadas por el script.
- Operación: validar y crear un objeto de etiqueta anotada.
- Comprobación: `git cat-file`, `git ls-files --stage` o `git show-ref` comprueban el dato escrito.

## Modelo mental

Los comandos de plomería operan sobre índice, objetos o referencias sin aplicar todas las decisiones de los comandos de usuario. Un script debe validar entradas y estado antes de escribir.

Valida el identificador anterior y el tipo de objeto antes de escribir. Esa comprobación evita actualizar el repositorio desde un estado que otro proceso ya cambió.

## Forma de referencia

```text
git mktag
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Usa un repositorio temporal y guarda los identificadores antes de escribir. Verifica cada objeto con `git cat-file` y cada referencia con `git show-ref`.

## Páginas relacionadas

- [`git mktree`](../plumbing-write/mktree.md)
- [`git merge-index`](../plumbing-write/merge-index.md)
- [`git multi-pack-index`](../plumbing-write/multi-pack-index.md)

## Fuente

- [git-mktag - Creates a tag object with extra validation](https://git-scm.com/docs/git-mktag)
