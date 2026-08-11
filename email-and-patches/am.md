---
title: "git am"
source: "https://git-scm.com/docs/git-am"
section: "email-and-patches"
---

# `git am`

## Ejemplo de partida

```bash
git am 0001-corrige-indice.patch
# Si aparece un conflicto:
git am --continue
```

Este caso usa `git am` para convertir una serie de parches de correo en commits. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: una serie de commits, parches o mensajes de correo.
- Operación: convertir una serie de parches de correo en commits.
- Comprobación: el receptor obtiene parches o commits con el orden, autoría y mensaje esperados.

## Modelo mental

Cada parche puede transportar autoría, mensaje y diferencias. El receptor valida, aplica y registra la serie en su propio historial.

Conserva el orden de la serie y separa autor de quien aplica el parche. Los conflictos se resuelven antes de continuar con el siguiente mensaje.

## Forma de referencia

```text
git am [--signoff] [--keep] [--[no-]keep-cr] [--[no-]utf8] [--[no-]verify]
	 [--[no-]3way] [--interactive] [--committer-date-is-author-date]
	 [--ignore-date] [--ignore-space-change | --ignore-whitespace]
	 [--whitespace=<action>] [-C<n>] [-p<n>] [--directory=<dir>]
# …
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior.

## Práctica

Genera una serie de dos commits en una rama de prueba. Inspecciona los archivos de parche y aplícalos en otro clon.

## Páginas relacionadas

- [`git format-patch`](../email-and-patches/format-patch.md)
- [`git imap-send`](../email-and-patches/imap-send.md)

## Fuente

- [git-am - Apply a series of patches from a mailbox](https://git-scm.com/docs/git-am)
