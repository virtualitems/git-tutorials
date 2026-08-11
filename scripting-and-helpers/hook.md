---
title: "git hook"
source: "https://git-scm.com/docs/git-hook"
section: "scripting-and-helpers"
---

# `git hook`

## Ejemplo de partida

```bash
git hook list pre-commit
git hook run pre-commit
```

Este caso usa `git hook` para enumerar o ejecutar hooks mediante Git. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: enumerar o ejecutar hooks mediante Git.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git hook run [--allow-unknown-hook-name] [--ignore-missing] [--to-stdin=<path>] [(-j|--jobs) <n>]
	<hook-name> [-- <hook-args>]
git hook list [--allow-unknown-hook-name] [-z] [--show-scope] <hook-name>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git interpret-trailers`](../scripting-and-helpers/interpret-trailers.md)
- [`git fmt-merge-msg`](../scripting-and-helpers/fmt-merge-msg.md)
- [`git mailinfo`](../scripting-and-helpers/mailinfo.md)

## Fuente

- [git-hook - Run Git hooks](https://git-scm.com/docs/git-hook)
