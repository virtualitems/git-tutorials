---
title: "git restore"
source: "https://git-scm.com/docs/git-restore"
section: "basic-snapshotting"
---

# `git restore`

## Ejemplo de partida

```bash
git restore --source=HEAD -- guia.txt
git restore --staged guia.txt
```

Este caso usa `git restore` para recuperar contenido de rutas en el índice o el área de trabajo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las rutas y el estado de origen seleccionados por los argumentos.
- Operación: recuperar contenido de rutas en el índice o el área de trabajo.
- Comprobación: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Modelo mental

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Forma de referencia

```text
git restore [<options>] [--source=<tree>] [--staged] [--worktree] [--] <pathspec>…
git restore [<options>] [--source=<tree>] [--staged] [--worktree] --pathspec-from-file=<file> [--pathspec-file-nul]
git restore (-p|--patch) [<options>] [--source=<tree>] [--staged] [--worktree] [--] [<pathspec>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

## Páginas relacionadas

- [`git rm`](../basic-snapshotting/rm.md)
- [`git reset`](../basic-snapshotting/reset.md)
- [`git status`](../basic-snapshotting/status.md)

## Fuente

- [git-restore - Restore working tree files](https://git-scm.com/docs/git-restore)
