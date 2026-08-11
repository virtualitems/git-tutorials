---
title: "gittutorial"
source: "https://git-scm.com/docs/gittutorial"
section: "guides"
---

# `gittutorial`

## Ejemplo de partida

```bash
git init -b main
printf 'Biblioteca\n' > README.md
git add README.md
git commit -m "Inicia el proyecto"
```

Este caso usa `gittutorial` para recorrer el ciclo de crear, registrar, inspeccionar y compartir cambios. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: recorrer el ciclo de crear, registrar, inspeccionar y compartir cambios.
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

- [`gittutorial-2`](../guides/gittutorial-2.md)
- [`gitsubmodules`](../guides/gitsubmodules.md)
- [`gitworkflows`](../guides/gitworkflows.md)

## Fuente

- [gittutorial - A tutorial introduction to Git](https://git-scm.com/docs/gittutorial)
