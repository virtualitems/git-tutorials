---
title: "git backfill"
source: "https://git-scm.com/docs/git-backfill"
section: "administration"
---

# `git backfill`

## Ejemplo de partida

```bash
git clone --filter=blob:none https://example.test/biblioteca.git
cd biblioteca
git backfill main~50..main
```

Este caso usa `git backfill` para descargar en lotes los objetos que faltan en un clon parcial. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: descargar en lotes los objetos que faltan en un clon parcial.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git backfill [--min-batch-size=<n>] [--[no-]sparse] [--[no-]include-edges] [<revision-range>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git clean`](../administration/clean.md)
- [`git archive`](../administration/archive.md)
- [`git count-objects`](../administration/count-objects.md)

## Fuente

- [git-backfill - Download missing objects in a partial clone](https://git-scm.com/docs/git-backfill)
