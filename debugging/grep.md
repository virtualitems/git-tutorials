---
title: "git grep"
source: "https://git-scm.com/docs/git-grep"
section: "debugging"
---

# `git grep`

## Ejemplo de partida

```bash
git grep -n "TODO" -- '*.js'
```

Este caso usa `git grep` para buscar texto en archivos del área de trabajo o de un árbol. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un patrón, una ruta y el rango de historial que limita la búsqueda.
- Operación: buscar texto en archivos del área de trabajo o de un árbol.
- Comprobación: la salida identifica líneas, archivos o commits que cumplen el criterio.

## Modelo mental

La búsqueda combina revisiones, rutas y contenido. Primero delimita el conjunto de commits o archivos; después interpreta la evidencia que devuelve Git.

Reduce primero el rango y las rutas. Después interpreta cada coincidencia dentro de ese conjunto, sin atribuir significado a elementos que quedaron fuera.

## Forma de referencia

```text
git grep [-a | --text] [-I] [--textconv] [-i | --ignore-case] [-w | --word-regexp]
	   [-v | --invert-match] [-h|-H] [--full-name]
	   [-E | --extended-regexp] [-G | --basic-regexp]
	   [-P | --perl-regexp]
# …
```

Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prepara un historial corto con un cambio por commit. Delimita una ruta o un rango para comprobar qué evidencia incluye y cuál excluye el comando.

## Páginas relacionadas

- [`git blame`](../debugging/blame.md)
- [`git bisect`](../debugging/bisect.md)

## Fuente

- [git-grep - Print lines matching a pattern](https://git-scm.com/docs/git-grep)
