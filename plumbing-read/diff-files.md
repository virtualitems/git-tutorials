---
title: "git diff-files"
source: "https://git-scm.com/docs/git-diff-files"
section: "plumbing-read"
---

# `git diff-files`

## Ejemplo de partida

```bash
git diff-files -- README.md
```

Este caso usa `git diff-files` para comparar el área de trabajo con el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: comparar el área de trabajo con el índice.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git diff-files [-q] [-0 | -1 | -2 | -3 | -c | --cc] [<common-diff-options>] [<path>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git diff-index`](../plumbing-read/diff-index.md)
- [`git cherry`](../plumbing-read/cherry.md)
- [`git diff-pairs`](../plumbing-read/diff-pairs.md)

## Fuente

- [git-diff-files - Compares files in the working tree and the index](https://git-scm.com/docs/git-diff-files)
