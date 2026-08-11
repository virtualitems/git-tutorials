---
title: "git rev-parse"
source: "https://git-scm.com/docs/git-rev-parse"
section: "plumbing-read"
---

# `git rev-parse`

## Ejemplo de partida

```bash
git rev-parse --show-toplevel
git rev-parse HEAD^{tree}
```

Este caso usa `git rev-parse` para resolver revisiones y separar opciones para scripts. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: resolver revisiones y separar opciones para scripts.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git rev-parse [<options>] <arg>…
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git show-index`](../plumbing-read/show-index.md)
- [`git rev-list`](../plumbing-read/rev-list.md)
- [`git show-ref`](../plumbing-read/show-ref.md)

## Fuente

- [git-rev-parse - Pick out and massage parameters](https://git-scm.com/docs/git-rev-parse)
