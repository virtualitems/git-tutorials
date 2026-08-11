---
title: "gitnamespaces"
source: "https://git-scm.com/docs/gitnamespaces"
section: "guides"
---

# `gitnamespaces`

## Ejemplo de partida

```bash
GIT_NAMESPACE=curso-a git upload-pack /srv/git/biblioteca.git
GIT_NAMESPACE=curso-b git upload-pack /srv/git/biblioteca.git
```

Este caso usa `gitnamespaces` para aislar conjuntos de referencias dentro de un repositorio servidor. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: aislar conjuntos de referencias dentro de un repositorio servidor.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
GIT_NAMESPACE=<namespace> git upload-pack
GIT_NAMESPACE=<namespace> git receive-pack
```

Los elementos entre `<` y `>` se sustituyen por valores.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitremote-helpers`](../guides/gitremote-helpers.md)
- [`gitglossary`](../guides/gitglossary.md)
- [`gitsubmodules`](../guides/gitsubmodules.md)

## Fuente

- [gitnamespaces - Git namespaces](https://git-scm.com/docs/gitnamespaces)
