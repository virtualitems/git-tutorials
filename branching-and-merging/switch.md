---
title: "git switch"
source: "https://git-scm.com/docs/git-switch"
section: "branching-and-merging"
---

# `git switch`

## Ejemplo de partida

```bash
git switch -c tema-portada
git switch main
```

Este caso usa `git switch` para cambiar de rama o crear una rama antes de cambiar. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las ramas, commits o rutas que participan en la operación.
- Operación: cambiar de rama o crear una rama antes de cambiar.
- Comprobación: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Modelo mental

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Forma de referencia

```text
git switch [<options>] [--no-guess] <branch>
git switch [<options>] --detach [<start-point>]
git switch [<options>] (-c|-C) <new-branch> [<start-point>]
git switch [<options>] --orphan <new-branch>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

## Páginas relacionadas

- [`git tag`](../branching-and-merging/tag.md)
- [`git stash`](../branching-and-merging/stash.md)
- [`git worktree`](../branching-and-merging/worktree.md)

## Fuente

- [git-switch - Switch branches](https://git-scm.com/docs/git-switch)
