---
title: "git send-email"
source: "https://git-scm.com/docs/git-send-email"
section: "email-and-patches"
---

# `git send-email`

## Ejemplo de partida

```bash
git send-email --to=lista@example.test parches/*.patch
```

Este caso usa `git send-email` para enviar parches por correo electrónico. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: una serie de commits, parches o mensajes de correo.
- Operación: enviar parches por correo electrónico.
- Comprobación: el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.

## Modelo mental

Cada parche puede transportar autoría, mensaje y diferencias. El receptor valida, aplica y registra la serie en su propio historial.

Conserva el orden de la serie y separa autor de quien aplica el parche. Los conflictos se resuelven antes de continuar con el siguiente mensaje.

## Forma de referencia

```text
git send-email [<options>] (<file>|<directory>)…
git send-email [<options>] <format-patch-options>
git send-email --dump-aliases
git send-email --translate-aliases
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Genera una serie de dos commits en una rama de prueba. Inspecciona los archivos de parche y aplícalos en otro clon.

## Páginas relacionadas

- [`git imap-send`](../email-and-patches/imap-send.md)
- [`git format-patch`](../email-and-patches/format-patch.md)

## Fuente

- [git-send-email - Send a collection of patches as emails](https://git-scm.com/docs/git-send-email)
