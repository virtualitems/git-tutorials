---
title: "git clean"
source: "https://git-scm.com/docs/git-clean"
section: "administration"
---

# `git clean`

## Ejemplo de partida

```bash
git clean -nd
git clean -fd
```

Este caso usa `git clean` para eliminar archivos que Git no sigue. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: eliminar archivos que Git no sigue.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git clean [-d] [-f] [-i] [-n] [-q] [-e <pattern>] [-x | -X] [--] [<pathspec>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Condición que debes comprobar

Ejecuta primero `git clean -n`. La opción `-f` elimina archivos sin seguimiento.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git count-objects`](../administration/count-objects.md)
- [`git backfill`](../administration/backfill.md)
- [`git filter-branch`](../administration/filter-branch.md)

## Fuente

- [git-clean - Remove untracked files from the working tree](https://git-scm.com/docs/git-clean)
