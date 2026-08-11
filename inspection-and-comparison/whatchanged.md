---
title: "git whatchanged"
source: "https://git-scm.com/docs/git-whatchanged"
section: "inspection-and-comparison"
---

# `git whatchanged`

## Ejemplo de partida

```bash
git whatchanged --oneline -- README.md
```

Este caso usa `git whatchanged` para mostrar commits junto con diferencias en formato sin procesar. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los estados u objetos que la consulta debe mostrar o comparar.
- Operación: mostrar commits junto con diferencias en formato sin procesar.
- Comprobación: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Modelo mental

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Forma de referencia

```text
git whatchanged <option>…
```

Los elementos entre `<` y `>` se sustituyen por valores. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

## Páginas relacionadas

- [`git verify-tag`](../inspection-and-comparison/verify-tag.md)
- [`git verify-commit`](../inspection-and-comparison/verify-commit.md)

## Fuente

- [git-whatchanged - Show logs with differences each commit introduces](https://git-scm.com/docs/git-whatchanged)
