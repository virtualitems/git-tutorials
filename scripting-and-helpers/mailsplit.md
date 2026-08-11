---
title: "git mailsplit"
source: "https://git-scm.com/docs/git-mailsplit"
section: "scripting-and-helpers"
---

# `git mailsplit`

## Ejemplo de partida

```bash
mkdir mensajes
git mailsplit -o mensajes serie.mbox
```

Este caso usa `git mailsplit` para dividir un buzón mbox o Maildir en mensajes. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: datos controlados por entrada estándar, argumentos o configuración.
- Operación: dividir un buzón mbox o Maildir en mensajes.
- Comprobación: la salida y el código de retorno distinguen el caso aceptado del rechazado.

## Modelo mental

Estos comandos resuelven una parte del flujo y suelen comunicarse mediante entrada estándar, salida estándar, configuración o códigos de salida.

Define entrada, salida y código de retorno como contrato del proceso. No dependas de texto orientado a personas cuando exista un formato para scripts.

## Forma de referencia

```text
git mailsplit [-b] [-f<nn>] [-d<prec>] [--keep-cr] [--mboxrd]
		-o<directory> [--] [(<mbox>|<Maildir>)…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Pasa una entrada controlada, captura salida y código de retorno, y repite la prueba con un caso válido y otro inválido.

## Páginas relacionadas

- [`git merge-one-file`](../scripting-and-helpers/merge-one-file.md)
- [`git mailinfo`](../scripting-and-helpers/mailinfo.md)
- [`git patch-id`](../scripting-and-helpers/patch-id.md)

## Fuente

- [git-mailsplit - Simple UNIX mbox splitter program](https://git-scm.com/docs/git-mailsplit)
