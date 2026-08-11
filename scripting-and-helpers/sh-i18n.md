---
title: "git sh-i18n"
source: "https://git-scm.com/docs/git-sh-i18n"
section: "scripting-and-helpers"
---

# `git sh-i18n`

## Ejemplo de partida

```bash
. "$(git --exec-path)/git-sh-i18n"
eval_gettext 'Procesando $archivo'
```

Este caso usa `git sh-i18n` para cargar funciones de internacionalización en scripts de shell. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: cargar funciones de internacionalización en scripts de shell.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
. "$(git --exec-path)/git-sh-i18n"
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git sh-setup`](../scripting-and-helpers/sh-setup.md)
- [`git patch-id`](../scripting-and-helpers/patch-id.md)
- [`git stripspace`](../scripting-and-helpers/stripspace.md)

## Fuente

- [git-sh-i18n - Git’s i18n setup code for shell scripts](https://git-scm.com/docs/git-sh-i18n)
