---
title: "gitfaq"
source: "https://git-scm.com/docs/gitfaq"
section: "guides"
---

# `gitfaq`

## Ejemplo de partida

```bash
git add README.md
git restore --staged README.md
git status --short
```

Este caso usa `gitfaq` para resolver preguntas sobre configuración, historial y archivos. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: resolver preguntas sobre configuración, historial y archivos.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
git add README.md
git restore --staged README.md
git status --short
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitglossary`](../guides/gitglossary.md)
- [`giteveryday`](../guides/giteveryday.md)
- [`gitnamespaces`](../guides/gitnamespaces.md)

## Fuente

- [gitfaq - Frequently asked questions about using Git](https://git-scm.com/docs/gitfaq)
