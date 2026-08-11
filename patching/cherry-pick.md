---
title: "git cherry-pick"
source: "https://git-scm.com/docs/git-cherry-pick"
section: "patching"
---

# `git cherry-pick`

## Ejemplo de partida

```bash
git switch release
git cherry-pick a1b2c3d
```

Este caso usa `git cherry-pick` para aplicar en la rama actual el cambio de commits existentes. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un parche, un commit o un rango que representa cambios.
- Operación: aplicar en la rama actual el cambio de commits existentes.
- Comprobación: el diff y el historial muestran si cambiaron archivos, índice o commits.

## Modelo mental

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Forma de referencia

```text
git cherry-pick [--edit] [-n] [-m <parent-number>] [-s] [-x] [--ff]
		  [-S[<keyid>]] <commit>…
git cherry-pick (--continue | --skip | --abort | --quit)
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

## Páginas relacionadas

- [`git rebase`](../patching/rebase.md)
- [`git apply`](../patching/apply.md)
- [`git replay`](../patching/replay.md)

## Fuente

- [git-cherry-pick - Apply the changes introduced by some existing commits](https://git-scm.com/docs/git-cherry-pick)
