---
title: "git last-modified"
source: "https://git-scm.com/docs/git-last-modified"
section: "inspection-and-comparison"
---

# `git last-modified`

## Ejemplo de partida

```bash
git last-modified --recursive HEAD -- docs/
```

Este caso usa `git last-modified` para mostrar el commit que modificó por última vez cada ruta. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los estados u objetos que la consulta debe mostrar o comparar.
- Operación: mostrar el commit que modificó por última vez cada ruta.
- Comprobación: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Modelo mental

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Forma de referencia

```text
git last-modified [--recursive] [--show-trees] [--max-depth=<depth>] [-z]
		  [<revision-range>] [[--] <pathspec>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Condición que debes comprobar

La documentación marca este comando como experimental. Comprueba su disponibilidad en la versión instalada.

## Práctica

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

## Páginas relacionadas

- [`git log`](../inspection-and-comparison/log.md)
- [`git difftool`](../inspection-and-comparison/difftool.md)
- [`git range-diff`](../inspection-and-comparison/range-diff.md)

## Fuente

- [git-last-modified - EXPERIMENTAL: Show when files were last modified](https://git-scm.com/docs/git-last-modified)
