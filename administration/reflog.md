---
title: "git reflog"
source: "https://git-scm.com/docs/git-reflog"
section: "administration"
---

# `git reflog`

## Ejemplo de partida

```bash
git reflog --date=iso
git show HEAD@{1}
```

Este caso usa `git reflog` para consultar y administrar el registro de cambios de referencias. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: consultar y administrar el registro de cambios de referencias.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git reflog [show] [<log-options>] [<ref>]
git reflog list
git reflog exists <ref>
git reflog write <ref> <old-oid> <new-oid> <message>
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git repack`](../administration/repack.md)
- [`git prune`](../administration/prune.md)
- [`git replace`](../administration/replace.md)

## Fuente

- [git-reflog - Manage reflog information](https://git-scm.com/docs/git-reflog)
