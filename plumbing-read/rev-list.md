---
title: "git rev-list"
source: "https://git-scm.com/docs/git-rev-list"
section: "plumbing-read"
---

# `git rev-list`

## Ejemplo de partida

```bash
git rev-list --count main
git rev-list main --not origin/main
```

Este caso usa `git rev-list` para enumerar commits alcanzables según límites y filtros. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: enumerar commits alcanzables según límites y filtros.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git rev-list [<options>] <commit>… [--] [<path>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git rev-parse`](../plumbing-read/rev-parse.md)
- [`git repo`](../plumbing-read/repo.md)
- [`git show-index`](../plumbing-read/show-index.md)

## Fuente

- [git-rev-list - Lists commit objects in reverse chronological order](https://git-scm.com/docs/git-rev-list)
