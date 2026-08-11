---
title: "git prune"
source: "https://git-scm.com/docs/git-prune"
section: "administration"
---

# `git prune`

## Ejemplo de partida

```bash
git prune --dry-run
```

Este caso usa `git prune` para eliminar objetos sueltos que ningún objeto alcanzable necesita. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: los objetos, referencias o archivos de almacenamiento que se van a inspeccionar.
- Operación: eliminar objetos sueltos que ningún objeto alcanzable necesita.
- Comprobación: los modos de simulación y las consultas de tamaño muestran el efecto antes y después.

## Modelo mental

Git almacena objetos sueltos, packs, referencias y reflogs. Las tareas de administración reorganizan o eliminan datos según su alcanzabilidad y antigüedad.

Relaciona cada archivo con su alcanzabilidad y retención. La compactación cambia la representación; la poda puede cambiar qué datos se pueden recuperar.

## Forma de referencia

```text
git prune [-n] [-v] [--progress] [--expire <time>] [--] [<head>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Condición que debes comprobar

Este comando puede eliminar objetos que ya no sean alcanzables. Verifica reflogs y copias antes de ejecutarlo.

## Práctica

Haz la prueba en una copia. Ejecuta primero el modo de inspección o simulación disponible y registra referencias, reflogs y tamaño antes de modificar datos.

## Páginas relacionadas

- [`git reflog`](../administration/reflog.md)
- [`git pack-refs`](../administration/pack-refs.md)
- [`git repack`](../administration/repack.md)

## Fuente

- [git-prune - Prune all unreachable objects from the object database](https://git-scm.com/docs/git-prune)
