---
title: "git imap-send"
source: "https://git-scm.com/docs/git-imap-send"
section: "email-and-patches"
---

# `git imap-send`

## Ejemplo de partida

```bash
git format-patch --stdout origin/main..HEAD | git imap-send
```

Este caso usa `git imap-send` para enviar una colección de parches a una carpeta IMAP. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: una serie de commits, parches o mensajes de correo.
- Operación: enviar una colección de parches a una carpeta IMAP.
- Comprobación: el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.

## Modelo mental

Cada parche puede transportar autoría, mensaje y diferencias. El receptor valida, aplica y registra la serie en su propio historial.

Conserva el orden de la serie y separa autor de quien aplica el parche. Los conflictos se resuelven antes de continuar con el siguiente mensaje.

## Forma de referencia

```text
git imap-send [-v] [-q] [--[no-]curl] [(--folder|-f) <folder>]
git imap-send --list
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales.

## Práctica

Genera una serie de dos commits en una rama de prueba. Inspecciona los archivos de parche y aplícalos en otro clon.

## Páginas relacionadas

- [`git send-email`](../email-and-patches/send-email.md)
- [`git format-patch`](../email-and-patches/format-patch.md)
- [`git am`](../email-and-patches/am.md)

## Fuente

- [git-imap-send - Send a collection of patches from stdin to an IMAP folder](https://git-scm.com/docs/git-imap-send)
