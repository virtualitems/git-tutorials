---
title: "githooks"
source: "https://git-scm.com/docs/githooks"
section: "guides"
---

# `githooks`

## Ejemplo de partida

```ini
# .git/hooks/pre-commit
#!/bin/sh
exec ./scripts/verificar-formato.sh
```

Este caso usa `githooks` para ejecutar programas en puntos definidos del flujo de Git. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: ejecutar programas en puntos definidos del flujo de Git.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
# .git/hooks/pre-commit
#!/bin/sh
exec ./scripts/verificar-formato.sh
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitignore`](../guides/gitignore.md)
- [`gitcli`](../guides/gitcli.md)
- [`gitmailmap`](../guides/gitmailmap.md)

## Fuente

- [githooks - Hooks used by Git](https://git-scm.com/docs/githooks)
