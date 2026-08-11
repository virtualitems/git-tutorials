---
title: "git diff-tree"
source: "https://git-scm.com/docs/git-diff-tree"
section: "plumbing-read"
---

# `git diff-tree`

## Ejemplo de partida

```bash
git diff-tree --no-commit-id --name-status -r HEAD
```

Este caso usa `git diff-tree` para comparar los blobs y modos de dos árboles. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: comparar los blobs y modos de dos árboles.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git diff-tree [--stdin] [-m] [-s] [-v] [--no-commit-id] [--pretty]
	      [-t] [-r] [-c | --cc] [--combined-all-paths] [--root] [--merge-base]
	      [<common-diff-options>] <tree-ish> [<tree-ish>] [<path>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git for-each-ref`](../plumbing-read/for-each-ref.md)
- [`git diff-pairs`](../plumbing-read/diff-pairs.md)
- [`git for-each-repo`](../plumbing-read/for-each-repo.md)

## Fuente

- [git-diff-tree - Compares the content and mode of blobs found via two tree objects](https://git-scm.com/docs/git-diff-tree)
