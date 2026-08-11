---
title: "git credential-cache"
source: "https://git-scm.com/docs/git-credential-cache"
section: "scripting-and-helpers"
---

# `git credential-cache`

## Ejemplo de partida

```bash
git config --global credential.helper 'cache --timeout=900'
```

Este caso usa `git credential-cache` para mantener credenciales durante un tiempo en memoria. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: mantener credenciales durante un tiempo en memoria.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git config credential.helper 'cache [<options>]'
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git credential-store`](../scripting-and-helpers/credential-store.md)
- [`git credential`](../scripting-and-helpers/credential.md)
- [`git fmt-merge-msg`](../scripting-and-helpers/fmt-merge-msg.md)

## Fuente

- [git-credential-cache - Helper to temporarily store passwords in memory](https://git-scm.com/docs/git-credential-cache)
