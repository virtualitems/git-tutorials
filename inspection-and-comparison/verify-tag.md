---
title: "git verify-tag"
source: "https://git-scm.com/docs/git-verify-tag"
section: "inspection-and-comparison"
---

# `git verify-tag`

## Ejemplo de partida

```bash
git verify-tag v1.0
```

Este caso usa `git verify-tag` para verificar la firma criptográfica de etiquetas. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los estados u objetos que la consulta debe mostrar o comparar.
- Operación: verificar la firma criptográfica de etiquetas.
- Comprobación: la salida cambia cuando se modifica una sola revisión, ruta u opción de formato.

## Modelo mental

Estas operaciones leen objetos, referencias, índice o área de trabajo. Sus argumentos determinan los dos estados que se comparan o el conjunto que se recorre.

Nombra los estados que se leen a cada lado de la consulta. La revisión omitida suele implicar HEAD, el índice o el área de trabajo según el comando.

## Forma de referencia

```text
git verify-tag [-v | --verbose] [--format=<format>] [--raw] <tag>…
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Ejecuta la consulta sobre dos revisiones conocidas. Cambia un solo argumento y explica qué conjunto de objetos o rutas cambió.

## Páginas relacionadas

- [`git whatchanged`](../inspection-and-comparison/whatchanged.md)
- [`git verify-commit`](../inspection-and-comparison/verify-commit.md)
- [`git show-branch`](../inspection-and-comparison/show-branch.md)

## Fuente

- [git-verify-tag - Check the GPG signature of tags](https://git-scm.com/docs/git-verify-tag)
