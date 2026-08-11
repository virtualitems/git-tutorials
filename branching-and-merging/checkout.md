---
title: "git checkout"
source: "https://git-scm.com/docs/git-checkout"
section: "branching-and-merging"
---

# `git checkout`

## Ejemplo de partida

```bash
git checkout main
git checkout HEAD~1 -- README.md
```

Este caso usa `git checkout` para cambiar de rama o restaurar rutas desde otro estado. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las ramas, commits o rutas que participan en la operación.
- Operación: cambiar de rama o restaurar rutas desde otro estado.
- Comprobación: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Modelo mental

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Forma de referencia

```text
git checkout [-q] [-f] [-m] [<branch>]
git checkout [-q] [-f] [-m] --detach [<branch>]
git checkout [-q] [-f] [-m] [--detach] <commit>
git checkout [-q] [-f] [-m] [[-b|-B|--orphan] <new-branch>] [<start-point>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

## Páginas relacionadas

- [`git history`](../branching-and-merging/history.md)
- [`git branch`](../branching-and-merging/branch.md)
- [`git merge`](../branching-and-merging/merge.md)

## Fuente

- [git-checkout - Switch branches or restore working tree files](https://git-scm.com/docs/git-checkout)
