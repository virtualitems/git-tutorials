---
title: "git maintenance"
source: "https://git-scm.com/docs/git-maintenance"
section: "administration"
---

# `git maintenance`

## Ejemplo de partida

```bash
git maintenance run --task=commit-graph
git maintenance run --task=gc
```

Este caso usa `git maintenance` para ejecutar o programar tareas de mantenimiento del repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: ejecutar o programar tareas de mantenimiento del repositorio.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git maintenance run [<options>]
git maintenance start [--scheduler=<scheduler>]
git maintenance (stop|register|unregister) [<options>]
git maintenance is-needed [<options>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git pack-refs`](../administration/pack-refs.md)
- [`git gc`](../administration/gc.md)
- [`git prune`](../administration/prune.md)

## Fuente

- [git-maintenance - Run tasks to optimize Git repository data](https://git-scm.com/docs/git-maintenance)
