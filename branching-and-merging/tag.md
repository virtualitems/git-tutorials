---
title: "git tag"
source: "https://git-scm.com/docs/git-tag"
section: "branching-and-merging"
---

# `git tag`

## Ejemplo de partida

```bash
git tag -a v1.0 -m "Primera entrega"
git show v1.0
```

Este caso usa `git tag` para crear, listar, verificar y eliminar etiquetas. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las ramas, commits o rutas que participan en la operación.
- Operación: crear, listar, verificar y eliminar etiquetas.
- Comprobación: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Modelo mental

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Forma de referencia

```text
git tag [-a | -s | -u <key-id>] [-f] [-m <msg> | -F <file>] [-e]
	[(--trailer <token>[(=|:)<value>])…]
	<tagname> [<commit> | <object>]
git tag -d <tagname>…
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

## Páginas relacionadas

- [`git worktree`](../branching-and-merging/worktree.md)
- [`git switch`](../branching-and-merging/switch.md)
- [`git stash`](../branching-and-merging/stash.md)

## Fuente

- [git-tag - Create, list, delete or verify tags](https://git-scm.com/docs/git-tag)
