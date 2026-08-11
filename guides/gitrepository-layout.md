---
title: "gitrepository-layout"
source: "https://git-scm.com/docs/gitrepository-layout"
section: "guides"
---

# `gitrepository-layout`

## Ejemplo de partida

```bash
biblioteca/
├── .git/
│   ├── HEAD
│   ├── config
│   ├── index
│   ├── objects/
│   └── refs/
└── README.md
```

Este caso usa `gitrepository-layout` para identificar los archivos y directorios internos de un repositorio. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: identificar los archivos y directorios internos de un repositorio.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
biblioteca/
├── .git/
│   ├── HEAD
│   ├── config
# …
```

Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitrevisions`](../guides/gitrevisions.md)
- [`gitmodules`](../guides/gitmodules.md)
- [`gitmailmap`](../guides/gitmailmap.md)

## Fuente

- [gitrepository-layout - Git Repository Layout](https://git-scm.com/docs/gitrepository-layout)
