---
title: "gitattributes"
source: "https://git-scm.com/docs/gitattributes"
section: "guides"
---

# `gitattributes`

## Ejemplo de partida

```ini
# .gitattributes
*.txt text eol=lf
*.bin binary
docs/*.md diff=markdown
```

Este caso usa `gitattributes` para asignar atributos a rutas para diff, merge, exportación y filtros. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: asignar atributos a rutas para diff, merge, exportación y filtros.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
# .gitattributes
*.txt text eol=lf
*.bin binary
docs/*.md diff=markdown
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitcli`](../guides/gitcli.md)
- [`gitworkflows`](../guides/gitworkflows.md)
- [`githooks`](../guides/githooks.md)

## Fuente

- [gitattributes - Defining attributes per path](https://git-scm.com/docs/gitattributes)
