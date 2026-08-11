---
title: "gitk"
source: "https://git-scm.com/docs/gitk"
section: "graphical-tools"
---

# `gitk`

## Ejemplo de partida

```bash
gitk --all
```

Este caso usa `gitk` para explorar el historial y sus relaciones en una interfaz gráfica. Los nombres de archivo, revisiones, ramas y direcciones del ejemplo representan valores que debes sustituir por los de tu repositorio.

## Qué se deriva del ejemplo

- Entrada: el repositorio y la vista u operación elegida en la interfaz.
- Operación: explorar el historial y sus relaciones en una interfaz gráfica.
- Comprobación: los comandos de consulta confirman el mismo estado que presenta la interfaz.

## Modelo mental

La interfaz presenta operaciones que también existen en el modelo de objetos, índice, referencias y commits. La vista cambia; el repositorio conserva el mismo estado.

Relaciona cada acción de la interfaz con índice, commit o referencia. Usa una consulta de Git para comprobar el cambio de estado.

## Forma de referencia

```text
gitk [<options>] [<revision-range>] [--] [<path>…]
```

Los elementos entre `<` y `>` se sustituyen por valores. Los corchetes delimitan partes opcionales. Los puntos suspensivos permiten repetir el elemento anterior. El separador `--` termina las opciones y permite tratar lo que sigue como rutas.

## Práctica

Realiza una operación en la interfaz y verifica el resultado con `git status`, `git log` o `git show`.

## Páginas relacionadas

- [`gitweb`](../graphical-tools/gitweb.md)
- [`git instaweb`](../graphical-tools/instaweb.md)
- [`git gui`](../graphical-tools/gui.md)

## Fuente

- [gitk - The Git repository browser](https://git-scm.com/docs/gitk)
