---
title: "gitignore"
source: "https://git-scm.com/docs/gitignore"
section: "guides"
---

# `gitignore`

## Ejemplo de partida

```ini
# .gitignore
.env
node_modules/
build/*.log
!build/.gitkeep
```

Este caso usa `gitignore` para declarar patrones de archivos que Git debe dejar sin seguimiento. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: declarar patrones de archivos que Git debe dejar sin seguimiento.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
# .gitignore
.env
node_modules/
build/*.log
# …
```

Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitmailmap`](../guides/gitmailmap.md)
- [`githooks`](../guides/githooks.md)
- [`gitmodules`](../guides/gitmodules.md)

## Fuente

- [gitignore - Specifies intentionally untracked files to ignore](https://git-scm.com/docs/gitignore)
