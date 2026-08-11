---
title: "gitcli"
source: "https://git-scm.com/docs/gitcli"
section: "guides"
---

# `gitcli`

## Ejemplo de partida

```bash
git log main..tema -- docs/
git restore --source=HEAD -- README.md
```

Este caso usa `gitcli` para interpretar opciones, revisiones y rutas en la línea de comandos. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: interpretar opciones, revisiones y rutas en la línea de comandos.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
git log main..tema -- docs/
git restore --source=HEAD -- README.md
```

El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`githooks`](../guides/githooks.md)
- [`gitattributes`](../guides/gitattributes.md)
- [`gitignore`](../guides/gitignore.md)

## Fuente

- [gitcli - Git command-line interface and conventions](https://git-scm.com/docs/gitcli)
