---
title: "git blame"
source: "https://git-scm.com/docs/git-blame"
section: "debugging"
---

# `git blame`

## Ejemplo de partida

```bash
git blame -L 10,20 -- README.md
```

Este caso usa `git blame` para mostrar el commit y autor asociados con cada línea de un archivo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un patrón, una ruta y el rango de historial que limita la búsqueda.
- Operación: mostrar el commit y autor asociados con cada línea de un archivo.
- Comprobación: la salida identifica líneas, archivos o commits que cumplen el criterio.

## Modelo mental

La búsqueda combina revisiones, rutas y contenido. Primero delimita el conjunto de commits o archivos; después interpreta la evidencia que devuelve Git.

Reduce primero el rango y las rutas. Después interpreta cada coincidencia dentro de ese conjunto, sin atribuir significado a elementos que quedaron fuera.

## Forma de referencia

```text
git blame [-c] [-b] [-l] [--root] [-t] [-f] [-n] [-s] [-e] [-p] [-w] [--incremental]
	  [-L <range>] [-S <revs-file>] [-M] [-C] [-C] [-C] [--since=<date>]
	  [--ignore-rev <rev>] [--ignore-revs-file <file>]
	  [--color-lines] [--color-by-age] [--progress] [--abbrev=<n>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Prepara un historial corto con un cambio por commit. Delimita una ruta o un rango para comprobar qué evidencia incluye y cuál excluye el comando.

## Páginas relacionadas

- [`git grep`](../debugging/grep.md)
- [`git bisect`](../debugging/bisect.md)
- [`git annotate`](../debugging/annotate.md)

## Fuente

- [git-blame - Show what revision and author last modified each line of a file](https://git-scm.com/docs/git-blame)
