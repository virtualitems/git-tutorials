---
title: "git show-branch"
source: "https://git-scm.com/docs/git-show-branch"
section: "inspection-and-comparison"
---

# `git show-branch`

## Ejemplo de partida

```bash
git show-branch main tema-portada
```

Este caso usa `git show-branch` para comparar el desarrollo representado por varias ramas. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los estados u objetos que la consulta debe mostrar o comparar.
- Operación: comparar el desarrollo representado por varias ramas.
- Comprobación: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Modelo mental

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Forma de referencia

```text
git show-branch [-a | --all] [-r | --remotes] [--topo-order | --date-order]
		[--current] [--color[=<when>] | --no-color] [--sparse]
		[--more=<n> | --list | --independent | --merge-base]
		[--no-name | --sha1-name] [--topics]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

## Páginas relacionadas

- [`git verify-commit`](../inspection-and-comparison/verify-commit.md)
- [`git show`](../inspection-and-comparison/show.md)
- [`git verify-tag`](../inspection-and-comparison/verify-tag.md)

## Fuente

- [git-show-branch - Show branches and their commits](https://git-scm.com/docs/git-show-branch)
