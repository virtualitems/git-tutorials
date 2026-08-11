---
title: "git add"
source: "https://git-scm.com/docs/git-add"
section: "basic-snapshotting"
---

# `git add`

## Ejemplo de partida

```bash
printf 'capítulo 1\n' > guia.txt
git add guia.txt
git status --short
```

Este caso usa `git add` para copiar cambios del área de trabajo al índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las rutas y el estado de origen seleccionados por los argumentos.
- Operación: copiar cambios del área de trabajo al índice.
- Comprobación: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Modelo mental

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Forma de referencia

```text
git add [--verbose | -v] [--dry-run | -n] [--force | -f] [--interactive | -i] [--patch | -p]
	[--edit | -e] [--[no-]all | -A | --[no-]ignore-removal | [--update | -u]] [--sparse]
	[--intent-to-add | -N] [--refresh] [--ignore-errors] [--ignore-missing] [--renormalize]
	[--chmod=(+|-)x] [--pathspec-from-file=<file> [--pathspec-file-nul]]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

## Páginas relacionadas

- [`git commit`](../basic-snapshotting/commit.md)
- [`git mv`](../basic-snapshotting/mv.md)

## Fuente

- [git-add - Add file contents to the index](https://git-scm.com/docs/git-add)
