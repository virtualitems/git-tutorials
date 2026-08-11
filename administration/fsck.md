---
title: "git fsck"
source: "https://git-scm.com/docs/git-fsck"
section: "administration"
---

# `git fsck`

## Ejemplo de partida

```bash
git fsck --full
```

Este caso usa `git fsck` para comprobar conectividad y validez de los objetos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: comprobar conectividad y validez de los objetos.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git fsck [--tags] [--root] [--unreachable] [--cache] [--no-reflogs]
	 [--[no-]full] [--strict] [--verbose] [--lost-found]
	 [--[no-]dangling] [--[no-]progress] [--connectivity-only]
	 [--[no-]name-objects] [--[no-]references] [<object>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git gc`](../administration/gc.md)
- [`git filter-branch`](../administration/filter-branch.md)
- [`git maintenance`](../administration/maintenance.md)

## Fuente

- [git-fsck - Verifies the connectivity and validity of the objects in the database](https://git-scm.com/docs/git-fsck)
