---
title: "gitrevisions"
source: "https://git-scm.com/docs/gitrevisions"
section: "guides"
---

# `gitrevisions`

## Ejemplo de partida

```bash
git show HEAD~2
git log main..tema-portada
git diff v1.0...main
```

Este caso usa `gitrevisions` para seleccionar commits y rangos mediante la sintaxis de revisiones. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: seleccionar commits y rangos mediante la sintaxis de revisiones.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
git show HEAD~2
git log main..tema-portada
git diff v1.0...main
```

Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitrepository-layout`](../guides/gitrepository-layout.md)
- [`gitmodules`](../guides/gitmodules.md)

## Fuente

- [gitrevisions - Specifying revisions and ranges for Git](https://git-scm.com/docs/gitrevisions)
