---
title: "git commit"
source: "https://git-scm.com/docs/git-commit"
section: "basic-snapshotting"
---

# `git commit`

## Ejemplo de partida

```bash
git add guia.txt
git commit -m "Añade el primer capítulo"
```

Este caso usa `git commit` para registrar en el historial el contenido preparado en el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las rutas y el estado de origen seleccionados por los argumentos.
- Operación: registrar en el historial el contenido preparado en el índice.
- Comprobación: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Modelo mental

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Forma de referencia

```text
git commit [-a | --interactive | --patch] [-s] [-v] [-u[<mode>]] [--amend]
	   [--dry-run] <commit>_ | --fixup [(amend|reword):"><commit>]
	   [-F <file> | -m <msg>] [--reset-author] [--allow-empty]
	   [--allow-empty-message] [--no-verify] [-e] [--author=<author>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

## Páginas relacionadas

- [`git mv`](../basic-snapshotting/mv.md)
- [`git add`](../basic-snapshotting/add.md)
- [`git notes`](../basic-snapshotting/notes.md)

## Fuente

- [git-commit - Record changes to the repository](https://git-scm.com/docs/git-commit)
