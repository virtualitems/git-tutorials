---
title: "git rm"
source: "https://git-scm.com/docs/git-rm"
section: "basic-snapshotting"
---

# `git rm`

## Ejemplo de partida

```bash
git rm notas-temporales.txt
git commit -m "Retira notas temporales"
```

Este caso usa `git rm` para retirar rutas del índice y, por defecto, del área de trabajo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las rutas y el estado de origen seleccionados por los argumentos.
- Operación: retirar rutas del índice y, por defecto, del área de trabajo.
- Comprobación: `git status` permite distinguir cambios en el área de trabajo, el índice y HEAD.

## Modelo mental

El área de trabajo contiene los archivos editables. El índice describe el próximo snapshot. Un commit registra un árbol derivado del índice y enlaza con commits anteriores.

Identifica el origen y el destino de cada cambio. Una orden puede leer HEAD y escribir el índice sin modificar el archivo del área de trabajo.

## Forma de referencia

```text
git rm [-f | --force] [-n] [-r] [--cached] [--ignore-unmatch]
       [--quiet] [--pathspec-from-file=<file> [--pathspec-file-nul]]
       [--] [<pathspec>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Crea un repositorio temporal, modifica una ruta y ejecuta `git status --short` antes y después de cada línea del ejemplo.

## Páginas relacionadas

- [`git status`](../basic-snapshotting/status.md)
- [`git restore`](../basic-snapshotting/restore.md)
- [`git reset`](../basic-snapshotting/reset.md)

## Fuente

- [git-rm - Remove files from the working tree and from the index](https://git-scm.com/docs/git-rm)
