---
title: "git pack-redundant"
source: "https://git-scm.com/docs/git-pack-redundant"
section: "plumbing-read"
---

# `git pack-redundant`

## Ejemplo de partida

```bash
git pack-redundant --all
```

Este caso usa `git pack-redundant` para detectar packs cuyo contenido ya está cubierto por otros packs. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: detectar packs cuyo contenido ya está cubierto por otros packs.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git pack-redundant [--verbose] [--alt-odb] (--all | <pack-filename>…)
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git repo`](../plumbing-read/repo.md)
- [`git name-rev`](../plumbing-read/name-rev.md)
- [`git rev-list`](../plumbing-read/rev-list.md)

## Fuente

- [git-pack-redundant - Find redundant pack files](https://git-scm.com/docs/git-pack-redundant)
