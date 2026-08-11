---
title: "gitworkflows"
source: "https://git-scm.com/docs/gitworkflows"
section: "guides"
---

# `gitworkflows`

## Ejemplo de partida

```bash
main:          A---B-------M
                         /
tema-portada:     C---D
```

Este caso usa `gitworkflows` para organizar ramas, integración y publicación en un equipo. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: organizar ramas, integración y publicación en un equipo.
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

- [`gitattributes`](../guides/gitattributes.md)
- [`gittutorial-2`](../guides/gittutorial-2.md)
- [`gitcli`](../guides/gitcli.md)

## Fuente

- [gitworkflows - An overview of recommended workflows with Git](https://git-scm.com/docs/gitworkflows)
