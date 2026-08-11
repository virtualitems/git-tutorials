---
title: "git ls-files"
source: "https://git-scm.com/docs/git-ls-files"
section: "plumbing-read"
---

# `git ls-files`

## Ejemplo de partida

```bash
git ls-files --stage
git ls-files --others --exclude-standard
```

Este caso usa `git ls-files` para enumerar entradas del índice y su relación con el área de trabajo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: enumerar entradas del índice y su relación con el área de trabajo.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git ls-files [-z] [-t] [-v] [-f]
		[-c|--cached] [-d|--deleted] [-o|--others] [-i|--ignored]
		[-s|--stage] [-u|--unmerged] [-k|--killed] [-m|--modified]
		[--resolve-undo]
# …
```

Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git ls-tree`](../plumbing-read/ls-tree.md)
- [`git get-tar-commit-id`](../plumbing-read/get-tar-commit-id.md)
- [`git merge-base`](../plumbing-read/merge-base.md)

## Fuente

- [git-ls-files - Show information about files in the index and the working tree](https://git-scm.com/docs/git-ls-files)
