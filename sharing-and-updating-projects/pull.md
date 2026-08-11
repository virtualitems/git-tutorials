---
title: "git pull"
source: "https://git-scm.com/docs/git-pull"
section: "sharing-and-updating-projects"
---

# `git pull`

## Ejemplo de partida

```bash
git pull --ff-only origin main
```

Este caso usa `git pull` para descargar cambios e integrarlos en la rama actual. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio, las referencias y el sentido de la transferencia.
- Operación: descargar cambios e integrarlos en la rama actual.
- Comprobación: las referencias locales y remotas permiten separar descarga, integración y publicación.

## Modelo mental

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Forma de referencia

```text
git pull [<options>] [<repository> [<refspec>…]]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

## Páginas relacionadas

- [`git push`](../sharing-and-updating-projects/push.md)
- [`git ls-remote`](../sharing-and-updating-projects/ls-remote.md)
- [`git remote`](../sharing-and-updating-projects/remote.md)

## Fuente

- [git-pull - Fetch from and integrate with another repository or a local branch](https://git-scm.com/docs/git-pull)
