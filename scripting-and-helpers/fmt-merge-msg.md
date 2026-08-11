---
title: "git fmt-merge-msg"
source: "https://git-scm.com/docs/git-fmt-merge-msg"
section: "scripting-and-helpers"
---

# `git fmt-merge-msg`

## Ejemplo de partida

```bash
git fetch origin main
git fmt-merge-msg --log < .git/FETCH_HEAD
```

Este caso usa `git fmt-merge-msg` para generar el mensaje de un commit de fusión. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: generar el mensaje de un commit de fusión.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git fmt-merge-msg [-m <message>] [--into-name <branch>] [--log[=<n>] | --no-log]
git fmt-merge-msg [-m <message>] [--log[=<n>] | --no-log] -F <file>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git hook`](../scripting-and-helpers/hook.md)
- [`git credential-store`](../scripting-and-helpers/credential-store.md)
- [`git interpret-trailers`](../scripting-and-helpers/interpret-trailers.md)

## Fuente

- [git-fmt-merge-msg - Produce a merge commit message](https://git-scm.com/docs/git-fmt-merge-msg)
