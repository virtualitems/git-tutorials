---
title: "git range-diff"
source: "https://git-scm.com/docs/git-range-diff"
section: "inspection-and-comparison"
---

# `git range-diff`

## Ejemplo de partida

```bash
git range-diff main..tema-v1 main..tema-v2
```

Este caso usa `git range-diff` para comparar dos versiones de una serie de commits. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los estados u objetos que la consulta debe mostrar o comparar.
- Operación: comparar dos versiones de una serie de commits.
- Comprobación: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Modelo mental

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Forma de referencia

```text
git range-diff [--color=[<when>]] [--no-color] [<diff-options>]
	[--no-dual-color] [--creation-factor=<factor>]
	[--left-only | --right-only] [--diff-merges=<format>]
	[--remerge-diff] [--no-notes | --notes[=<ref>]]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

## Páginas relacionadas

- [`git shortlog`](../inspection-and-comparison/shortlog.md)
- [`git log`](../inspection-and-comparison/log.md)
- [`git show`](../inspection-and-comparison/show.md)

## Fuente

- [git-range-diff - Compare two commit ranges (e.g. two versions of a branch)](https://git-scm.com/docs/git-range-diff)
