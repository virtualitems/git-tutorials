---
title: "git mv"
source: "https://git-scm.com/docs/git-mv"
section: "basic-snapshotting"
---

# `git mv`

## Ejemplo de partida

```bash
git mv borrador.md capitulos/introduccion.md
git status --short
```

Este caso usa `git mv` para mover o renombrar una ruta seguida por Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las rutas y el estado de origen seleccionados por los argumentos.
- Operación: mover o renombrar una ruta seguida por Git.
- Comprobación: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Modelo mental

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Forma de referencia

```text
git mv [-v] [-f] [-n] [-k] <source> <destination>
git mv [-v] [-f] [-n] [-k] <source>... <destination-directory>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

## Páginas relacionadas

- [`git notes`](../basic-snapshotting/notes.md)
- [`git commit`](../basic-snapshotting/commit.md)
- [`git reset`](../basic-snapshotting/reset.md)

## Fuente

- [git-mv - Move or rename a file, a directory, or a symlink](https://git-scm.com/docs/git-mv)
