---
title: "git refs"
source: "https://git-scm.com/docs/git-refs"
section: "branching-and-merging"
---

# `git refs`

## Ejemplo de partida

```bash
git refs list refs/heads
git refs verify --strict
```

Este caso usa `git refs` para consultar y modificar referencias mediante transacciones. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las ramas, commits o rutas que participan en la operación.
- Operación: consultar y modificar referencias mediante transacciones.
- Comprobación: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Modelo mental

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Forma de referencia

```text
git refs migrate --ref-format=<format> [--no-reflog] [--dry-run]
git refs verify [--strict] [--verbose]
git refs list [--count=<count>] [--shell|--perl|--python|--tcl]
		   [(--sort=<key>)…] [--format=<format>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

## Páginas relacionadas

- [`git rerere`](../branching-and-merging/rerere.md)
- [`git merge-tree`](../branching-and-merging/merge-tree.md)
- [`git stash`](../branching-and-merging/stash.md)

## Fuente

- [git-refs - Low-level access to refs](https://git-scm.com/docs/git-refs)
