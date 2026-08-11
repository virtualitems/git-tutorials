---
title: "git sh-setup"
source: "https://git-scm.com/docs/git-sh-setup"
section: "scripting-and-helpers"
---

# `git sh-setup`

## Ejemplo de partida

```bash
. "$(git --exec-path)/git-sh-setup"
require_work_tree
```

Este caso usa `git sh-setup` para cargar funciones comunes para scripts de shell de Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: cargar funciones comunes para scripts de shell de Git.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
. "$(git --exec-path)/git-sh-setup"
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git stripspace`](../scripting-and-helpers/stripspace.md)
- [`git sh-i18n`](../scripting-and-helpers/sh-i18n.md)
- [`git url-parse`](../scripting-and-helpers/url-parse.md)

## Fuente

- [git-sh-setup - Common Git shell script setup code](https://git-scm.com/docs/git-sh-setup)
