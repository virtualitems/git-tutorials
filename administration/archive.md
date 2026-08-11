---
title: "git archive"
source: "https://git-scm.com/docs/git-archive"
section: "administration"
---

# `git archive`

## Ejemplo de partida

```bash
git archive --format=zip --output=entrega.zip HEAD
```

Este caso usa `git archive` para crear un archivo tar o zip a partir de un árbol de Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: crear un archivo tar o zip a partir de un árbol de Git.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git archive [--format=<fmt>] [--list] [--prefix=<prefix>/] [<extra>]
	      [-o <file> | --output=<file>] [--worktree-attributes]
	      [--remote=<repo> [--exec=<git-upload-archive>]] <tree-ish>
	      [<path>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git backfill`](../administration/backfill.md)
- [`git clean`](../administration/clean.md)

## Fuente

- [git-archive - Create an archive of files from a named tree](https://git-scm.com/docs/git-archive)
