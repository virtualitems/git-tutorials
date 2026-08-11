---
title: "git replay"
source: "https://git-scm.com/docs/git-replay"
section: "patching"
---

# `git replay`

## Ejemplo de partida

```bash
git replay --onto=main main..tema-portada
```

Este caso usa `git replay` para reproducir commits sobre una base y comunicar el cambio de referencias. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: un parche, un commit o un rango que representa cambios.
- Operación: reproducir commits sobre una base y comunicar el cambio de referencias.
- Comprobación: el diff y el historial muestran si cambiaron archivos, índice o commits.

## Modelo mental

Un parche representa diferencias de contenido. Aplicarlo puede modificar archivos, el índice o producir commits nuevos, según el comando.

Determina si la operación aplica diferencias a archivos, al índice o al historial. Esa elección define cómo se comprueba y cómo se revierte el resultado.

## Forma de referencia

```text
(EXPERIMENTAL!) git replay ([--contained] --onto=<newbase> | --advance=<branch> | --revert=<branch>)
			     [--ref=<ref>] [--ref-action=<mode>] <revision-range>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Trabaja en una rama de prueba. Compara `git diff`, `git diff --staged` y `git log --oneline --graph` antes y después.

## Páginas relacionadas

- [`git revert`](../patching/revert.md)
- [`git rebase`](../patching/rebase.md)
- [`git cherry-pick`](../patching/cherry-pick.md)

## Fuente

- [git-replay - EXPERIMENTAL: Replay commits on a new base, works with bare repos too](https://git-scm.com/docs/git-replay)
