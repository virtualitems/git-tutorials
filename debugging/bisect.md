---
title: "git bisect"
source: "https://git-scm.com/docs/git-bisect"
section: "debugging"
---

# `git bisect`

## Ejemplo de partida

```bash
git bisect start
git bisect bad
git bisect good v1.0
git bisect run ./prueba.sh
git bisect reset
```

Este caso usa `git bisect` para localizar por búsqueda binaria el commit que introdujo un cambio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un patrón, una ruta y el rango de historial que limita la búsqueda.
- Operación: localizar por búsqueda binaria el commit que introdujo un cambio.
- Comprobación: la salida identifica líneas, archivos o commits que cumplen el criterio.

## Modelo mental

La búsqueda combina revisiones, rutas y contenido. Primero delimita el conjunto de commits o archivos; después interpreta la evidencia que devuelve Git.

Reduce primero el rango y las rutas. Después interpreta cada coincidencia dentro de ese conjunto, sin atribuir significado a elementos que quedaron fuera.

## Forma de referencia

```text
git bisect start [--term-(bad|new)=<term-new> --term-(good|old)=<term-old>]
		 [--no-checkout] [--first-parent] [<bad> [<good>…]] [--] [<pathspec>…]
git bisect (bad|new|<term-new>) [<rev>]
git bisect (good|old|<term-old>) [<rev>…]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Prepara un historial corto con un cambio por commit. Delimita una ruta o un rango para comprobar qué evidencia incluye y cuál excluye el comando.

## Páginas relacionadas

- [`git blame`](../debugging/blame.md)
- [`git annotate`](../debugging/annotate.md)
- [`git grep`](../debugging/grep.md)

## Fuente

- [git-bisect - Use binary search to find the commit that introduced a bug](https://git-scm.com/docs/git-bisect)
