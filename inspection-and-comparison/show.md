---
title: "git show"
source: "https://git-scm.com/docs/git-show"
section: "inspection-and-comparison"
---

# `git show`

## Ejemplo de partida

```bash
git show --stat HEAD
git show HEAD:README.md
```

Este caso usa `git show` para mostrar un objeto y la información asociada a su tipo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los estados u objetos que la consulta debe mostrar o comparar.
- Operación: mostrar un objeto y la información asociada a su tipo.
- Comprobación: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Modelo mental

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Forma de referencia

```text
git show [<options>] [<object>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

## Páginas relacionadas

- [`git show-branch`](../inspection-and-comparison/show-branch.md)
- [`git shortlog`](../inspection-and-comparison/shortlog.md)
- [`git verify-commit`](../inspection-and-comparison/verify-commit.md)

## Fuente

- [git-show - Show various types of objects](https://git-scm.com/docs/git-show)
