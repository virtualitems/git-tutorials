---
title: "git remote"
source: "https://git-scm.com/docs/git-remote"
section: "sharing-and-updating-projects"
---

# `git remote`

## Ejemplo de partida

```bash
git remote add origin https://example.test/equipo/biblioteca.git
git remote -v
```

Este caso usa `git remote` para crear y administrar nombres para repositorios remotos. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio, las referencias y el sentido de la transferencia.
- Operación: crear y administrar nombres para repositorios remotos.
- Comprobación: las referencias locales y remotas permiten separar descarga, integración y publicación.

## Modelo mental

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Forma de referencia

```text
git remote [-v | --verbose]
git remote add [-t <branch>] [-m <master>] [-f] [--[no-]tags] [--mirror=(fetch|push)] <name> <URL>
git remote rename [--[no-]progress] <old> <new>
git remote remove <name>
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

## Páginas relacionadas

- [`git request-pull`](../sharing-and-updating-projects/request-pull.md)
- [`git push`](../sharing-and-updating-projects/push.md)
- [`git submodule`](../sharing-and-updating-projects/submodule.md)

## Fuente

- [git-remote - Manage set of tracked repositories](https://git-scm.com/docs/git-remote)
