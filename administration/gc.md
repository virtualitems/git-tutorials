---
title: "git gc"
source: "https://git-scm.com/docs/git-gc"
section: "administration"
---

# `git gc`

## Ejemplo de partida

```bash
git count-objects -v
git gc
git count-objects -v
```

Este caso usa `git gc` para compactar el almacenamiento y retirar datos que ya pueden podarse. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: compactar el almacenamiento y retirar datos que ya pueden podarse.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git gc [--aggressive] [--auto] [--[no-]detach] [--quiet] [--prune=<date> | --no-prune] [--force] [--keep-largest-pack]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git maintenance`](../administration/maintenance.md)
- [`git fsck`](../administration/fsck.md)
- [`git pack-refs`](../administration/pack-refs.md)

## Fuente

- [git-gc - Cleanup unnecessary files and optimize the local repository](https://git-scm.com/docs/git-gc)
