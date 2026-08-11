---
title: "git mailinfo"
source: "https://git-scm.com/docs/git-mailinfo"
section: "scripting-and-helpers"
---

# `git mailinfo`

## Ejemplo de partida

```bash
git mailinfo mensaje.txt cambio.patch < correo.eml
```

Este caso usa `git mailinfo` para separar metadatos, mensaje y parche de un correo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: separar metadatos, mensaje y parche de un correo.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git mailinfo [-k|-b] [-u | --encoding=<encoding> | -n]
	       [--[no-]scissors] [--quoted-cr=<action>]
	       <msg> <patch>
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git mailsplit`](../scripting-and-helpers/mailsplit.md)
- [`git interpret-trailers`](../scripting-and-helpers/interpret-trailers.md)
- [`git merge-one-file`](../scripting-and-helpers/merge-one-file.md)

## Fuente

- [git-mailinfo - Extracts patch and authorship from a single e-mail message](https://git-scm.com/docs/git-mailinfo)
