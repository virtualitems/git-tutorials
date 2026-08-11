---
title: "git format-patch"
source: "https://git-scm.com/docs/git-format-patch"
section: "email-and-patches"
---

# `git format-patch`

## Ejemplo de partida

```bash
git format-patch origin/main..HEAD --output-directory parches/
```

Este caso usa `git format-patch` para representar commits como archivos de parche para correo. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: una serie de commits, parches o mensajes de correo.
- Operación: representar commits como archivos de parche para correo.
- Comprobación: el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.

## Modelo mental

Cada parche puede transportar autoría, mensaje y diferencias. El receptor valida, aplica y registra la serie en su propio historial.

Conserva el orden de la serie y separa autor de quien aplica el parche. Los conflictos se resuelven antes de continuar con el siguiente mensaje.

## Forma de referencia

```text
git format-patch [-k] [(-o|--output-directory) <dir> | --stdout]
		   [--no-thread | --thread[=<style>]]
		   [(--attach|--inline)[=<boundary>] | --no-attach]
		   [-s | --signoff]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Genera una serie de dos commits en una rama de prueba. Inspecciona los archivos de parche y aplícalos en otro clon.

## Páginas relacionadas

- [`git imap-send`](../email-and-patches/imap-send.md)
- [`git am`](../email-and-patches/am.md)
- [`git send-email`](../email-and-patches/send-email.md)

## Fuente

- [git-format-patch - Prepare patches for e-mail submission](https://git-scm.com/docs/git-format-patch)
