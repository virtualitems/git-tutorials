---
title: "git patch-id"
source: "https://git-scm.com/docs/git-patch-id"
section: "scripting-and-helpers"
---

# `git patch-id`

## Ejemplo de partida

```bash
git show HEAD | git patch-id --stable
```

Este caso usa `git patch-id` para calcular una identidad estable para el contenido de un parche. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: calcular una identidad estable para el contenido de un parche.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git patch-id [--stable | --unstable | --verbatim]
```

Los corchetes delimitan partes opcionales.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git sh-i18n`](../scripting-and-helpers/sh-i18n.md)
- [`git merge-one-file`](../scripting-and-helpers/merge-one-file.md)
- [`git sh-setup`](../scripting-and-helpers/sh-setup.md)

## Fuente

- [git-patch-id - Compute unique IDs for patches](https://git-scm.com/docs/git-patch-id)
