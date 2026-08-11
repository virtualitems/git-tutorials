---
title: "git show-index"
source: "https://git-scm.com/docs/git-show-index"
section: "plumbing-read"
---

# `git show-index`

## Ejemplo de partida

```bash
git show-index < .git/objects/pack/pack-ejemplo.idx
```

Este caso usa `git show-index` para leer la tabla de objetos de un índice de pack. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: leer la tabla de objetos de un índice de pack.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git show-index [--object-format=<hash-algorithm>] < <pack-idx-file>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git show-ref`](../plumbing-read/show-ref.md)
- [`git rev-parse`](../plumbing-read/rev-parse.md)
- [`git unpack-file`](../plumbing-read/unpack-file.md)

## Fuente

- [git-show-index - Show packed archive index](https://git-scm.com/docs/git-show-index)
