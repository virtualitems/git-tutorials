---
title: "git revert"
source: "https://git-scm.com/docs/git-revert"
section: "patching"
---

# `git revert`

## Ejemplo de partida

```bash
git revert a1b2c3d
```

Este caso usa `git revert` para crear un commit que invierte el efecto de otro commit. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un parche, un commit o un rango que representa cambios.
- Operación: crear un commit que invierte el efecto de otro commit.
- Comprobación: el diff y el historial muestran si cambiaron archivos, índice o commits.

## Modelo mental

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Forma de referencia

```text
git revert [--[no-]edit] [-n] [-m <parent-number>] [-s] [-S[<keyid>]] <commit>…
git revert (--continue | --skip | --abort | --quit)
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

## Páginas relacionadas

- [`git replay`](../patching/replay.md)
- [`git rebase`](../patching/rebase.md)

## Fuente

- [git-revert - Revert some existing commits](https://git-scm.com/docs/git-revert)
