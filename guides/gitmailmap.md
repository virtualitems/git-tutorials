---
title: "gitmailmap"
source: "https://git-scm.com/docs/gitmailmap"
section: "guides"
---

# `gitmailmap`

## Ejemplo de partida

```bash
Ana Torres <ana@example.test> <ana@correo-antiguo.test>
```

Este caso usa `gitmailmap` para unificar nombres y correos que representan a una misma persona. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: unificar nombres y correos que representan a una misma persona.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
Ana Torres <ana@example.test> <ana@correo-antiguo.test>
```

Los elementos entre `<` y `>` se sustituyen por valores.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitmodules`](../guides/gitmodules.md)
- [`gitignore`](../guides/gitignore.md)
- [`gitrepository-layout`](../guides/gitrepository-layout.md)

## Fuente

- [gitmailmap - Map author/committer names and/or E-Mail addresses](https://git-scm.com/docs/gitmailmap)
