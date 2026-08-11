---
title: "git mergetool"
source: "https://git-scm.com/docs/git-mergetool"
section: "branching-and-merging"
---

# `git mergetool`

## Ejemplo de partida

```bash
git mergetool
git status --short
```

Este caso usa `git mergetool` para abrir una herramienta para resolver conflictos de fusión. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las ramas, commits o rutas que participan en la operación.
- Operación: abrir una herramienta para resolver conflictos de fusión.
- Comprobación: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Modelo mental

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Forma de referencia

```text
git mergetool [--tool=<tool>] [-y | --[no-]prompt] [<file>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

## Páginas relacionadas

- [`git merge-tree`](../branching-and-merging/merge-tree.md)
- [`git merge`](../branching-and-merging/merge.md)
- [`git refs`](../branching-and-merging/refs.md)

## Fuente

- [git-mergetool - Run merge conflict resolution tools to resolve merge conflicts](https://git-scm.com/docs/git-mergetool)
