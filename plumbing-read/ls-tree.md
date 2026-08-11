---
title: "git ls-tree"
source: "https://git-scm.com/docs/git-ls-tree"
section: "plumbing-read"
---

# `git ls-tree`

## Ejemplo de partida

```bash
git ls-tree -r --name-only HEAD
```

Este caso usa `git ls-tree` para enumerar el contenido de un objeto árbol. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: enumerar el contenido de un objeto árbol.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git ls-tree [-d] [-r] [-t] [-l] [-z]
	    [--name-only] [--name-status] [--object-only] [--full-name] [--full-tree] [--abbrev[=<n>]] [--format=<format>]
	    <tree-ish> [<path>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git merge-base`](../plumbing-read/merge-base.md)
- [`git ls-files`](../plumbing-read/ls-files.md)
- [`git name-rev`](../plumbing-read/name-rev.md)

## Fuente

- [git-ls-tree - List the contents of a tree object](https://git-scm.com/docs/git-ls-tree)
