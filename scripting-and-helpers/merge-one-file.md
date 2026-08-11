---
title: "git merge-one-file"
source: "https://git-scm.com/docs/git-merge-one-file"
section: "scripting-and-helpers"
---

# `git merge-one-file`

## Ejemplo de partida

```bash
git merge-index git-merge-one-file -a
```

Este caso usa `git merge-one-file` para resolver una ruta durante una fusión de tres vías. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: resolver una ruta durante una fusión de tres vías.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git merge-one-file
```

Esta forma nombra la entrada que la operación espera.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git patch-id`](../scripting-and-helpers/patch-id.md)
- [`git mailsplit`](../scripting-and-helpers/mailsplit.md)
- [`git sh-i18n`](../scripting-and-helpers/sh-i18n.md)

## Fuente

- [git-merge-one-file - The standard helper program to use with git-merge-index](https://git-scm.com/docs/git-merge-one-file)
