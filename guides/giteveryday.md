---
title: "giteveryday"
source: "https://git-scm.com/docs/giteveryday"
section: "guides"
---

# `giteveryday`

## Ejemplo de partida

```bash
git status
git add README.md
git commit -m "Actualiza instrucciones"
git log --oneline -3
```

Este caso usa `giteveryday` para resolver tareas diarias con un conjunto de comandos. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: resolver tareas diarias con un conjunto de comandos.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
git status
git add README.md
git commit -m "Actualiza instrucciones"
git log --oneline -3
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitfaq`](../guides/gitfaq.md)
- [`gitdiffcore`](../guides/gitdiffcore.md)
- [`gitglossary`](../guides/gitglossary.md)

## Fuente

- [giteveryday - A useful minimum set of commands for Everyday Git](https://git-scm.com/docs/giteveryday)
