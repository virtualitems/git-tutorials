---
title: "git status"
source: "https://git-scm.com/docs/git-status"
section: "basic-snapshotting"
---

# `git status`

## Ejemplo de partida

```bash
git status --short --branch
```

Este caso usa `git status` para comparar el área de trabajo y el índice con el commit actual. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las rutas y el estado de origen seleccionados por los argumentos.
- Operación: comparar el área de trabajo y el índice con el commit actual.
- Comprobación: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Modelo mental

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Forma de referencia

```text
git status [<options>] [--] [<pathspec>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

## Páginas relacionadas

- [`git rm`](../basic-snapshotting/rm.md)
- [`git restore`](../basic-snapshotting/restore.md)

## Fuente

- [git-status - Show the working tree status](https://git-scm.com/docs/git-status)
