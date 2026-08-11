---
title: "gitcvs-migration"
source: "https://git-scm.com/docs/gitcvs-migration"
section: "guides"
---

# `gitcvs-migration`

## Ejemplo de partida

```bash
git cvsimport -C biblioteca modulo
cd biblioteca
git log --oneline --all
```

Este caso usa `gitcvs-migration` para trasladar prácticas y datos de CVS a Git. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: trasladar prácticas y datos de CVS a Git.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
git cvsimport *
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitdiffcore`](../guides/gitdiffcore.md)
- [`gitcredentials`](../guides/gitcredentials.md)
- [`giteveryday`](../guides/giteveryday.md)

## Fuente

- [gitcvs-migration - Git for CVS users](https://git-scm.com/docs/gitcvs-migration)
