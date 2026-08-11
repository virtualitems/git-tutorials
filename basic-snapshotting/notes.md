---
title: "git notes"
source: "https://git-scm.com/docs/git-notes"
section: "basic-snapshotting"
---

# `git notes`

## Ejemplo de partida

```bash
git notes add -m "Revisado en clase" HEAD
git notes show HEAD
```

Este caso usa `git notes` para asociar anotaciones a objetos sin cambiar los objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las rutas y el estado de origen seleccionados por los argumentos.
- Operación: asociar anotaciones a objetos sin cambiar los objetos.
- Comprobación: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Modelo mental

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Forma de referencia

```text
git notes [list [<object>]]
git notes add [-f] [--allow-empty] [--[no-]separator | --separator=<paragraph-break>] [--[no-]stripspace] [-F <file> | -m <msg> | (-c | -C) <object>] [-e] [<object>]
git notes copy [-f] ( --stdin | <from-object> [<to-object>] )
git notes append [--allow-empty] [--[no-]separator | --separator=<paragraph-break>] [--[no-]stripspace] [-F <file> | -m <msg> | (-c | -C) <object>] [-e] [<object>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

## Páginas relacionadas

- [`git reset`](../basic-snapshotting/reset.md)
- [`git mv`](../basic-snapshotting/mv.md)
- [`git restore`](../basic-snapshotting/restore.md)

## Fuente

- [git-notes - Add or inspect object notes](https://git-scm.com/docs/git-notes)
