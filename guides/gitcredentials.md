---
title: "gitcredentials"
source: "https://git-scm.com/docs/gitcredentials"
section: "guides"
---

# `gitcredentials`

## Ejemplo de partida

```bash
git config --global credential.helper 'cache --timeout=900'
git config --show-origin --get-all credential.helper
```

Este caso usa `gitcredentials` para configurar la obtención y el almacenamiento de credenciales. Los nombres del ejemplo representan un repositorio de práctica. Sustitúyelos después de identificar qué objeto, referencia, ruta o valor de configuración representa cada uno.

## Qué se deriva del ejemplo

- Entrada: el estado de repositorio representado por el caso.
- Operación: configurar la obtención y el almacenamiento de credenciales.
- Comprobación: los comandos de inspección permiten relacionar el resultado con objetos, referencias, rutas o configuración.

## Modelo mental

La guía conecta comandos con objetos, referencias, rutas y configuración. El ejemplo sirve para observar una relación antes de nombrar la regla.

Cambia un solo elemento del caso y vuelve a observar el repositorio. La diferencia identifica la regla que controla ese elemento.

## Forma de referencia

```text
git config credential.https://example.com.username myusername
git config credential.helper "$helper $options"
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Reproduce el ejemplo en un repositorio temporal. Anota qué objeto, referencia, ruta o valor de configuración explica cada resultado.

## Páginas relacionadas

- [`gitcvs-migration`](../guides/gitcvs-migration.md)
- [`gitcore-tutorial`](../guides/gitcore-tutorial.md)
- [`gitdiffcore`](../guides/gitdiffcore.md)

## Fuente

- [gitcredentials - Providing usernames and passwords to Git](https://git-scm.com/docs/gitcredentials)
