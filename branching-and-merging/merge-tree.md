---
title: "git merge-tree"
source: "https://git-scm.com/docs/git-merge-tree"
section: "branching-and-merging"
---

# `git merge-tree`

## Ejemplo de partida

```bash
git merge-tree --write-tree main tema-portada
```

Este caso usa `git merge-tree` para calcular una fusión y exponer su resultado sin cambiar el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las ramas, commits o rutas que participan en la operación.
- Operación: calcular una fusión y exponer su resultado sin cambiar el índice.
- Comprobación: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Modelo mental

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Forma de referencia

```text
git merge-tree [--write-tree] [<options>] <branch1> <branch2>
git merge-tree [--trivial-merge] <base-tree> <branch1> <branch2> (deprecated)
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

## Páginas relacionadas

- [`git refs`](../branching-and-merging/refs.md)
- [`git mergetool`](../branching-and-merging/mergetool.md)
- [`git rerere`](../branching-and-merging/rerere.md)

## Fuente

- [git-merge-tree - Perform merge without touching index or working tree](https://git-scm.com/docs/git-merge-tree)
