---
title: "git merge-base"
source: "https://git-scm.com/docs/git-merge-base"
section: "plumbing-read"
---

# `git merge-base`

## Ejemplo de partida

```bash
base=$(git merge-base main tema-portada)
git show --oneline --no-patch "$base"
```

Este caso usa `git merge-base` para calcular ancestros comunes para una fusión. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: objetos, referencias, árboles o entradas del índice que debe leer la consulta.
- Operación: calcular ancestros comunes para una fusión.
- Comprobación: la salida estructurada puede compararse o pasar a otro proceso sin alterar el repositorio.

## Modelo mental

La salida expone datos internos para inspección o scripts. Los formatos explícitos y los separadores NUL evitan ambigüedad cuando los nombres contienen espacios o saltos de línea.

Fija el formato de salida que consumirá el siguiente proceso. Usa separadores NUL cuando una ruta pueda contener caracteres que también actúan como separadores de texto.

## Forma de referencia

```text
git merge-base [-a | --all] <commit> <commit>…
git merge-base [-a | --all] --octopus <commit>…
git merge-base --is-ancestor <commit> <commit>
git merge-base --independent <commit>…
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prueba con nombres que contengan espacios. Si el comando ofrece `-z`, procesa la salida por bytes y conserva los separadores NUL.

## Páginas relacionadas

- [`git name-rev`](../plumbing-read/name-rev.md)
- [`git ls-tree`](../plumbing-read/ls-tree.md)
- [`git pack-redundant`](../plumbing-read/pack-redundant.md)

## Fuente

- [git-merge-base - Find as good common ancestors as possible for a merge](https://git-scm.com/docs/git-merge-base)
