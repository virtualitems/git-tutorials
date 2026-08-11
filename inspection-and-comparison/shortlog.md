---
title: "git shortlog"
source: "https://git-scm.com/docs/git-shortlog"
section: "inspection-and-comparison"
---

# `git shortlog`

## Ejemplo de partida

```bash
git shortlog --summary --numbered --all
```

Este caso usa `git shortlog` para agrupar el historial por autor y resumir sus commits. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los estados u objetos que la consulta debe mostrar o comparar.
- Operación: agrupar el historial por autor y resumir sus commits.
- Comprobación: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Modelo mental

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Forma de referencia

```text
git shortlog [<options>] [<revision-range>] [[--] <path>…]
git log --pretty=short | git shortlog [<options>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

## Páginas relacionadas

- [`git show`](../inspection-and-comparison/show.md)
- [`git range-diff`](../inspection-and-comparison/range-diff.md)
- [`git show-branch`](../inspection-and-comparison/show-branch.md)

## Fuente

- [git-shortlog - Summarize git log output](https://git-scm.com/docs/git-shortlog)
