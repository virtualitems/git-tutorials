---
title: "gitglossary"
source: "https://git-scm.com/docs/gitglossary"
section: "guides"
---

# `gitglossary`

## Ejemplo de partida

```text
HEAD -> refs/heads/main -> commit -> tree -> blob
```

Este caso usa `gitglossary` para relacionar los términos usados por la documentación de Git. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: relacionar los términos usados por la documentación de Git.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
HEAD -> refs/heads/main -> commit -> tree -> blob
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitnamespaces`](../guides/gitnamespaces.md)
- [`gitfaq`](../guides/gitfaq.md)
- [`gitremote-helpers`](../guides/gitremote-helpers.md)

## Fuente

- [gitglossary - A Git Glossary](https://git-scm.com/docs/gitglossary)
