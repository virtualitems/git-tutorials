---
title: "git fetch"
source: "https://git-scm.com/docs/git-fetch"
section: "sharing-and-updating-projects"
---

# `git fetch`

## Ejemplo de partida

```bash
git fetch origin
git log --oneline main..origin/main
```

Este caso usa `git fetch` para descargar objetos y referencias sin integrar la rama actual. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio, las referencias y el sentido de la transferencia.
- Operación: descargar objetos y referencias sin integrar la rama actual.
- Comprobación: las referencias locales y remotas permiten separar descarga, integración y publicación.

## Modelo mental

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Forma de referencia

```text
git fetch [<options>] [<repository> [<refspec>…]]
git fetch [<options>] <group>
git fetch --multiple [<options>] [(<repository>|<group>)…]
git fetch --all [<options>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

## Páginas relacionadas

- [`git ls-remote`](../sharing-and-updating-projects/ls-remote.md)
- [`git bundle`](../sharing-and-updating-projects/bundle.md)
- [`git pull`](../sharing-and-updating-projects/pull.md)

## Fuente

- [git-fetch - Download objects and refs from another repository](https://git-scm.com/docs/git-fetch)
