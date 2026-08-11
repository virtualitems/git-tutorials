---
title: "git interpret-trailers"
source: "https://git-scm.com/docs/git-interpret-trailers"
section: "scripting-and-helpers"
---

# `git interpret-trailers`

## Ejemplo de partida

```bash
printf '%s\n' 'Corrige el índice' | git interpret-trailers --trailer 'Reviewed-by: Ana <ana@example.test>'
```

Este caso usa `git interpret-trailers` para analizar y añadir campos al final de mensajes de commit. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: analizar y añadir campos al final de mensajes de commit.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git interpret-trailers [--in-place] [--trim-empty]
			[(--trailer (<key>|<key-alias>)[(=|:)<value>])…]
			[--parse] [<file>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git mailinfo`](../scripting-and-helpers/mailinfo.md)
- [`git hook`](../scripting-and-helpers/hook.md)
- [`git mailsplit`](../scripting-and-helpers/mailsplit.md)

## Fuente

- [git-interpret-trailers - Add or parse structured information in commit messages](https://git-scm.com/docs/git-interpret-trailers)
