---
title: "gitremote-helpers"
source: "https://git-scm.com/docs/gitremote-helpers"
section: "guides"
---

# `gitremote-helpers`

## Ejemplo de partida

```bash
git remote add datos transporte::direccion
git fetch datos
# Git busca un ejecutable llamado git-remote-transporte
```

Este caso usa `gitremote-helpers` para implementar transportes mediante procesos auxiliares. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: implementar transportes mediante procesos auxiliares.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
git remote-<transport> <repository> [<URL>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitsubmodules`](../guides/gitsubmodules.md)
- [`gitnamespaces`](../guides/gitnamespaces.md)
- [`gittutorial`](../guides/gittutorial.md)

## Fuente

- [gitremote-helpers - Helper programs to interact with remote repositories](https://git-scm.com/docs/gitremote-helpers)
