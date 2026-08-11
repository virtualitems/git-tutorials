---
title: "git rebase"
source: "https://git-scm.com/docs/git-rebase"
section: "patching"
---

# `git rebase`

## Ejemplo de partida

```bash
git switch tema-portada
git rebase main
```

Este caso usa `git rebase` para reaplicar commits sobre una base distinta. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un parche, un commit o un rango que representa cambios.
- Operación: reaplicar commits sobre una base distinta.
- Comprobación: el diff y el historial muestran si cambiaron archivos, índice o commits.

## Modelo mental

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Forma de referencia

```text
git rebase [-i | --interactive] [<options>] [--exec <cmd>]
	[--onto <newbase> | --keep-base] [<upstream> [<branch>]]
git rebase [-i | --interactive] [<options>] [--exec <cmd>] [--onto <newbase>]
	--root [<branch>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

## Páginas relacionadas

- [`git replay`](../patching/replay.md)
- [`git cherry-pick`](../patching/cherry-pick.md)
- [`git revert`](../patching/revert.md)

## Fuente

- [git-rebase - Reapply commits on top of another base tip](https://git-scm.com/docs/git-rebase)
