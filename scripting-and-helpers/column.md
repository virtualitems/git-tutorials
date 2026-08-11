---
title: "git column"
source: "https://git-scm.com/docs/git-column"
section: "scripting-and-helpers"
---

# `git column`

## Ejemplo de partida

```bash
printf '%s\n' main develop release | git column --mode=column
```

Este caso usa `git column` para organizar líneas de entrada en columnas. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: organizar líneas de entrada en columnas.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git column [--command=<name>] [--[raw-]mode=<mode>] [--width=<width>]
	     [--indent=<string>] [--nl=<string>] [--padding=<n>]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git credential`](../scripting-and-helpers/credential.md)
- [`git check-ref-format`](../scripting-and-helpers/check-ref-format.md)
- [`git credential-cache`](../scripting-and-helpers/credential-cache.md)

## Fuente

- [git-column - Display data in columns](https://git-scm.com/docs/git-column)
