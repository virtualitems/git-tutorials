---
title: "git cat-file"
source: "https://git-scm.com/docs/git-cat-file"
section: "plumbing-read"
---

# `git cat-file`

## Ejemplo de partida

```bash
git cat-file -t HEAD
git cat-file -p HEAD^{tree}
```

Este caso usa `git cat-file` para consultar el tipo, tamaño o contenido de objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: consultar el tipo, tamaño o contenido de objetos.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git cat-file <type> <object>
git cat-file (-e | -p | -t | -s) <object>
git cat-file (--textconv | --filters)
	     [<rev>:<path|tree-ish> | --path=<path|tree-ish> <rev>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git cherry`](../plumbing-read/cherry.md)
- [`git diff-files`](../plumbing-read/diff-files.md)

## Fuente

- [git-cat-file - Provide contents or details of repository objects](https://git-scm.com/docs/git-cat-file)
