---
title: "git ls-remote"
source: "https://git-scm.com/docs/git-ls-remote"
section: "sharing-and-updating-projects"
---

# `git ls-remote`

## Ejemplo de partida

```bash
git ls-remote --heads origin
```

Este caso usa `git ls-remote` para enumerar referencias anunciadas por un repositorio remoto. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio, las referencias y el sentido de la transferencia.
- Operación: enumerar referencias anunciadas por un repositorio remoto.
- Comprobación: las referencias locales y remotas permiten separar descarga, integración y publicación.

## Modelo mental

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Forma de referencia

```text
git ls-remote [--branches] [--tags] [--refs] [--upload-pack=<exec>]
	      [-q | --quiet] [--exit-code] [--get-url] [--sort=<key>]
	      [--symref] [<repository> [<patterns>…]]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

## Páginas relacionadas

- [`git pull`](../sharing-and-updating-projects/pull.md)
- [`git fetch`](../sharing-and-updating-projects/fetch.md)
- [`git push`](../sharing-and-updating-projects/push.md)

## Fuente

- [git-ls-remote - List references in a remote repository](https://git-scm.com/docs/git-ls-remote)
