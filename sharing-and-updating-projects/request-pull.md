---
title: "git request-pull"
source: "https://git-scm.com/docs/git-request-pull"
section: "sharing-and-updating-projects"
---

# `git request-pull`

## Ejemplo de partida

```bash
git request-pull v1.0 https://example.test/equipo/biblioteca.git main
```

Este caso usa `git request-pull` para generar un resumen para solicitar que otra persona integre cambios. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio, las referencias y el sentido de la transferencia.
- Operación: generar un resumen para solicitar que otra persona integre cambios.
- Comprobación: las referencias locales y remotas permiten separar descarga, integración y publicación.

## Modelo mental

La transferencia copia objetos y actualiza referencias. Descargar, integrar y publicar son operaciones separadas aunque algunos comandos las encadenen.

Distingue las referencias de seguimiento remoto de la rama actual. Descargar una referencia no integra por sí mismo sus commits.

## Forma de referencia

```text
git request-pull [-p] <start> <URL> [<end>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Usa dos clones locales del mismo repositorio. Observa por separado los objetos descargados, las ramas remotas y la rama actual.

## Páginas relacionadas

- [`git submodule`](../sharing-and-updating-projects/submodule.md)
- [`git remote`](../sharing-and-updating-projects/remote.md)
- [`git push`](../sharing-and-updating-projects/push.md)

## Fuente

- [git-request-pull - Generates a summary of pending changes](https://git-scm.com/docs/git-request-pull)
