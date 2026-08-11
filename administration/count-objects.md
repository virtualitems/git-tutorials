---
title: "git count-objects"
source: "https://git-scm.com/docs/git-count-objects"
section: "administration"
---

# `git count-objects`

## Ejemplo de partida

```bash
git count-objects -v -H
```

Este caso usa `git count-objects` para medir objetos sueltos, packs y espacio ocupado. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: medir objetos sueltos, packs y espacio ocupado.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git count-objects [-v] [-H | --human-readable]
```

Los corchetes delimitan partes opcionales.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git filter-branch`](../administration/filter-branch.md)
- [`git clean`](../administration/clean.md)
- [`git fsck`](../administration/fsck.md)

## Fuente

- [git-count-objects - Count unpacked number of objects and their disk consumption](https://git-scm.com/docs/git-count-objects)
