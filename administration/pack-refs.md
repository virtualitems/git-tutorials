---
title: "git pack-refs"
source: "https://git-scm.com/docs/git-pack-refs"
section: "administration"
---

# `git pack-refs`

## Ejemplo de partida

```bash
git show-ref --heads
git pack-refs --all --prune
```

Este caso usa `git pack-refs` para compactar referencias sueltas dentro del archivo packed-refs. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: compactar referencias sueltas dentro del archivo packed-refs.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git pack-refs [--all] [--no-prune] [--auto] [--include <pattern>] [--exclude <pattern>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git prune`](../administration/prune.md)
- [`git maintenance`](../administration/maintenance.md)
- [`git reflog`](../administration/reflog.md)

## Fuente

- [git-pack-refs - Pack heads and tags for efficient repository access](https://git-scm.com/docs/git-pack-refs)
