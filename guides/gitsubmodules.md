---
title: "gitsubmodules"
source: "https://git-scm.com/docs/gitsubmodules"
section: "guides"
---

# `gitsubmodules`

## Ejemplo de partida

```bash
superproyecto/.gitmodules
superproyecto/temas/base/.git
```

Este caso usa `gitsubmodules` para entender el modelo de repositorios anidados como submódulos. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: entender el modelo de repositorios anidados como submódulos.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
.gitmodules, $GIT_DIR/config
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gittutorial`](../guides/gittutorial.md)
- [`gitremote-helpers`](../guides/gitremote-helpers.md)
- [`gittutorial-2`](../guides/gittutorial-2.md)

## Fuente

- [gitsubmodules - Mounting one repository inside another](https://git-scm.com/docs/gitsubmodules)
