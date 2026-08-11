---
title: "git difftool"
source: "https://git-scm.com/docs/git-difftool"
section: "inspection-and-comparison"
---

# `git difftool`

## Ejemplo de partida

```bash
git difftool main..tema-portada -- README.md
```

Este caso usa `git difftool` para ver comparaciones con una herramienta externa. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los estados u objetos que la consulta debe mostrar o comparar.
- Operación: ver comparaciones con una herramienta externa.
- Comprobación: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Modelo mental

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Forma de referencia

```text
git difftool [<options>] [<commit> [<commit>]] [--] [<path>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

## Páginas relacionadas

- [`git last-modified`](../inspection-and-comparison/last-modified.md)
- [`git diff`](../inspection-and-comparison/diff.md)
- [`git log`](../inspection-and-comparison/log.md)

## Fuente

- [git-difftool - Show changes using common diff tools](https://git-scm.com/docs/git-difftool)
