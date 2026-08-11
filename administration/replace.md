---
title: "git replace"
source: "https://git-scm.com/docs/git-replace"
section: "administration"
---

# `git replace`

## Ejemplo de partida

```bash
original=$(git rev-parse HEAD~1)
sustituto=$(git rev-parse HEAD)
git replace "$original" "$sustituto"
```

Este caso usa `git replace` para sustituir un objeto por otro durante el recorrido del repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: sustituir un objeto por otro durante el recorrido del repositorio.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git replace [-f] <object> <replacement>
git replace [-f] --edit <object>
git replace [-f] --graft <commit> [<parent>…]
git replace [-f] --convert-graft-file
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`scalar`](../administration/scalar.md)
- [`git repack`](../administration/repack.md)
- [`git reflog`](../administration/reflog.md)

## Fuente

- [git-replace - Create, list, delete refs to replace objects](https://git-scm.com/docs/git-replace)
