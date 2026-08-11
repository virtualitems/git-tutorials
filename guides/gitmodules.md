---
title: "gitmodules"
source: "https://git-scm.com/docs/gitmodules"
section: "guides"
---

# `gitmodules`

## Ejemplo de partida

```ini
[submodule "temas/base"]
    path = temas/base
    url = https://example.test/equipo/tema.git
```

Este caso usa `gitmodules` para declarar la ruta, URL y comportamiento de submódulos. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: declarar la ruta, URL y comportamiento de submódulos.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
[submodule "temas/base"]
    path = temas/base
    url = https://example.test/equipo/tema.git
```

Los corchetes delimitan partes opcionales.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitrepository-layout`](../guides/gitrepository-layout.md)
- [`gitmailmap`](../guides/gitmailmap.md)
- [`gitrevisions`](../guides/gitrevisions.md)

## Fuente

- [gitmodules - Defining submodule properties](https://git-scm.com/docs/gitmodules)
