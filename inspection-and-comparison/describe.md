---
title: "git describe"
source: "https://git-scm.com/docs/git-describe"
section: "inspection-and-comparison"
---

# `git describe`

## Ejemplo de partida

```bash
git tag v1.0
git describe --tags --always HEAD
```

Este caso usa `git describe` para nombrar un commit con la referencia cercana que lo alcanza. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los estados u objetos que la consulta debe mostrar o comparar.
- Operación: nombrar un commit con la referencia cercana que lo alcanza.
- Comprobación: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Modelo mental

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Forma de referencia

```text
git describe [--all] [--tags] [--contains] [--abbrev=<n>] [<commit-ish>…]
git describe [--all] [--tags] [--contains] [--abbrev=<n>] --dirty[=<mark>]
git describe <blob>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

## Páginas relacionadas

- [`git diff`](../inspection-and-comparison/diff.md)
- [`git difftool`](../inspection-and-comparison/difftool.md)

## Fuente

- [git-describe - Give an object a human readable name based on an available ref](https://git-scm.com/docs/git-describe)
