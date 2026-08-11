---
title: "git submodule"
source: "https://git-scm.com/docs/git-submodule"
section: "sharing-and-updating-projects"
---

# `git submodule`

## Ejemplo de partida

```bash
git submodule add https://example.test/equipo/tema.git temas/base
git submodule update --init --recursive
```

Este caso usa `git submodule` para administrar repositorios incluidos dentro de otro repositorio. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio, las referencias y el sentido de la transferencia.
- Operación: administrar repositorios incluidos dentro de otro repositorio.
- Comprobación: las referencias locales y remotas permiten separar descarga, integración y publicación.

## Modelo mental

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Forma de referencia

```text
git submodule [--quiet] [--cached]
git submodule [--quiet] add [<options>] [--] <repository> [<path>]
git submodule [--quiet] status [--cached] [--recursive] [--] [<path>…]
git submodule [--quiet] init [--] [<path>…]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

## Páginas relacionadas

- [`git request-pull`](../sharing-and-updating-projects/request-pull.md)
- [`git remote`](../sharing-and-updating-projects/remote.md)

## Fuente

- [git-submodule - Initialize, update or inspect submodules](https://git-scm.com/docs/git-submodule)
