---
title: "git reset"
source: "https://git-scm.com/docs/git-reset"
section: "basic-snapshotting"
---

# `git reset`

## Ejemplo de partida

```bash
git add guia.txt
git reset HEAD -- guia.txt
git status --short
```

Este caso usa `git reset` para mover HEAD o restablecer el índice y, según el modo, el área de trabajo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las rutas y el estado de origen seleccionados por los argumentos.
- Operación: mover HEAD o restablecer el índice y, según el modo, el área de trabajo.
- Comprobación: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Modelo mental

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Forma de referencia

```text
git reset [--soft | --mixed [-N] | --hard | --merge | --keep] [-q] [<commit>]
git reset [-q] [<tree-ish>] [--] <pathspec>…
git reset [-q] [--pathspec-from-file=<file> [--pathspec-file-nul]] [<tree-ish>]
git reset (--patch | -p) [<tree-ish>] [--] [<pathspec>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Condición que debes comprobar

`--hard` también reemplaza archivos del área de trabajo. El ejemplo usa el modo predeterminado y solo retira una ruta del índice.

## Práctica

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

## Páginas relacionadas

- [`git restore`](../basic-snapshotting/restore.md)
- [`git notes`](../basic-snapshotting/notes.md)
- [`git rm`](../basic-snapshotting/rm.md)

## Fuente

- [git-reset - Set HEAD or the index to a known state](https://git-scm.com/docs/git-reset)
