---
title: "git worktree"
source: "https://git-scm.com/docs/git-worktree"
section: "branching-and-merging"
---

# `git worktree`

## Ejemplo de partida

```bash
git worktree add ../biblioteca-release release
git worktree list
```

Este caso usa `git worktree` para vincular varias áreas de trabajo al mismo repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las ramas, commits o rutas que participan en la operación.
- Operación: vincular varias áreas de trabajo al mismo repositorio.
- Comprobación: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Modelo mental

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Forma de referencia

```text
git worktree add [-f] [--detach] [--checkout] [--lock [--reason <string>]]
		 [--orphan] [(-b | -B) <new-branch>] <path> [<commit-ish>]
git worktree list [-v | --porcelain [-z]]
git worktree lock [--reason <string>] <worktree>
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

## Páginas relacionadas

- [`git tag`](../branching-and-merging/tag.md)
- [`git switch`](../branching-and-merging/switch.md)

## Fuente

- [git-worktree - Manage multiple working trees](https://git-scm.com/docs/git-worktree)
