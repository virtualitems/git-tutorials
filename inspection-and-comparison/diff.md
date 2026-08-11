---
title: "git diff"
source: "https://git-scm.com/docs/git-diff"
section: "inspection-and-comparison"
---

# `git diff`

## Ejemplo de partida

```bash
git diff
git diff --staged
git diff main..tema-portada
```

Este caso usa `git diff` para comparar contenido entre el área de trabajo, el índice y commits. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los estados u objetos que la consulta debe mostrar o comparar.
- Operación: comparar contenido entre el área de trabajo, el índice y commits.
- Comprobación: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Modelo mental

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Forma de referencia

```text
git diff [<options>] [<commit>] [--] [<path>…]
git diff [<options>] --cached [--merge-base] [<commit>] [--] [<path>…]
git diff [<options>] [--merge-base] <commit> [<commit>…] <commit> [--] [<path>…]
git diff [<options>] <commit>...<commit> [--] [<path>…]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

## Páginas relacionadas

- [`git difftool`](../inspection-and-comparison/difftool.md)
- [`git describe`](../inspection-and-comparison/describe.md)
- [`git last-modified`](../inspection-and-comparison/last-modified.md)

## Fuente

- [git-diff - Show changes between commits, commit and working tree, etc](https://git-scm.com/docs/git-diff)
