---
title: "git stripspace"
source: "https://git-scm.com/docs/git-stripspace"
section: "scripting-and-helpers"
---

# `git stripspace`

## Ejemplo de partida

```bash
printf 'Título  \n\n\nCuerpo\n' | git stripspace
```

Este caso usa `git stripspace` para normalizar espacios, líneas vacías y comentarios de un mensaje. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: normalizar espacios, líneas vacías y comentarios de un mensaje.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git stripspace [-s | --strip-comments]
git stripspace [-c | --comment-lines]
```

Los corchetes delimitan partes opcionales.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git url-parse`](../scripting-and-helpers/url-parse.md)
- [`git sh-setup`](../scripting-and-helpers/sh-setup.md)
- [`git sh-i18n`](../scripting-and-helpers/sh-i18n.md)

## Fuente

- [git-stripspace - Remove unnecessary whitespace](https://git-scm.com/docs/git-stripspace)
