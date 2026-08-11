---
title: "git stash"
source: "https://git-scm.com/docs/git-stash"
section: "branching-and-merging"
---

# `git stash`

## Ejemplo de partida

```bash
git stash push -m "portada incompleta"
git switch main
git stash pop
```

Este caso usa `git stash` para guardar cambios sin commit y recuperar un área de trabajo limpia. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las ramas, commits o rutas que participan en la operación.
- Operación: guardar cambios sin commit y recuperar un área de trabajo limpia.
- Comprobación: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Modelo mental

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Forma de referencia

```text
git stash list [<log-options>]
git stash show [-u | --include-untracked | --only-untracked] [<diff-options>] [<stash>]
git stash drop [-q | --quiet] [<stash>]
git stash pop [--index] [-q | --quiet] [<stash>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

## Páginas relacionadas

- [`git switch`](../branching-and-merging/switch.md)
- [`git rerere`](../branching-and-merging/rerere.md)
- [`git tag`](../branching-and-merging/tag.md)

## Fuente

- [git-stash - Stash the changes in a dirty working directory away](https://git-scm.com/docs/git-stash)
