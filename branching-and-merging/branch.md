---
title: "git branch"
source: "https://git-scm.com/docs/git-branch"
section: "branching-and-merging"
---

# `git branch`

## Ejemplo de partida

```bash
git branch tema-portada
git branch --list
git branch -d tema-portada
```

Este caso usa `git branch` para listar, crear, renombrar y eliminar ramas. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: las ramas, commits o rutas que participan en la operación.
- Operación: listar, crear, renombrar y eliminar ramas.
- Comprobación: `git log --graph` y `git show-ref` muestran los commits y punteros resultantes.

## Modelo mental

Una rama es una referencia que apunta a un commit. Cambiar de rama mueve HEAD; fusionar o reorganizar historial crea o reasigna commits y referencias.

Distingue los commits de los nombres que los señalan. Reescribir o fusionar puede crear commits nuevos aunque el contenido final coincida.

## Forma de referencia

```text
git branch [--color[=<when>] | --no-color] [--show-current]
	   [-v [--abbrev=<n> | --no-abbrev]]
	   [--column[=<options>] | --no-column] [--sort=<key>]
	   [--merged [<commit>]] [--no-merged [<commit>]]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Dibuja los commits como nodos y las ramas como nombres móviles. Ejecuta el ejemplo y vuelve a dibujar solo los punteros que cambiaron.

## Páginas relacionadas

- [`git checkout`](../branching-and-merging/checkout.md)
- [`git history`](../branching-and-merging/history.md)

## Fuente

- [git-branch - List, create, or delete branches](https://git-scm.com/docs/git-branch)
