---
title: "git bundle"
source: "https://git-scm.com/docs/git-bundle"
section: "sharing-and-updating-projects"
---

# `git bundle`

## Ejemplo de partida

```bash
git bundle create entrega.bundle main
git bundle verify entrega.bundle
git clone entrega.bundle copia
```

Este caso usa `git bundle` para transportar objetos y referencias dentro de un solo archivo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio, las referencias y el sentido de la transferencia.
- Operación: transportar objetos y referencias dentro de un solo archivo.
- Comprobación: las referencias locales y remotas permiten separar descarga, integración y publicación.

## Modelo mental

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Forma de referencia

```text
git bundle create [-q | --quiet | --progress]
		    [--version=<version>] <file> <git-rev-list-args>
git bundle verify [-q | --quiet] <file>
git bundle list-heads <file> [<refname>…]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

## Páginas relacionadas

- [`git fetch`](../sharing-and-updating-projects/fetch.md)
- [`git ls-remote`](../sharing-and-updating-projects/ls-remote.md)

## Fuente

- [git-bundle - Move objects and refs by archive](https://git-scm.com/docs/git-bundle)
