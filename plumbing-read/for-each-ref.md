---
title: "git for-each-ref"
source: "https://git-scm.com/docs/git-for-each-ref"
section: "plumbing-read"
---

# `git for-each-ref`

## Ejemplo de partida

```bash
git for-each-ref --sort=-committerdate --format='%(refname:short) %(objectname:short)' refs/heads/
```

Este caso usa `git for-each-ref` para filtrar, ordenar y formatear referencias. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: filtrar, ordenar y formatear referencias.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git for-each-ref [--count=<count>] [--shell|--perl|--python|--tcl]
		   [(--sort=<key>)…] [--format=<format>]
		   [--include-root-refs] [--points-at=<object>]
		   [--merged[=<object>]] [--no-merged[=<object>]]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git for-each-repo`](../plumbing-read/for-each-repo.md)
- [`git diff-tree`](../plumbing-read/diff-tree.md)
- [`git format-rev`](../plumbing-read/format-rev.md)

## Fuente

- [git-for-each-ref - Output information on each ref](https://git-scm.com/docs/git-for-each-ref)
