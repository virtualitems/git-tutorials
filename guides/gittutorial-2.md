---
title: "gittutorial-2"
source: "https://git-scm.com/docs/gittutorial-2"
section: "guides"
---

# `gittutorial-2`

## Ejemplo de partida

```bash
git cat-file -p HEAD
git cat-file -p HEAD^{tree}
git ls-files --stage
```

Este caso usa `gittutorial-2` para relacionar el índice, los objetos y las referencias detrás de los comandos. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: relacionar el índice, los objetos y las referencias detrás de los comandos.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
git *
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitworkflows`](../guides/gitworkflows.md)
- [`gittutorial`](../guides/gittutorial.md)
- [`gitattributes`](../guides/gitattributes.md)

## Fuente

- [gittutorial-2 - A tutorial introduction to Git: part two](https://git-scm.com/docs/gittutorial-2)
