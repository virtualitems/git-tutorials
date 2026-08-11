---
title: "git diff-index"
source: "https://git-scm.com/docs/git-diff-index"
section: "plumbing-read"
---

# `git diff-index`

## Ejemplo de partida

```bash
git diff-index --cached HEAD -- README.md
```

Este caso usa `git diff-index` para comparar un árbol con el índice o el área de trabajo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: comparar un árbol con el índice o el área de trabajo.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git diff-index [-m] [--cached] [--merge-base] [<common-diff-options>] <tree-ish> [<path>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git diff-pairs`](../plumbing-read/diff-pairs.md)
- [`git diff-files`](../plumbing-read/diff-files.md)
- [`git diff-tree`](../plumbing-read/diff-tree.md)

## Fuente

- [git-diff-index - Compare a tree to the working tree or index](https://git-scm.com/docs/git-diff-index)
