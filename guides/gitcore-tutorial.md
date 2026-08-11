---
title: "gitcore-tutorial"
source: "https://git-scm.com/docs/gitcore-tutorial"
section: "guides"
---

# `gitcore-tutorial`

## Ejemplo de partida

```bash
blob=$(printf 'hola\n' | git hash-object -w --stdin)
printf '100644 blob %s\tREADME.md\n' "$blob" | git mktree
```

Este caso usa `gitcore-tutorial` para construir commits con objetos, árboles, el índice y referencias. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: construir commits con objetos, árboles, el índice y referencias.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
blob=$(printf 'hola\n' | git hash-object -w --stdin)
printf '100644 blob %s\tREADME.md\n' "$blob" | git mktree
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitcredentials`](../guides/gitcredentials.md)
- [`gitcvs-migration`](../guides/gitcvs-migration.md)

## Fuente

- [gitcore-tutorial - A Git core tutorial for developers](https://git-scm.com/docs/gitcore-tutorial)
