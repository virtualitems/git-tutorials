---
title: "git annotate"
source: "https://git-scm.com/docs/git-annotate"
section: "debugging"
---

# `git annotate`

## Ejemplo de partida

```bash
git annotate README.md
```

Este caso usa `git annotate` para atribuir cada línea de un archivo a un commit. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un patrón, una ruta y el rango de historial que limita la búsqueda.
- Operación: atribuir cada línea de un archivo a un commit.
- Comprobación: la salida identifica líneas, archivos o commits que cumplen el criterio.

## Modelo mental

La búsqueda combina revisiones, rutas y contenido. Primero delimita el conjunto de commits o archivos; después interpreta la evidencia que devuelve Git.

Reduce primero el rango y las rutas. Después interpreta cada coincidencia dentro de ese conjunto, sin atribuir significado a elementos que quedaron fuera.

## Forma de referencia

```text
git annotate [<options>] [<rev-opts>] [<rev>] [--] <file>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Prepara un historial corto con un cambio por commit. Delimita una ruta o un rango para comprobar qué evidencia incluye y cuál excluye el comando.

## Páginas relacionadas

- [`git bisect`](../debugging/bisect.md)
- [`git blame`](../debugging/blame.md)

## Fuente

- [git-annotate - Annotate file lines with commit information](https://git-scm.com/docs/git-annotate)
