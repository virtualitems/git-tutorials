---
title: "git log"
source: "https://git-scm.com/docs/git-log"
section: "inspection-and-comparison"
---

# `git log`

## Ejemplo de partida

```bash
git log --oneline --decorate --graph --all
```

Este caso usa `git log` para consultar commits con filtros y formatos de salida. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los estados u objetos que la consulta debe mostrar o comparar.
- Operación: consultar commits con filtros y formatos de salida.
- Comprobación: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Modelo mental

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Forma de referencia

```text
git log [<options>] [<revision-range>] [[--] <path>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

## Páginas relacionadas

- [`git range-diff`](../inspection-and-comparison/range-diff.md)
- [`git last-modified`](../inspection-and-comparison/last-modified.md)
- [`git shortlog`](../inspection-and-comparison/shortlog.md)

## Fuente

- [git-log - Show commit logs](https://git-scm.com/docs/git-log)
