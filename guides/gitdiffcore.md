---
title: "gitdiffcore"
source: "https://git-scm.com/docs/gitdiffcore"
section: "guides"
---

# `gitdiffcore`

## Ejemplo de partida

```bash
git diff -M -C --find-copies-harder HEAD~1 HEAD
```

Este caso usa `gitdiffcore` para entender las transformaciones que producen la salida de diff. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: entender las transformaciones que producen la salida de diff.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
git diff *
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`giteveryday`](../guides/giteveryday.md)
- [`gitcvs-migration`](../guides/gitcvs-migration.md)
- [`gitfaq`](../guides/gitfaq.md)

## Fuente

- [gitdiffcore - Tweaking diff output](https://git-scm.com/docs/gitdiffcore)
