---
title: "git apply"
source: "https://git-scm.com/docs/git-apply"
section: "patching"
---

# `git apply`

## Ejemplo de partida

```bash
git apply --check cambio.patch
git apply cambio.patch
```

Este caso usa `git apply` para aplicar un parche sobre archivos o sobre el índice. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un parche, un commit o un rango que representa cambios.
- Operación: aplicar un parche sobre archivos o sobre el índice.
- Comprobación: el diff y el historial muestran si cambiaron archivos, índice o commits.

## Modelo mental

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Forma de referencia

```text
git apply [--stat] [--numstat] [--summary] [--check]
	  [--index | --intent-to-add] [--3way] [--ours | --theirs | --union]
	  [--apply] [--no-add] [--build-fake-ancestor=<file>] [-R | --reverse]
	  [--allow-binary-replacement | --binary] [--reject] [-z]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

## Páginas relacionadas

- [`git cherry-pick`](../patching/cherry-pick.md)
- [`git rebase`](../patching/rebase.md)

## Fuente

- [git-apply - Apply a patch to files and/or to the index](https://git-scm.com/docs/git-apply)
