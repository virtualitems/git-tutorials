---
title: "git rerere"
source: "https://git-scm.com/docs/git-rerere"
section: "branching-and-merging"
---

# `git rerere`

## Ejemplo de partida

```bash
git config rerere.enabled true
git rerere status
```

Este caso usa `git rerere` para recordar resoluciones de conflictos y reutilizarlas. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las ramas, commits o rutas que participan en la operación.
- Operación: recordar resoluciones de conflictos y reutilizarlas.
- Comprobación: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Modelo mental

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Forma de referencia

```text
git rerere [clear | forget <pathspec>… | diff | status | remaining | gc]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

## Páginas relacionadas

- [`git stash`](../branching-and-merging/stash.md)
- [`git refs`](../branching-and-merging/refs.md)
- [`git switch`](../branching-and-merging/switch.md)

## Fuente

- [git-rerere - Reuse recorded resolution of conflicted merges](https://git-scm.com/docs/git-rerere)
