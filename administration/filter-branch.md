---
title: "git filter-branch"
source: "https://git-scm.com/docs/git-filter-branch"
section: "administration"
---

# `git filter-branch`

## Ejemplo de partida

```bash
git filter-branch --tree-filter 'rm -f secreto.txt' -- --all
```

Este caso usa `git filter-branch` para reescribir ramas mediante filtros sobre cada commit. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: reescribir ramas mediante filtros sobre cada commit.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git filter-branch [--setup <command>] [--subdirectory-filter <directory>]
	[--env-filter <command>] [--tree-filter <command>]
	[--index-filter <command>] [--parent-filter <command>]
	[--msg-filter <command>] [--commit-filter <command>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Condición que debes comprobar

Este comando reescribe identificadores en toda la parte afectada del historial. Trabaja sobre una copia y conserva referencias de respaldo.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git fsck`](../administration/fsck.md)
- [`git count-objects`](../administration/count-objects.md)
- [`git gc`](../administration/gc.md)

## Fuente

- [git-filter-branch - Rewrite branches](https://git-scm.com/docs/git-filter-branch)
